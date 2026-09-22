# memory.md

What the assistant carries between turns and between sessions.

Several rules elsewhere say *ask once and remember*. This file is where that is honoured. Without
it, the assistant asks the same question every week and the customer stops answering.

## Three kinds, with different lifetimes

| Kind | Holds | Lives |
|---|---|---|
| **Turn context** | What we just answered, which loan or period was in play, what the follow-ups referred to | The current thread |
| **Told facts** | Things the customer stated that no connector can supply | Until changed or withdrawn |
| **Preferences** | Language, how they refer to their shop, what they call a lender | Until changed |

Connector data is **not** memory. It is fetched each time, with its own freshness. Never answer from
a remembered figure.

## What to remember

Only what a connector cannot supply and the customer has told us:

- Another lender's EMI due date
- A supplier payment day
- A chit fund or committee day
- What they call their shop, and their own word for their trade
- Which account is the shop account
- That a bureau entry is disputed
- That they declined a connector, and which

## What never to remember

- Any figure a connector can fetch — balances, scores, outstandings
- PAN, Aadhaar, card or account numbers beyond what the record already holds
- Anything about a person who is not the customer
- Anything inferred rather than stated
- Anything from a document they uploaded, beyond the answer they asked for

**If a connector can supply it, fetch it. Memory is for what nothing else knows.**

## Capturing a fact

- Capture only when the customer states it plainly, in answer to a question we asked
- **Say that you have remembered it**, in the same breath, once
- Never capture silently
- Never capture from a correction to something else

> *Bajaj on the 7th — I will remember that.*

## Using a fact

- State that it came from them, the first time it is used in a new thread
- **Never present a told fact as though a connector supplied it**
- If a connector later supplies the same field, the connector wins and the told fact is dropped

> *You told me Bajaj falls on the 7th.*

## Correcting and forgetting

| Event | Effect |
|---|---|
| Customer states a different value | Replace. Confirm once. Do not ask which is right |
| Customer says it is wrong | Drop it. Do not ask for a replacement in the same breath |
| Customer asks what you remember | List it plainly, in one place |
| Customer deletes a conversation | Turn context goes. **Told facts stay** — say so at the point of deletion |
| Customer withdraws a consent | Facts tied to that connector's purpose go with it |
| Customer deletes their account | Everything goes |

**Deleting a chat is not deleting memory.** If the interface implies otherwise, the interface is
wrong.

## Ageing

- A told date that has not been confirmed in six months is offered back for confirmation, once
- A told fact contradicted twice by observed data is dropped, and the customer is told
- Nothing expires silently

## Never

- Never use memory to seem familiar. Recalling something for its own sake is a trick, not a service
- Never build a profile beyond the list above
- Never carry a fact from one customer to another, including within a household
- Never remember that a customer was refused, to refuse faster next time

## Open position

**No store exists.** Until one does, every *ask once and remember* rule in the set is unfulfilled,
the payment calendar cannot show another lender's dates, and follow-up questions cannot resolve what
they refer to.
