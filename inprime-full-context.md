# InPrime Customer App — full context

Everything established to date. Paste into a new session, or hand to someone joining the project.
**As of 12 September 2026.**

---

## 1 · What this is

| | |
|---|---|
| **Company** | InPrime Finserv — an NBFC lending to the "informal prime" segment |
| **Customer** | Indian shopkeepers. Kirana, medical, mobile, textile, restaurant, hardware, salon, dairy |
| **Product** | A conversational AI app. Not a dashboard — the customer asks, the assistant answers with a short line of text plus, sometimes, one visual artifact |
| **My role** | Arnav Srivastava, Product Intern |
| **Driving the architecture** | Siddharth |
| **UI/UX** | Dnyaneshwar — owns the HTML/CSS prototype and the artifact design catalogue |
| **Languages** | Kannada, Hindi, English |

**The customer, as written into the grounding document**
- Reads slowly. Reads English barely
- Holding the phone at a counter, one hand, customers watching
- May be using a money app for the first time
- Has heard of CIBIL and is slightly afraid of it
- Cares more about money owed to them and money going out than about a credit score

---

## 2 · Decisions by meeting

| Date | What was decided |
|---|---|
| **25 Aug** | ChatGPT-style app concept. Freemium model — free tier with a basic loan connector, ₹99 paid tier unlocks full LLM and more connectors including the bureau |
| **26 Aug** | Cards → tables. 40–50 use cases to be documented |
| **27 Aug** | Chat-first pivot locked. Day-0 connectors named: **SMS, Credit bureau, Account Aggregator**. Field research: shopkeepers prefer **typing over voice**, want quick payment info over feature depth |
| **29 Aug** | Reversed 26 Aug — tiles and cards, tables only when the data demands it. Connectors open conversationally via bottom sheets. Credit score via PAN input + AI insight. Good/warning/bad grading |
| **2 Sep** | Onboarding flow locked: language → walkthrough videos → OTP → occupation capture. HTML/CSS prototype and grounding doc planned |
| **4 Sep** | No content — mic check only |
| **8 Sep** | **Artifacts must be use-case specific, not generic containers.** Named, use-case-bound, fixed labels. Onboarding simplified — minimal typing, compact nudges. EMI calculator prioritized as the one interactive artifact |
| **10 Sep** | **Multi-agent architecture.** One instruction file per agent, dispatched by a master file, plus an admin-configurable layer above the system prompt |

**Siddharth's instruction on how to write the docs (10 Sep):** concrete not open-ended, in plain English, guardrailed but not too strict, guardrails are one part not the whole, match the architecture.

**Unresolved contradiction:** 27 Aug's field finding — typing over voice — has never been reconciled against the rest of the project's framing of voice as the primary input. Both statements are on record. Worth settling before treating Indic ASR as the top-priority unowned dependency.

---

## 3 · The architecture

### Runtime chain

```
master.md
  → 1 guardrail.md       in: message         out: in_scope | refusal_text
  → 2 connector.md       in: intent          out: sources[], missing[]
  → 3 sources.md         in: named source    out: values{}, gaps[]
  → 4 artifact-picker.md in: intent+values   out: artifact name | null
  → 5 story.md           in: everything      out: text, follow_ups[]
  → code renders
```

Any agent can stop the chain: the guardrail by refusing, the connector by finding nothing connected, the picker by returning none. **None of the three is a failure state.** Steps 2 and 3 may loop.

### The files — status as of this session

| File | Job | Owner | Status |
|---|---|---|---|
| `master.md` | Dispatches the agents. Holds the rules binding all of them | Engineering | **Drafted this session** |
| `guardrail.md` | Is this in scope. Refuses or passes on | Admin (Siddharth per the log) | **Drafted this session** |
| `connector.md` | Names the data needed. Checks availability | Admin (Siddharth per the log) | **Drafted this session** |
| `sources.md` | What each source holds and cannot answer | Engineering | **Drafted this session** |
| `artifact-picker.md` | Chooses one artifact, or none | Admin (Siddharth per the log) | **Drafted this session** |
| `story.md` | Writes the text around the artifact | Admin | Not drafted. Notion log assigns this to Siddharth |
| `voice.md` | Shared tone. Read by guardrail and story | Admin | Not drafted. Notion log assigns this to Siddharth |
| `intent-set.md` | 71 intents, phrasings, scope | Admin | Exists in Notion (separate page), not yet reconciled into a standalone file |
| `artifacts.md` | The artifact catalogue, read by the picker | Admin | Superseded by the 12 Sep design file — see §6 |
| `copy-deck.md` | 88 fixed strings, three languages | Admin + compliance | Exists, English only. Kannada/Hindi blocking |
| `data-contracts.md` | Fields, types, missing-field behaviour | Engineering | 15 of 39 written |

**Note:** the five files drafted this session were built by lifting sections out of the Grounding Document v5 and reconciling them against the 12 Sep artifact catalogue and the full meeting log. Two of the five (`guardrail.md`, `connector.md`, `artifact-picker.md`) are, per the Notion meeting log, actions assigned to **Siddharth, not me** — worth a quick check on ownership before these are treated as final.

