# scenarios.md

Worked customer situations that define what "personalised" means. Each is a reference case for the
chain and a test case for the evaluation set. Loaded per case, never whole.

**Plan note.** Free and paid tiers are a proposal until the commercial model is decided:
ETI customers with an active loan get everything free; others get a monthly free allowance of
analytical questions (size to set), with a paid tier for more. Home preload, alerts, reminders,
connectors, grievance, fraud help and talking to a person never count against the allowance.

---

## S1 · Nothing connected

| Field | Value |
|---|---|
| Customer situation | New. Kirana shop. Just finished onboarding |
| Language/script | Kannada, Kannada script |
| Known facts and sources | Name, occupation, shop name — onboarding |
| Connected / declined / unavailable | None connected. Nothing declined |
| Plan | Free, allowance unused |
| Recent conversation or action | None |

- **On open:** greeting only. No banner, no card, no numbers
- **Suggested questions:** What is my credit score? · How did my shop do this month? · Is this loan SMS real?
- **Customer asks:** "What is my credit score?"
- **Answer and card:** one line — "I can find it, but I need your permission first." Card: credit bureau connect sheet — what is read, one-time permission, Yes / Not now
- **Follow-ups:** Why do you need my PAN? · Does checking lower my score?
- **Must not:** estimate a score · show any figure · ask for PAN before consent
- **If missing / fails:** Not now → explain what a score is in general, no card; do not re-ask in this chat
- **Why useful:** first answer in under a minute; the customer learns exactly what connecting unlocks

---

## S2 · EMI approaching

| Field | Value |
|---|---|
| Customer situation | InPrime customer. EMI ₹12,450 due in 3 days. Auto-pay on |
| Language/script | Hindi, Devanagari |
| Known facts and sources | EMI, due date, mandate — InPrime records, today 07:10 · balance ₹18,240 — Account Aggregator, yesterday |
| Connected / declined / unavailable | InPrime, bureau, Account Aggregator connected. SMS declined |
| Plan | Free (ETI) |
| Recent conversation or action | Asked about income last week |

- **On open:** no banner (auto-pay on). Priority card: Next EMI — ₹12,450, 5 September, "Auto-pay is on. Nothing for you to do"
- **Suggested questions:** Will my balance cover it? · How did my shop do this month?
- **Customer asks:** "Will my balance cover it?"
- **Answer and card:** "Yes — ₹18,240 was in your Canara account yesterday, more than the ₹12,450 EMI." Card: Balance, with "as of" time
- **Follow-ups:** What else is due this month? · Remind me a day before
- **Must not:** "don't worry" · promise the debit will succeed · figures the model wrote
- **If missing / fails:** balance older than 2 days → say its date and that it may have changed · mandate status unknown → say so, offer Remind me · auto-pay off → tier 2 banner "EMI due Friday" and EMI due card with Remind me
- **Why useful:** the one worry of the week answered before it becomes a bounce

---

## S3 · Overdue

| Field | Value |
|---|---|
| Customer situation | Two loans overdue: InPrime gold loan ₹8,730, 12 days late · Bajaj ₹12,450 reported overdue |
| Language/script | English with Hindi words, Latin script |
| Known facts and sources | InPrime overdue — InPrime records, today · Bajaj overdue — bureau, pulled 24 July |
| Connected / declined / unavailable | InPrime, bureau connected. Account Aggregator not connected |
| Plan | Free (ETI) |
| Recent conversation or action | Ignored an EMI reminder 12 days ago |

- **On open:** tier 1 banner — "2 loans overdue · ₹21,180 · oldest is 12 days late". Below: score card if the score moved
- **Suggested questions:** What do I pay first? · What does this do to my score?
- **Customer asks:** taps the banner
- **Answer and card:** "Two payments are late. Ours is ₹8,730, 12 days late. Bajaj shows ₹12,450 overdue on your report from 24 July." Card: Overdue — InPrime amount, days late, charges, Pay now · Bajaj row with amount and report date, no pay button
- **Follow-ups:** Pay the InPrime amount · I already paid Bajaj · Talk to a person
- **Must not:** threaten · mention legal action or recovery · say the Bajaj loan is still unpaid today · rank which to pay first before legal sign-off
- **If missing / fails:** payment fails → no double charge, retry · "I already paid Bajaj" → report may take up to 45 days to update, remember what they told us · hardship mentioned → options, then callback
- **Why useful:** one clear view of what is late and a single action, in a calm tone

---

## S4 · Disputed bureau entry

