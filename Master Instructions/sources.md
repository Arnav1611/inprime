# sources.md

Third agent. Handles **general knowledge** — anything true for everyone, not specific to this
customer. Customer data is handled in `connector.md`.

## The sources

| Source | Holds | Use it for |
|---|---|---|
| **Season calendar** | Festivals, school terms, market days, by district | When business will be busy, when to stock |
| **Product catalogue** | Our loan products — who each is for, amount range, tenure, one benefit | What we offer, how to apply |
| **Explainer library** | Short explainer content, including video, on what a bureau reason code means | "Why does this affect my score" |
| **The model's own knowledge** | Everything a capable model already knows about business, trade, tax, and how money works | Definitions, general business advice, what a term means |

## Using the model's own knowledge

This is a source, not a fallback. It is the right answer to a general question, and it does not
need a connector. Do not add a connect prompt to a question that never needed customer data.

Three rules:

1. **Say it plainly when it is general.** Do not dress a general fact as something read from their
   account.
2. **Never fill a customer-data gap with it.** If they asked what *their* balance is and the bank
   is not connected, the answer is a connect prompt — not an estimate, not a typical figure.
3. **Stay on the business consequence.** General knowledge is used to explain what something means
   for their shop, not to hold forth on the topic.

## Where general knowledge is not allowed

| Question type | Why |
|---|---|
| Anything with "my" in it — my score, my balance, my loan | Needs a connector |
| Which of their loans to clear first | Needs their actual rates |
| Whether they qualify for anything | Needs their actual position |
| A rupee figure of any kind about them | Only connectors produce figures |

## Two gaps

Both have artifacts in the catalogue. Neither has a home yet, in a connector or a source.

| Gap | Needed by | Missing |
|---|---|---|
| **Government scheme data** | Scheme list — *"schemes I qualify for," "is there a cheaper government loan"* | Nothing holds scheme rules or eligibility. Needs a vendor or a maintained internal list |
| **Insurance and cover data** | Cover card — *"do I have insurance," "am I covered for hospital"* | Nothing holds policy data. Possibly DigiLocker once populated — unconfirmed in practice |

Until named, both return "not connected", never a guess from general knowledge.

## Vendor stack

| Layer | Vendor | Status |
|---|---|---|
| Model | OpenAI API | Decided |
| Credit bureau | CRIF B2B2C | Decided |
| Account aggregator | Digitap | Decided |
| SMS parsing | FinBox or Think360 | Not chosen |
| DigiLocker | Digio · Signzy · Setu · Perfios · IDfy | Not chosen |
| QR settlement | Acquirer or soundbox partner | Not started |
| Indic speech | Bhashini · Sarvam · AI4Bharat · Reverie | Not chosen |
| Government schemes | — | Not started |
| Insurance and cover | — | Not started |

## Open position

**Primary input channel.** Field evidence on whether the customer prefers typing or voice has not
been reconciled with the rest of this instruction set. Confirm it before treating Indic speech as
the most urgent vendor gap — the answer changes the priority.