### The rules that bind every agent

1. **No agent states a number.** Source agents return values, code renders them
2. **No agent invents an artifact.** The picker chooses from the list or returns none
3. **No agent guesses.** Below the confidence floor, the answer is a person
4. Every response ends with two or three follow-up questions
5. **Artifacts are built by deterministic code, not the model.** The model names a container, code fills it via the data contract
6. **Only the EMI calculator (A-28) is interactive.** Everything else is display-only

### Day-0 versus later

Per 27 Aug: **Day-0 = SMS, Credit bureau, Account Aggregator.** QR settlement, DigiLocker and the season calendar connect only when the customer first asks something that needs them.

### The guardrail test

Not *is this topic on a list*. The test is: **does answering this help the customer with their money or their business?** Political and policy questions affecting their trade are allowed. When in doubt, pass it through.

---

## 4 · The data reality — this constrains everything

Measured on **130 real CRIF accounts**:

| Field | Fill rate |
|---|---|
| EMI amount | 27% |
| Credit limit | 2% |
| Payment history | 84% carry none |
| **Payment due dates** | **Absent entirely** |

**Three things that can never be computed**
- **Credit utilisation** — the limit is missing
- **Other lenders' due dates** — ask the customer, then remember
- **Score point values** — the bureau publishes none. State effects, never invented points

---

## 5 · Field research

Five shops surveyed, 15 questions.

- **4 of 5 shops give no udhaar.** Undercut the P0 headline feature. Recommendation: pause it, test a second cohort
- **Multi-QR aggregation is the only confirmed gap.** No app shows the combined total across 2–3 QR codes into one account
- **Shopkeepers prefer typing over voice** (27 Aug) — see the unresolved contradiction in §2
- Output: `InPrime-Field-Research.pptx`, 11 slides

---

## 6 · The artifact catalogue — now 77 artifacts, not 44

**This session's key discovery:** the file you'd been treating as a design-theme reference
(`InPrime Artifacts.dc.html`) is the finalized, rendered design catalogue — built after the six
group prompts from the previous session. It supersedes the 44-item "Artifacts" Notion page.

| | |
|---|---|
| **Artifacts** | 77, IDs A-01 to A-77 |
| **Shared components** (patterns, never picked directly) | 18, IDs C-01 to C-18 |
| **Sections** | Understand my shop · Plan the season · Track my loans · Pay less, pay smarter · Borrow more · Understand my credit score · Stay safe and on time · Get help · Before/while the assistant works · G1 Income and cashflow · G2 Bank statement · G3 Bureau alerts · G4 Bureau and score · G5 Existing InPrime loan · G6 InPrime products |
| **Full index with sources** | `artifact-picker.md`, drafted this session |

**Two gaps this catalogue surfaced, not present in any earlier document:**

| Gap | Artifact | Missing |
|---|---|---|
| Government scheme data | A-33 Scheme list | No source holds scheme eligibility anywhere |
| Insurance / cover data | A-46 Cover card | No source holds policy or cover data |

**One structural correction:** A-65 through A-68 (new loan detected, overdue, payment marked, loan closed) are **push alerts triggered by bureau data changes**, not artifacts chosen in response to a question. They need a separate trigger path outside the guardrail→connector→picker chain.

---

## 7 · Notion documents

All under **Customer App** `392b05e533a2816eb1f9f511fd05b242`.

| Doc | ID | State |
|---|---|---|
| Grounding Document — InPrime AI | `3d2b05e5-33a2-8171-8972-cbb863fb6763` | v5. Multi-agent instruction set, file map, instruction-file flow chart, test suite, open positions |
| Artifacts | `3d0b05e5-33a2-8176-ae7c-d029a9178e25` | 38 rows. **Superseded by the 77-artifact catalogue in the uploaded design file — needs reconciling** |
| UI Elements — artifact catalogue | `3cfb05e5-33a2-81b9-81a2-fc9e2a3e4517` | 57 elements, 12 sections |
| Use Cases — conversational app | `3c9b05e5-33a2-818d-af8d-e6518aea9fe4` | 180 questions, 17 groups A–Q |
| Third-party stack | `3d4b05e5-33a2-8141-9bc6-f59979c3190d` | Vendors by layer with status |
| Intent set | `3d7b05e5-33a2-8134-8140-c4fcd0a44045` | 71 intents, 58 at launch |
| Artifact data contracts | `3d7b05e5-33a2-8100-bb49-e8e2fc288689` | 15 of 39 |
| Copy deck | `3d7b05e5-33a2-8156-bc19-d418a1ef4313` | 88 strings, English only |
| Evaluation set | `3d7b05e5-33a2-813f-a75a-e3d58c492752` | 94 cases, 8 categories, 4 blocking |
| Occupation capture | `3d7b05e5-33a2-8115-9b41-f5f55cd81988` | ~80 occupations, 12 groups |
| Shopkeeper Survey | `3c3b05e5-33a2-81c2-86cb-c02eb544eed6` | 15 questions |
| Conversations & Meetings Log | `c81c8eb8-8610-435e-a28b-54de27cde19e` | Database. Most recent entry: 10 Sep. **No 11 or 12 Sep entry exists** |

