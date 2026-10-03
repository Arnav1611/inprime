# card-contracts.md

One small contract per launch card. Code reads this to fill a card; the model reads it to decide
whether a card fits. Looked up per card, never loaded whole.

**Plan column** follows the proposal in `scenarios.md`: *Free* = never counts · *Allowance* = counts
against the free allowance for non-ETI customers · ETI customers with an active loan get all free.

**Figma frames** marked *(ID to confirm)* exist in the file but have no frame code yet.

---

## C-01 · Next EMI

| | |
|---|---|
| Answers | When is my next EMI? · Is auto-pay on? |
| Fields · sources | Next instalment amount, due date, mandate status, bank and last 4 digits — InPrime records |
| Calculation | Next unpaid instalment in the schedule · "in N days" = due date − today (IST) |
| Appropriate | InPrime loan active; EMI due within 7 days, or asked |
| Not appropriate | No InPrime loan · EMI already paid this cycle · overdue exists (use C-13) |
| Partial / stale | Mandate status unknown → hide the auto-pay line, say "check auto-pay" · records older than 24h → show read time |
| Actions · follow-ups | Remind me · Will my balance cover it? · How did my shop do this month? |
| Plan | Free |
| Figma | OB-W1 · O-07 Home — composer + deck |

## C-02 · EMI due, not covered

| | |
|---|---|
| Answers | Is my EMI covered? |
| Fields · sources | Amount, due date, auto-pay off — InPrime records |
| Calculation | Due within 3 days and mandate inactive |
| Appropriate | Auto-pay off or cancelled, EMI due within 3 days |
| Not appropriate | Auto-pay on (use C-01) · already paid |
| Partial / stale | Mandate status unknown → treat as not covered, say so |
| Actions · follow-ups | Remind me · Pay now · Will my balance cover it? |
| Plan | Free |
| Figma | O-07 Home — EMI due variant · BN-05 |

## C-03 · Alert banner

| | |
|---|---|
| Answers | Is anything wrong? (unasked) |
| Fields · sources | Overdues, due dates, mandate status — InPrime records · overdues — bureau |
| Calculation | Tier 1 money missed › tier 2 due and not covered › tier 3 payment blocked · same tier → count and total; meta line names the oldest |
| Appropriate | Any tier 1–3 item |
| Not appropriate | Score moves, offers, festival notes (tier 4 — never a banner) · nothing wrong |
| Partial / stale | Bureau overdue shows its report date · cleared today → green for the session |
| Actions · follow-ups | Tap opens the thread with the answer and payment action |
| Plan | Free |
| Figma | BN-01 to BN-08 |

## C-04 · Connect sheet

| | |
|---|---|
| Answers | Any question that needs data not yet connected |
| Fields · sources | Connector name, why it is needed, what it reads, vendor line |
| Calculation | None |
| Appropriate | Question needs a connector that is not connected and not declined in this chat |
| Not appropriate | Declined earlier in this chat · during onboarding · general question needing no customer data |
| Partial / stale | Vendor down → "try again shortly", no sheet |
| Actions · follow-ups | Connect · Not now (equal weight) · What is an Account Aggregator? · How do I stop it later? |
| Plan | Free |
| Figma | S-01 My shop — connect your account · permission sheets: location, SMS, alerts, credit score, bank statement *(ID to confirm)* |

## C-05 · Monthly report card

| | |
|---|---|
| Answers | How did my shop do this month? |
| Fields · sources | Credits, debits, counterparty, category — Account Aggregator · credit alerts — SMS |
| Calculation | Money in = business credits (QR, UPI) in the month to date · money out = debits excluding own-account transfers · stayed = in − out · change vs last month only if both months are complete · SMS and AA duplicates counted once |
| Appropriate | At least 7 days of bank or SMS data |
| Not appropriate | Under 7 days of data · no bank or SMS connected (use C-04) |
| Partial / stale | Some accounts missing → label "1 of 2 accounts" · partial month → show dates covered, no comparison |
| Actions · follow-ups | Share (rounded amounts) · Send monthly · When was I busiest? · Where did my money go? |
| Plan | Allowance |
| Figma | S-02 My shop — report card |

## C-06 · Best day and best week

| | |
|---|---|
| Answers | When was I busiest? |
| Fields · sources | Daily business credits — Account Aggregator, SMS |
| Calculation | Best day = day with highest money in · best week = Monday–Sunday week with highest money in · sales by week W1–W4 |
| Appropriate | At least 14 days of data |
| Not appropriate | Under 14 days |
| Partial / stale | Show only complete weeks |
| Actions · follow-ups | Why was that week so strong? · Where did my money go? |
| Plan | Allowance |
| Figma | S-03 My shop — best days |

## C-07 · Where my money went

