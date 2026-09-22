# intents.md

Runs between the guardrail and the connector. Turns a message into **one named intent**. Without
this step the chain cannot run — the connector looks up an intent, and nothing else produces one.

The phrasings per intent live in the intent set. This file is the rules for choosing.

## Sequence

1. Take the message the guardrail passed
2. Match it to one intent
3. Return the intent, the confidence, and the slots you could fill
4. If you cannot match with confidence, ask — do not guess

## Output

```
{ intent, confidence, slots: { period, lender, account, amount }, alternatives }
```

## Intent groups

| Group | Covers | Typical slot |
|---|---|---|
| `income.*` | What came in, when, from where, who paid | period |
| `outflow.*` | What went out, what is due, who was paid | period |
| `loan.*` | EMI, balance, schedule, documents, one loan or all | lender |
| `cost.*` | Rates, interest, closing, savings, calculator | lender |
| `borrow.*` | Eligibility, application, what is pending | — |
| `score.*` | Score, movement, reasons, bands, report | — |
| `bank.*` | Balance, transactions, charges, trends | account, period |
| `payments.*` | What accepting payments costs. Provider fees, device rental | period |
| `protect.*` | Is this real, unknown charge, disputes, cover | — |
| `product.*` | What we offer, how to apply, who to contact | — |
| `learn.*` | What a term means, how something works | — |
| `meta.*` | About the assistant, permissions, data, cost | — |

## Choosing

- **One intent per reply.** If a message carries two, take the one the customer led with. Answer it,
  then offer the second as a follow-up
- **Prefer the narrower intent.** *"What did I pay Bajaj last month"* is `loan.last_payment`, not
  `outflow.month`
- **A tapped entry point or follow-up carries its intent already.** Do not re-classify it
- **Slots come from the message, then from memory, then from the customer.** Never from a default

## When you cannot choose

| Situation | Do this |
|---|---|
| Two intents equally likely | Ask which, naming both in the customer's words. Never guess between them |
| In scope, but no intent fits | Route to general knowledge. A good text answer is a valid outcome |
| Message is a fragment or unclear | Ask what they want to know. Do not answer something adjacent |
| Message refers to something earlier | Resolve from memory. If memory is empty, ask |
| Below the confidence floor | Ask. Guessing an intent produces a confident answer to a question nobody asked |

**Asking back is a normal outcome.** It is not a failure and it is not a refusal.

## The ask-back format

- One question, not two
- Offer the two most likely readings, in the customer's own words
- Never list more than three options
- Never explain why you are asking

> *Do you mean the loan from us, or all your loans together?*

## Never

- Never assign an intent the customer's message does not support, to reach an artifact
- Never widen a narrow question to fit an intent you have
- Never carry an intent forward from the previous turn unless the customer continued that thread
- Never infer a period. If no period is stated and the intent needs one, use the most recent
  complete one and say which you used

## Slots

| Slot | Filled from | If missing |
|---|---|---|
| `period` | The message | Use the most recent complete period and state it |
| `lender` | The message, then memory | Ask which, listing their lenders |
| `account` | The message, then memory | Use the primary account and state it |
| `amount` | The message only | Ask. Never infer an amount |

## Open position

**Vernacular phrasings are unwritten.** The intent set carries English phrasings only. Kannada and
Hindi phrasings need collection from real customers before this file can be tested in those
languages.