---

## 8 · Files produced locally, this session and prior

| File | What it is |
|---|---|
| `master.md` | Dispatches the agents, rules that bind them, file map, Day-0 note, subscription-gating flag |
| `guardrail.md` | The in-scope test, allow/refuse tables, Siddharth's political-question example, refusal format |
| `connector.md` | Source map by artifact group, the two named gaps, subscription flag |
| `sources.md` | What each source holds/cannot answer, the two gaps, vendor stack, the typing-vs-voice flag |
| `artifact-picker.md` | Full 77-artifact index with sources, components list, pairs, return-none list |
| `instruction-file-flow.html` | How the instruction files load each other — runtime chain vs reference files |
| `artifact-design-prompts.md` | Preamble + six group prompts that produced the 12 Sep 77-artifact catalogue |
| `InPrime-Field-Research.pptx` | 11 slides, field research findings |
| `release-1-wireframes.html`, `chat-first-app-wireframes.html`, `conversational-workflows.html`, `interaction-ideas.html`, `app-flows-29aug.html` | Earlier wireframe and flow explorations |

---

## 9 · Vendor stack

| Layer | Vendor | Status |
|---|---|---|
| LLM | OpenAI API | **Decided** |
| Credit bureau | CRIF B2B2C | **Decided** |
| Account Aggregator | Digitap | **Decided** |
| SMS parsing | FinBox or Think360 | Not chosen |
| DigiLocker | Digio · Signzy · Setu · Perfios · IDfy | Not chosen |
| QR settlement | Acquirer or soundbox partner | Not started |
| Indic speech | Bhashini · Sarvam · AI4Bharat · Reverie | **Unowned — urgency now in question, see §2** |
| Government schemes | — | **Not started, new** |
| Insurance / cover | — | **Not started, new** |

---

## 10 · Open flags, ranked

| # | Flag | Why it matters |
|---|---|---|
| 1 | **Typing vs voice contradiction** | 27 Aug field data says typing is preferred; the rest of the project frames voice as primary. Unreconciled |
| 2 | **Subscription gating absent from the agent chain** | The freemium model (25/27 Aug) names a paywall; nothing in `connector.md` checks tier before naming a source |
| 3 | **Two artifacts with no source** | A-33 (schemes), A-46 (insurance) — surfaced this session |
| 4 | **Bureau alerts forced through the wrong chain** | A-65–68 are push events, not question-driven picks |
| 5 | **"Never recommend" vs comparative advice** | The guardrail technically forbids the most trust-building answer in the product. Needs a legal position |
| 6 | **"Powered by Crisil" on the score gauge** | Should read CRIF. Customer-facing. Unfixed since August |
| 7 | **Artifacts doc un-merge** | 10 changes defined per the 8 Sep decision, not yet approved — and now the whole doc is superseded by the 77-item catalogue anyway |
| 8 | **Ownership of the 5 drafted files** | The Notion log assigns guardrail/connector/picker actions to Siddharth, not me |

---

## 11 · Pending work

**Finish before starting anything new**

| Item | State |
|---|---|
| Data contracts | 24 of 39 missing |
| Copy deck translation | Kannada and Hindi. Blocking |
| Reconcile the two artifact catalogues | 38-item Notion page vs 77-item design file |

**New docs recommended, none started**

| Tier | Doc |
|---|---|
| Blocking Release 1 | `story.md`, `voice.md` — assigned to Siddharth, not drafted |
| Blocking Release 1 | Consent and permission flow — AA, SMS, DigiLocker, bureau. Regulatory, unwritten |
| Blocking Release 1 | Admin console spec |
| Blocking Release 1 | Release 1 scope |
| Before prototype testing | Onboarding / cold start, empty/error/offline states, trust answers, escalation SOP, analytics plan |
| Later | Second cohort field plan, competitive teardown |

---

## 12 · Working notes and gotchas

**Notion**
- Content inside `<details>` toggles is not reachable by `update_content` search-replace. Use `replace_content` for whole-page rewrites
- Table cells match on inner text only — never include `<td>` tags in `old_str`
- `notion-query-meeting-notes` requires a Business-plan connection; use `notion-query-data-sources` with SQL mode against the meetings log's `collection://` URL instead

**Environment**
- The Linux workspace (bash) has been broken since a Windows update on 8 September — cannot reach the outputs folder. Write tool used directly throughout
- Audio transcription is unavailable — HuggingFace, openaipublic and alphacephei all return 403 through the proxy

**Style the user has asked for, repeatedly**
- Short, point-wise, one sentence per point
- Tables and flowcharts over paragraphs
- Say "customer," never "her" or "she"
- No complexity for its own sake
- Numbering must be correct and sequential
