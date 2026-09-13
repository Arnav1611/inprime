# artifact-picker.md

Part of the response agent. Picks one artifact, or none. The catalogue itself is `artifacts.md` —
look the artifact up there rather than holding the list in the prompt.

## Sequence

1. Take the intent and the values returned
2. Look up the artifact bound to that intent
3. Check every field that artifact needs is present
4. Return the artifact name, or none

## The rule that matters most

**An artifact is built for one use case and carries its own fixed labels.**

A general-purpose container filled with whichever number is to hand is the wrong answer, even when
the number is correct.

| | |
|---|---|
| **Wrong** | A big-number card showing ₹1,04,200, with a line underneath explaining what it is |
| **Right** | An income artifact whose own labels already say the month and that it came through QR. The number sits inside them |

If an artifact needs a sentence inside it to explain what it is showing, it is the wrong artifact.
The explanation belongs outside, in the text — see `story.md`.

## Picking

- One artifact. Two only where `artifacts.md` lists them as a pair. Never three
- **None is a common and correct answer**
- Never invent an artifact. Never merge two
- Never reuse an artifact from a neighbouring use case because it looks close enough
- Only the EMI calculator is interactive. Everything else is display-only

## Return none for

- How the product works, how it earns money, whether it is free
- Why a permission is needed, whether the data is safe
- Who or what the assistant is
- What a general term means — score, interest, GST
- Why an application was rejected
- Anything the guardrail passed through as borderline

A text answer with good follow-ups beats a weak artifact every time.

## Components are not artifacts

Pills, bars, callouts, status chips, buttons and the follow-up strip are shared patterns used
inside artifacts. **Never pick one directly** — that is how a general-purpose container gets back
in.

## Three shapes that break the normal flow

| Shape | How it differs |
|---|---|
| **Expandable sections** — the bank statement, and anything with parts | Asked for the balance, return the balance. Transactions, charges, and credits-and-debits each open on request, one at a time. Never return all of them at once |
| **Alerts** — a new loan appears, an overdue is detected, a payment is recorded, a loan closes | Not picked in answer to a question. Pushed when the data changes, carrying a detection time, because bureau data lags. These need their own trigger path |
| **Full-screen** — full bureau report, full bank statement, repayment schedule | Do not sit in the thread. Open full-screen and scrollable. The bureau report renders as its PDF |