| | |
|---|---|
| Answers | Where did my money go? |
| Fields · sources | Debits with category — Account Aggregator |
| Calculation | Sum per category: stock and suppliers · loan EMIs · rent and electricity · everything else · share = category ÷ money out |
| Appropriate | Bank connected, at least 7 days of debits |
| Not appropriate | SMS only (debits incomplete) |
| Partial / stale | Uncategorised debits go to "everything else", never guessed |
| Actions · follow-ups | How does this compare to last month? · What should I watch next month? |
| Plan | Allowance |
| Figma | S-04 My shop — where your money went |

## C-08 · Balance

| | |
|---|---|
| Answers | What's my balance? · Will my balance cover my EMI? |
| Fields · sources | Balance per linked account, fetch time — Account Aggregator |
| Calculation | Latest balance per account; no totals across banks unless asked |
| Appropriate | Account Aggregator connected |
| Not appropriate | Not connected (use C-04) |
| Partial / stale | Older than 2 days → show date and "may have changed" · pull limit reached → last balance |
| Actions · follow-ups | Show recent transactions · What charges did the bank take? |
| Plan | Free |
| Figma | Artifacts Library · Your bank account — balance *(ID to confirm)* |

## C-09 · Bank charges

| | |
|---|---|
| Answers | Why was money deducted? · What charges did the bank take? |
| Fields · sources | Debits categorised as bank charges — Account Aggregator, SMS |
| Calculation | Each charge with plain name · total for the period |
| Appropriate | At least one charge in the period |
| Not appropriate | No charges → text "No bank charges this month" |
| Partial / stale | Charge type unknown → show bank's description as is |
| Actions · follow-ups | How do I avoid this charge? · Show my full statement |
| Plan | Allowance |
| Figma | Artifacts Library · Bank charges *(ID to confirm)* |

## C-10 · Full bank statement

| | |
|---|---|
| Answers | Show my full statement |
| Fields · sources | All transactions for chosen period — Account Aggregator |
| Calculation | None |
| Appropriate | Asked directly |
| Not appropriate | Never as the first answer to a narrower question |
| Partial / stale | Shows the date range actually available |
| Actions · follow-ups | Download PDF · back to chat |
| Plan | Free |
| Figma | Artifacts Library · The full bank statement — full view *(ID to confirm)* |

## C-11 · Every loan in your name

| | |
|---|---|
| Answers | How much am I paying every month, in total? · How many loans do I have? |
| Fields · sources | Lender, type, tenure, status — bureau · EMI — InPrime records for ours, bureau EMI field for others, else what the customer told us |
| Calculation | Total monthly EMI = sum of EMIs of active loans · a loan with no known EMI is listed but excluded from the total, and named |
| Appropriate | Bureau connected, at least one active loan |
| Not appropriate | No active loans → text |
| Partial / stale | Show bureau report date · customer-told EMIs labelled "you told us" |
| Actions · follow-ups | Which one should I clear first? (after legal sign-off) · Is any of them overcharging me? |
| Plan | Free |
| Figma | L-02 My loan — all three loans |

## C-12 · Loan progress

| | |
|---|---|
| Answers | How much have I paid? · How much is left? |
| Fields · sources | Schedule, payments — InPrime records |
| Calculation | Paid so far = sum of instalments paid · left to pay = sum of scheduled instalments remaining · "N of M paid" |
| Appropriate | InPrime loan active |
| Not appropriate | Other lenders' loans (bureau has no schedule) |
| Partial / stale | Records older than 24h → read time |
| Actions · follow-ups | What has this loan cost me so far? · What if I close it early? |
| Plan | Free |
| Figma | L-01 My loan — living thread |

## C-13 · Overdue and pay

| | |
|---|---|
| Answers | What do I owe now? · Pay my overdue |
| Fields · sources | Overdue amount, days late, charges — InPrime records · other lenders' overdue — bureau |
| Calculation | Overdue = unpaid due instalments + charges · days late = today − oldest unpaid due date |
| Appropriate | Any overdue |
| Not appropriate | None overdue |
| Partial / stale | Bureau overdue shows report date; "if you've paid, it can take up to 45 days to update" |
| Actions · follow-ups | Pay now (InPrime only, amount confirmed first) · I already paid · Talk to a person |
| Plan | Free |
| Figma | Artifacts Library · Your InPrime loan — overdue *(ID to confirm)* |

## C-14 · Score today

| | |
|---|---|
| Answers | What is my credit score? |
| Fields · sources | Score, band, report date — bureau (CRIF) |
| Calculation | None — shown as reported |
| Appropriate | Bureau connected and a score exists |
| Not appropriate | No credit history (use C-17) |
| Partial / stale | Always shows "updated" date · bureau not responding → retry, message when ready |
| Actions · follow-ups | Why is it not higher? · Why did it drop? · Show my loans and cards |
| Plan | Free (monthly refresh) |
| Figma | Credit score flow — score reveal *(ID to confirm)* |

