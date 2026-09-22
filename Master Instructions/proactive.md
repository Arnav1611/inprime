# proactive.md

Everything the assistant says without being asked. Two kinds: what greets them when they open the
app, and what reaches them when it is closed.

The normal chain is reactive. This file is the only place the assistant speaks first.

## What is preloaded on open

The home screen is the chat. It carries **one thing**, chosen by the time of day and what is
happening.

| When they open | Show |
|---|---|
| Morning | Yesterday's takings |
| Evening | Today's takings so far |
| EMI due within three days | The EMI, instead of income |
| Anything overdue | The overdue, ahead of everything else |
| Nothing notable | The most recent complete period, and nothing else |

**One item, never a stack.** Followed by two or three nudges. If nothing qualifies, show the income
figure and the nudges — never an empty screen, never a tour.

## What is pushed when the app is closed

Only these. Nothing else earns an interruption.

| Trigger | Urgency |
|---|---|
| Something is overdue | Immediate |
| A loan appears on the bureau the customer did not expect | Immediate |
| An EMI falls due in three days, where auto-pay is off | Timed |
| A payment they made is now recorded | Next digest |
| A loan closed | Next digest |
| A reminder they asked for | At the time they set |
| Their score refreshed and moved | Next digest |

## Rules

- **One push at a time.** If two qualify, send the more serious and hold the other
- **At most one immediate push a day**, and at most three pushes a week in total
- **Nothing before 8am or after 8pm.** A money notification at night reads as a threat
- **Nothing on the day an EMI bounced.** They already know. Give it a day
- **Every push carries when it was detected.** Bureau data lags up to 45 days, and a customer who
  cleared something last week must not think we missed it
- **A push opens the thread at that message**, with follow-ups ready. Never a dead-end screen

## Persistent items

Some things stay until resolved rather than firing once:

- An overdue, while it is open
- A bureau record the customer has disputed
- A connector that failed during a journey they started

These sit at the top of the home chat, one at a time, most serious first. They are dismissible only
by being resolved — not by being swiped away.

## What never triggers a push

- A good month, a best day, a milestone, a streak
- Anything phrased as encouragement
- A product we offer, or an eligibility change
- A feature we have added
- Anything the customer could have asked and did not
- Anything that is true every month

**If it would not change what they do today, it is not a push.**

## Tone

The same rules as everywhere else, applied harder. A push arrives uninvited, so it earns less
patience.

- State what happened, in one line
- Say what it means for them, in one line
- Offer one thing to do
- Never celebrate, never warn, never create urgency a date has not created

## Frequency is a product decision, not a growth lever

A customer who mutes notifications is lost for every genuine alert afterwards, including the ones
that would have saved them money. **Under-sending is the safer failure.**

## Open position

**None of this is built.** Nothing currently watches for a data change. Until a watcher exists,
every alert in the catalogue is unreachable and the reminders surface promises something the
product cannot do.
