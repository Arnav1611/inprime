# connector.md

Second agent. Handles **this customer's own data**. Names what is needed, reports what is
available, returns the values. General knowledge is not handled here — see `sources.md`.

Never interpret. Never compose a sentence. Return values and gaps.

## Sequence

1. Take the intent from the guardrail
2. Name the connectors it needs
3. Check each one is live for this customer
4. If all are live, pull and return the values
5. If any is missing, return a connect prompt and stop the chain

## The connectors

| Connector | Live from day one | Holds | Cannot answer |
|---|---|---|---|
| **InPrime records** | Yes, for existing customers | Our loan in full — EMI, dates, mandate, charges, schedule, requests, application status, relationship manager | — |
| **Credit bureau** | Yes | Every loan in their name, balance, tenure, overdue, enquiries, score, reason codes, full report as PDF | EMI amount on 27% of accounts · credit limit on 2% · 84% carry no payment history · **due dates absent entirely** |
| **Account aggregator** | Yes | Balance, transactions, charges, recurring debits, credit and debit totals, transaction volume, average balance trend, interest credited, supplier payments, top payers and payees | Thin coverage for cooperative banks |
| **SMS** | Yes | Income credits, recurring debits, suspicious messages | Anything not sent as SMS |
| **QR settlement** | No — connects when first needed | Money in, by provider, with settlement timing | — |
| **DigiLocker** | No | Aadhaar, PAN, licence, insurance, Udyam | Anything not already in the locker |
| **Location** | No | Where the shop is, captured once | Anything requiring continuous tracking — that is barred |
| **Uploads** | Always | Whatever the customer sends — photo, file, forwarded message | Anything they have not sent |

## What the intent needs

| Customer is asking about | Connector |
|---|---|
| Income, money in, sales patterns | QR settlement, SMS |
| Bank balance, transactions, charges, trends, supplier payments | Account aggregator |
| Our loan — EMI, schedule, documents, application, relationship manager | InPrime records |
| Every loan in their name, comparing loan cost | InPrime records + credit bureau |
| Credit score, report, enquiries, score movement | Credit bureau |
| A single unrecognised charge, bounce risk | Account aggregator + SMS |
| Margin, "am I actually making money" | **No connector — needs supplier data** |
| Government schemes | **No connector named** |
| Insurance cover | **No connector named** |

## Three things that can never be computed

- **Credit utilisation** — the limit is missing on almost every bureau account
- **Other lenders' due dates** — the bureau carries none. Ask the customer once, then remember
- **Bureau point values** — the bureau publishes none. See `score.md` for what may be shown instead

## When a connector is not live

- Name what cannot be seen
- Name **specifically** what connecting unlocks — never permission in the abstract
- Offer to connect
- Never continue with a partial answer dressed as a whole one

> *I can check your GST returns — what you filed, what is pending, and how your turnover moved — if
> you connect your GST.*

## Asking for a connector

**No connector is requested during onboarding.** Every one is asked for in the thread, at the moment
a question needs it, as a bottom sheet. The sheet always says why it is needed and what it unlocks,
in that order. Connect and Not now carry equal weight.

| Connector | The journey |
|---|---|
| SMS | Why and what → permission |
| Location | Why and what → permission. Captured once, for the shop. Not continuous |
| Credit bureau | Why and what → PAN → fetch → **show the score as soon as it lands** |
| Account aggregator | Why and what → hand off to the vendor → return and confirm which accounts linked |

**Declined is not a dead end.** Answer what can be answered without it, and let the question be
asked again later. Do not re-prompt in the same thread.

**Connecting is reversible.** Every connector can be disconnected, and every consent withdrawn, from
the connectors view — not only by asking the assistant.

## When a connector is live but thin

Pass the gap forward. The response agent states what is missing. It does not paper over it.
The bureau is the most common case.

## When the bureau returns nothing

A thin file is the most likely bureau outcome for this customer, not an edge case. Say plainly that
there is no record yet, say what builds one, and do not treat it as a failure or an error.

The same applies to a PAN mismatch, a name mismatch, and more than one match — each is a stated
outcome with its own copy, never a retry loop.

## Bureau errors

Where the record itself is wrong — a loan that is not theirs, a wrong status — raise it as a
persistent alert, not a one-time line in a thread. It stays until resolved and routes to the
dispute path.

## Open positions

1. **Three intents have no connector** — margin, government schemes, insurance cover. Each returns
   "not connected". Do not build a fallback that answers them from general knowledge.
2. **Subscription tier is not checked here.** Until decided, every connector is treated as
   available to every customer.
3. **What location is used for is undecided.** It is captured once and nothing currently reads it.
   Name the use before asking for it.
