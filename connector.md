# connector.md

> Owner: Admin. Second in the chain. Given the intent, names which sources are needed and reports
> which are available. **Never fetches, never interprets** — that is the source agents' job.

## Job

1. Take the intent from the guardrail
2. Look it up in the source map below
3. Report which of the needed sources are connected
4. If all needed sources are connected, hand off to the source agents
5. If any needed source is missing, return a connect prompt and stop the chain

## Source map, by artifact group

Grouped the way the 12 Sep catalogue groups them. Full artifact list is in `artifact-picker.md`;
what each source holds is in `sources.md`.

| Customer is asking about | Source(s) needed | Day-0? |
|---|---|---|
| Shop income, money in, sales patterns (A-01–10) | QR settlement, SMS | Money in via SMS: yes. QR settlement: connects on first ask |
| Margin, "am I making money" (A-11) | No source yet — needs supplier data | Not available |
| Festivals, stock planning (A-12–13) | Season calendar | Reference data, always available |
| Our loan — EMI, balance, schedule, documents, RM (A-14–22, A-71–75) | InPrime records | Yes, for existing customers |
| Comparing or reducing loan cost (A-23–27, A-30) | InPrime records + Credit bureau | Bureau: yes. InPrime: yes |
| EMI calculator (A-28) | InPrime records only — it computes from terms already fetched | Yes |
| Eligibility, applying, checklist (A-29, A-31–32, A-76–77) | InPrime records | Yes |
| Government schemes (A-33) | **Not named — gap.** See `sources.md` | Not available |
| Credit score, report, enquiries (A-34–40, A-65–69) | Credit bureau | Yes |
| Single transaction, bounce risk (A-41–42) | Account Aggregator + SMS | Yes |
| Is this message real (A-43) | The message itself | Not a connector question |
| Reminders (A-44) | Whatever source holds the underlying date | Depends on the artifact reminded from |
| Requests, disputes (A-45) | InPrime records | Yes |
| Insurance cover (A-46) | **Not named — gap.** See `sources.md` | Not available |
| Talk to a person (A-47) | None | Always available |
| Bank balance, transactions, trends, supplier payments (A-52–64) | Account Aggregator | Yes |
| Score improvement plan, explainer video (A-69–70) | Credit bureau + Editorial content library | Yes |

## When a source is not connected

- Name what cannot be seen
- Name **specifically** what connecting would unlock — never permission in the abstract
- Offer to connect
- **Never let the chain continue with a partial answer dressed as a whole one**

> *I can check your GST returns — what you filed, what is pending, and how your turnover moved —
> if you connect your GST.*

## When a source is connected but thin

Pass the gap forward. The story builder must say what is missing, not paper over it. The bureau is
the most common case of this — see `sources.md` for its fill rates.

## Two open items

1. **Two artifacts have no named source at all** — A-33 (government schemes) and A-46 (insurance
   cover). Until a source is named, these always return "not connected," same as any other missing
   source. Do not build a fallback that answers from general knowledge instead
2. **Subscription tier is not part of this map.** Per `master.md`, the freemium model discussed
   25–27 Aug is not resolved here. Until it is, this file treats every source as available to every
   customer regardless of tier