| Field | Value |
|---|---|
| Customer situation | Bureau shows a new ₹50,000 personal loan the customer says they never took |
| Language/script | Kannada, Kannada script |
| Known facts and sources | New account, lender, opened date, amount — bureau, pulled 2 August |
| Connected / declined / unavailable | Bureau connected. SMS connected |
| Plan | Free, allowance unused |
| Recent conversation or action | Saw "New loan in your name" card on home |

- **On open:** priority card — New loan detected: lender, amount, date found
- **Suggested questions:** This is not mine · Who checked my credit?
- **Customer asks:** "I never took this loan"
- **Answer and card:** "Let's sort this out. The report shows this loan opened on 14 July. I cannot confirm fraud, but you have the right to dispute it." Card: New loan detected, with "I did not take this"
- **Follow-ups:** How do I raise a dispute? · Talk to a person · Will this affect my score?
- **Must not:** call it fraud or not fraud · promise removal · give a point figure for the score effect · suggest disputing a loan the customer did take
- **If missing / fails:** no in-app dispute path yet → raise a request and offer a person now · lender unknown on the report → say so
- **Why useful:** a frightening discovery gets a calm, correct next step instead of silence

---

## S5 · Incomplete bank history

| Field | Value |
|---|---|
| Customer situation | Two bank accounts. Only one linked. 22 days of data |
| Language/script | Hindi, Devanagari |
| Known facts and sources | Credits and debits 9–30 September — Account Aggregator, one account · second account is a cooperative bank not on Account Aggregator |
| Connected / declined / unavailable | Account Aggregator connected (partial). SMS declined. Second bank unavailable |
| Plan | Free, 3 of allowance left |
| Recent conversation or action | Linked bank 22 days ago |

- **On open:** priority card — income so far this month, labelled "1 of 2 accounts"
- **Suggested questions:** How did my shop do this month? · Add my other bank
- **Customer asks:** "How did my shop do this month?"
- **Answer and card:** "From 9 to 30 September, ₹64,300 came into your SBI account. Your other bank and cash are not included." Card: Monthly report card with period and "1 of 2 accounts" label, no month-on-month change
- **Follow-ups:** Upload my other bank statement · Where did my money go?
- **Must not:** extrapolate to a full month · compare with last month · call it a good or bad month
- **If missing / fails:** under 7 days of data → text only with the dates covered · Account Aggregator down → last data with its date
- **Why useful:** a real number the customer can trust, with the gaps stated plainly

---

## S6 · Declined permission

| Field | Value |
|---|---|
| Customer situation | Declined Account Aggregator and SMS earlier in this chat. Bureau connected |
| Language/script | English, Latin script |
| Known facts and sources | Three loans, EMIs — bureau, pulled 24 July · InPrime EMI — InPrime records |
| Connected / declined / unavailable | Bureau, InPrime connected. Account Aggregator and SMS declined |
| Plan | Free, allowance unused |
| Recent conversation or action | Tapped Not now on the bank sheet five minutes ago |

- **On open:** unchanged — bureau-based card if relevant
- **Suggested questions:** How much am I paying every month? · What is an Account Aggregator?
- **Customer asks:** "Where did my money go this month?"
- **Answer and card:** "I can't see your spending without your bank. What I can see: your loans take ₹15,180 a month." Card: Every loan in your name. No connect sheet
- **Follow-ups:** Which loan costs the most? · How do I connect my bank later?
- **Must not:** show the connect sheet again in this chat · estimate spending · make the customer feel wrong for declining
- **If missing / fails:** asks again later in a new chat → connect sheet may be offered once
- **Why useful:** declining is not a dead end; the customer still gets something true and useful

---

## S7 · Free allowance exhausted

| Field | Value |
|---|---|
| Customer situation | Not an InPrime customer. Used this month's free analytical questions |
| Language/script | Kannada, Kannada script |
| Known facts and sources | Score, loans — bureau · income — Account Aggregator |
| Connected / declined / unavailable | Bureau, Account Aggregator connected |
| Plan | Free, allowance used; resets 1 November |
| Recent conversation or action | Asked six detailed questions this week |

- **On open:** normal home — banner, priority card and alerts still show (free)
- **Suggested questions:** Remind me before my EMI · Check my score
- **Customer asks:** "Compare my three loans for me"
- **Answer and card:** "You've used this month's free questions; they reset on 1 November. Your alerts, reminders and score stay free." Card: plan card — what is free, what paid adds, price, reset date
- **Follow-ups:** Check my score · Set a reminder · Tell me about the paid plan
- **Must not:** block fraud help, overdue help, grievance or talking to a person · use urgency ("offer ends today") · answer partly and then cut off
- **If missing / fails:** payment for the paid plan fails → nothing charged, retry · allowance count unavailable → allow the question
- **Why useful:** the limit is clear and fair, and what matters for safety never stops working
