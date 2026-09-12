# sources.md

> Owner: Engineering. Read by the connector agent and the source agents. Never states a number
> itself — it returns values, which code renders.
> Sources below are cross-checked against the 12 Sep artifact catalogue (A-01 to A-77). Two gaps
> surfaced that were not in any earlier version of this file — flagged at the bottom.

## What each source holds

| Source | Day-0 | Holds | Cannot answer |
|---|---|---|---|
| **InPrime records** | Yes, for existing customers | Our loan in full — EMI, dates, mandate, charges, schedule, requests, RM contact | — |
| **Credit bureau · CRIF** | Yes | Every loan in their name, balance, tenure, overdue, enquiries, score, reason codes | EMI amount on 27% of accounts · credit limit on 2% · 84% carry no payment history · **due dates absent entirely** |
| **Account Aggregator** | Yes | Balances, recent transactions, recurring debits, business-transaction volume, average balance trend, interest credited, supplier payments, top payers/payees | Thin coverage for cooperative banks |
| **SMS** | Yes | Income credits, recurring debits, suspicious messages | Anything not sent as SMS |
| **QR settlement** | No — connects on first relevant question | Money in, by provider, with settlement timing | — |
| **DigiLocker** | No | Aadhaar, PAN, licence, insurance, Udyam | Anything not already in the locker |
| **Season calendar** | No, general reference | Festivals, school terms, market days, by district | — |
| **Editorial content library** | No, general reference | Short explainer videos — what a bureau reason code means, in plain language | Personalised advice. It explains a concept, it does not read the customer's own report |

## Two gaps this catalogue surfaced

Not caused by this rewrite — surfaced by it. Both artifacts existed before 12 Sep; neither had a
named source.

| Gap | Needed by | What is missing |
|---|---|---|
| **Government scheme data** | A-33 Scheme list — *"schemes I qualify for," "is there a cheaper government loan"* | No source holds scheme eligibility rules or scheme lists today. Needs a vendor or a maintained internal list |
| **Insurance / cover data** | A-46 Cover card — *"do I have insurance," "am I covered for hospital"* | No source holds policy or cover data. Likely DigiLocker once populated, but DigiLocker's insurance holding is unconfirmed in practice, not just in principle |

Until named, both artifacts return **none is connected** — the same as any other missing source —
not a silent guess.

## Three things that can never be computed

- **Credit utilisation** — the limit is missing on 98% of bureau accounts. Never imply otherwise
- **Other lenders' due dates** — the bureau carries none. Ask the customer once, then remember
- **Score point values** — the bureau publishes none. State effects, never invented points

## Not a source in the usual sense

Two artifacts read something other than a customer data source:

| Artifact | What it actually reads |
|---|---|
| A-43 Fraud result | The forwarded message itself, not a stored customer record |
| A-47 Callback card | Nothing — it routes to a person, it does not answer from data |

## Vendor stack

| Layer | Vendor | Status |
|---|---|---|
| LLM | OpenAI API | Decided |
| Credit bureau | CRIF B2B2C | Decided |
| Account Aggregator | Digitap | Decided |
| SMS parsing | FinBox or Think360 | Not chosen |
| DigiLocker | Digio · Signzy · Setu · Perfios · IDfy | Not chosen |
| QR settlement | Acquirer or soundbox partner | Not started |
| Indic speech | Bhashini · Sarvam · AI4Bharat · Reverie | Unowned |
| Government schemes | — | Not started. New, surfaced 12 Sep |
| Insurance / cover | — | Not started. New, surfaced 12 Sep |

## One flag from the field, not yet reconciled

The 27 Aug meeting log records that field research found shopkeepers **prefer typing over voice**
and want quick payment information over feature depth. This instruction set and the wider grounding
document elsewhere describe voice as the primary input. The two statements have not been reconciled
in any document reviewed for this draft. Worth resolving before the ASR vendor decision is treated
as urgent as it currently is.