## C-15 · Score change

| | |
|---|---|
| Answers | Why did my score drop? · What moved it? |
| Fields · sources | Current and previous score, reason codes, enquiries — bureau |
| Calculation | Change = current − previous pull · reasons in the bureau's ranked order, biggest first |
| Appropriate | Two pulls exist and the score changed |
| Not appropriate | First pull · no change |
| Partial / stale | No point figure per reason before compliance review — reasons and dates only |
| Actions · follow-ups | When will my score go back up? · What can I do now? · Explainer video (enquiries or payments) |
| Plan | Free |
| Figma | Credit score flow — "It dropped 14 points" *(ID to confirm)* |

## C-16 · The way back

| | |
|---|---|
| Answers | When will my score go back up? · How do I improve my score? |
| Fields · sources | Reason codes, enquiry dates, overdue status — bureau |
| Calculation | Recovery date = when the negative item stops counting, per bureau rules · projected score only after compliance review; until then date and direction |
| Appropriate | Score below its last high, or improvement asked |
| Not appropriate | No bureau data |
| Partial / stale | Always labelled "a projection, not a promise" |
| Actions · follow-ups | Remind me on the date · What if I apply anyway? · How do I get past 800? |
| Plan | Free |
| Figma | CS-04b Score — when it goes back up |

## C-17 · No credit history

| | |
|---|---|
| Answers | What is my credit score? (when none exists) |
| Fields · sources | Bureau "no record" response |
| Calculation | None |
| Appropriate | Bureau returns no record for the PAN |
| Not appropriate | PAN or name mismatch (edit PAN instead) |
| Partial / stale | — |
| Actions · follow-ups | How do I build a score? · I will check every month and tell you the day it appears |
| Plan | Free |
| Figma | Credit score flow — new to credit *(ID to confirm)* |

## C-18 · Reminders list

| | |
|---|---|
| Answers | What reminders do I have? · Remind me before my EMI |
| Fields · sources | Reminders store · due dates — InPrime records, customer-told dates |
| Calculation | Sorted by date |
| Appropriate | Asked, or after a reminder is set |
| Not appropriate | No reminders → text with "Remind me about something" |
| Partial / stale | Date passed → ask for a new date |
| Actions · follow-ups | Remind me about something else · Stop one of these |
| Plan | Free |
| Figma | D-02 Reminders |

## C-19 · EMI calculator

| | |
|---|---|
| Answers | What will my EMI be? |
| Fields · sources | Amount, rate, tenure — customer input or product catalogue |
| Calculation | EMI = P·r·(1+r)ⁿ ÷ ((1+r)ⁿ − 1), r = monthly rate, n = months · total interest = EMI × n − P · runs in the app, instant |
| Appropriate | EMI or affordability asked |
| Not appropriate | As a nudge to borrow |
| Partial / stale | Rate unknown → use product rate, labelled |
| Actions · follow-ups | Which InPrime loan fits this? · What if I pay it off early? |
| Plan | Free |
| Figma | Artifacts Library · EMI calculator *(ID to confirm)* |

## C-20 · InPrime products and eligibility

| | |
|---|---|
| Answers | What loans does InPrime give? · How much can I get? |
| Fields · sources | Product catalogue · bureau and income for indicative eligibility |
| Calculation | Eligibility from credit policy rules — labelled indicative |
| Appropriate | Asked about InPrime loans |
| Not appropriate | As an answer to a money worry · during overdue |
| Partial / stale | Nothing connected → product info only, no eligibility |
| Actions · follow-ups | Apply (redirects to website, app source tracked) · Compare products · What will my EMI be? |
| Plan | Free |
| Figma | Artifacts Library · InPrime products · Choosing a product *(ID to confirm)* |

## C-21 · Plan card

| | |
|---|---|
| Answers | Why can't I ask more? (allowance used) |
| Fields · sources | Allowance used, reset date, plan price |
| Calculation | Reset date = first day of next month |
| Appropriate | Free allowance used and an allowance question asked |
| Not appropriate | ETI customers · fraud, overdue, grievance, talk to a person |
| Partial / stale | Count unavailable → allow the question |
| Actions · follow-ups | Tell me about the paid plan · Check my score · Set a reminder |
| Plan | Free |
| Figma | Not designed |

---

## Held from launch

| Card | Why held | Figma |
|---|---|---|
| Which loan to clear first | Legal position on comparative advice | L-03 My loan — which to clear first |
| Document check | Uncertain-verdict state not designed | Upload flow *(ID to confirm)* |
| Bureau alerts | Change watcher not built | Artifacts Library · What the bureau reported |
| What to watch next month | Needs 12 months of data | S-05 My shop — September ahead |
| Payment costs (MDR) | Needs transaction-level QR data | Not designed |
