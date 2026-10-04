# card-contracts.md

One contract per card in the Artifacts Library (volume two), for the intelligent cards on landing, and for the new Day-0 products.
Code reads a contract to fill a card. The model reads it to decide whether a card fits the question.
Look up one contract at a time. Never load the whole file.

## How to read a contract

| Field | Meaning |
|---|---|
| Answers | The customer questions this card is the right answer for. |
| Fields and sources | The data the card needs, and where each piece comes from. |
| Calculation | Exactly how code works out every figure. The model never calculates or writes a figure. |
| Use when | Conditions that must all be true before this card is chosen. |
| Do not use when | Conditions that rule this card out. |
| Partial or stale data | What to do when some data is missing or old. |
| Actions | Buttons on the card itself. |
| Next nudges | The three quick-tap prompts shown above the chat box after this card. The Next-Nudge Engine generates them fresh each time; these are the defaults it starts from. |
| Plan | Every card is free on Day 0. |
| Status | Launch on Day 0, or the confirmed reason it is not on Day 0, or what is still to be confirmed. |
| Figma | The card's label on the Artifacts Board. |

## Terms used in every calculation

| Term | Meaning |
|---|---|
| Percentage change | Subtract the earlier amount from the current amount. Divide the result by the earlier amount. Multiply by 100. Round to one decimal place. If the earlier amount is zero, do not show a percentage. |
| Business credit | Money received from a customer of the shop: QR settlements (read from SMS on Day 0), UPI payments and card machine settlements. Not salary, refunds, loan disbursals or transfers from the customer's own accounts. |
| Own-account transfer | Money moved between two accounts that belong to the same customer. Never counted as money in or money out. |
| Complete period | A day, week or month that has fully ended. A week runs Monday to Sunday. |
| Same credit counted once | If a credit appears in both SMS and Account Aggregator with the same amount, date and reference, count it one time only. |
| Rounding | Show rupee amounts as whole rupees with Indian digit grouping, for example ₹1,04,200. On shared cards, round to the nearest hundred. |

## Day-0 decisions this file follows

| Decision | What it means for the cards |
|---|---|
| Monetisation of any kind is out of scope for Day 0. | Every card is free. There is no plan card and no usage allowance. |
| Answers are shaped to the question, with the cards that help it, or none. | An answer may show more than one card. Each card still answers one kind of question with fixed labels. |
| Three next nudges sit above the chat box, generated fresh after every answer. | Each contract lists three default next nudges. Whenever advice would be relevant, one nudge invites the user to ask for it. |
| Intelligent cards are the central cards shown when the user lands on the app. Day-0 scope: facts that are due or have changed. | The Day-0 intelligent cards are an upcoming or overdue EMI, the monthly report card, the most important bureau changes each month, and a reminder the user set. |
| Unprompted advice is out of scope for Day 0. | Intelligent cards state facts. Advice comes only when the user asks, and nudges invite them to ask. |
| The assistant recommends actions for the user's own money and business. It never strongly recommends another institution, and cites sources on industry comparisons. | Cards and answers may say what the user should do, for example clear an overdue. They never push the user towards a lender. |
| An InPrime loan comes up only when a loan makes real sense for the user, or the user asks. | Product and eligibility cards are never the answer to a question about something else. Applications redirect to the InPrime website with the app recorded as the source. |
| The bureau is refreshed once a month for every user who has connected it, and Bureau Alerts are replaced by the Monthly Bureau Update. | The four bureau change cards (15 to 18) ship on Day 0 inside the monthly update, most important change first. |
| Day-0 data sources: SMS (including QR settlement messages), credit bureau, Account Aggregator, InPrime loan records, festival calendar, general business knowledge. | Location, DigiLocker, GST and settlement data direct from payment providers are not on Day 0. |
| MDR questions and Document Check are answered from the model's general knowledge. Document Check also has its own dedicated option. | MDR is answered in text as general knowledge with a source. The actual charges a shop paid, from its own settlements, are not on Day 0. |
| RO details are shared only when the user asks, or the conversation calls for it. Change requests are raised as service requests. | The RO card is never shown unprompted. Any change to customer details goes through the service request card. |
| Shared versions hide amounts and personal details unless the user opts in, and carry the app identity and an install link. | Every share action on a card follows this rule. |
| Dark mode ships on Day 0. | Every card must render correctly in light and dark. |


## Design conflict marker

| Rule |
|---|
| "Design conflict" in the Figma row marks a place where the current design breaks a rule. Follow the rule, not the design, until the design is fixed. |

## A · Money in, money out

### 1a, 1b, 1c · Income card — yesterday, this week, this month

| Field | Details |
|---|---|
| Answers | What came in yesterday?<br>How is this week going?<br>How is the month going? |
| Fields and sources | Business credits with their date, from Account Aggregator<br>Business credits with their date, from SMS |
| Calculation | Money in: add up every business credit received in the period.<br>Yesterday: compare with the day before yesterday.<br>This week: compare with the full previous week.<br>This month: compare the month so far with the same number of days in the previous month.<br>Percentage change: subtract the earlier amount from the current amount, divide the result by the earlier amount, and multiply by 100.<br>If the same credit appears in both SMS and Account Aggregator, count it only once. |
| Use when | Bank or SMS is connected. |
| Do not use when | Nothing is connected. Show the connect sheet instead. |
| Partial or stale data | If the comparison period has no data, hide the comparison row and the percentage.<br>Always say that cash sales are not included.<br>If only one of the customer's bank accounts is linked, label the card with how many accounts are included. |
| Actions | None |
| Next nudges | Where did my money go?<br>When was I busiest?<br>Who paid me the most? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch inside the chat.<br>To confirm: whether income yesterday or today is also a Day-0 intelligent card on landing. The master document lists the Day-0 intelligent cards as an upcoming or overdue EMI, the monthly report card, the most important bureau changes each month, and a reminder the user set. |
| Figma | 1a · Income card - yesterday<br>1b · Income card - this week<br>1c · Income card - this month |

---

### 2 · Planned outflow

| Field | Details |
|---|---|
| Answers | What is going out this month?<br>What do I still have to pay?<br>Can I afford it this week? |
| Fields and sources | Recurring payees, their usual amount and expected date, from Account Aggregator<br>EMIs, from InPrime records and the credit bureau |
| Calculation | A payment is "planned" only if the same payee has been paid at least twice before at a regular interval.<br>Big number: add up only the planned payments that have not been paid yet this month.<br>Paid: add up the planned payments already debited this month.<br>This week toggle: add up only the unpaid planned payments due in the current week.<br>Heaviest week line: find the week with the largest total of unpaid planned payments and state that total. |
| Use when | At least two months of bank history are available. |
| Do not use when | Less than two months of bank history.<br>Only SMS is connected. |
| Partial or stale data | Never guess a payment that has not been seen at least twice. Say "only payments seen twice or more are included". |
| Actions | This week and this month switch |
| Next nudges | Will my balance cover it?<br>Remind me before the rent<br>Which supplier costs me most? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | 2 · Planned outflow |

---

### 3 · Top payers

| Field | Details |
|---|---|
| Answers | Who pays me the most?<br>Which customers matter?<br>Who stopped paying me? |
| Fields and sources | Credits grouped by the name of the person or business that paid, from Account Aggregator |
| Calculation | Group all credits in the period by payer name.<br>Sort payers by total amount, highest first.<br>Show the top four payers with their total and number of payments.<br>Add everyone else together into one line called "Everyone else".<br>Share line: add up the top four totals, divide by total money in, and multiply by 100. |
| Use when | At least ten credits in the period have a payer name. |
| Do not use when | Most credits have no payer name, for example only daily QR settlements. |
| Partial or stale data | Credits without a payer name go into "Everyone else". |
| Actions | None |
| Next nudges | Who stopped paying me?<br>Who do I pay the most?<br>Where does my money come from? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | 3 · Top payers |

---

### 4 · Top payees

| Field | Details |
|---|---|
| Answers | Who am I paying the most?<br>Where is my money going?<br>Which supplier costs me most? |
| Fields and sources | Debits grouped by the name of the person or business paid, from Account Aggregator |
| Calculation | Group all debits in the period by payee name.<br>Sort payees by total amount, highest first.<br>Show the top three or four payees with their total and number of payments.<br>Add everyone else together into one line called "Everyone else". |
| Use when | At least five debits in the period have a payee name. |
| Do not use when | Only SMS is connected. |
| Partial or stale data | Debits without a payee name go into "Everyone else". |
| Actions | None |
| Next nudges | Show my supplier payments<br>Where did my money go?<br>Who pays me the most? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | 4 · Top payees |

---

## B · Your bank account

### 5 · Balance card

| Field | Details |
|---|---|
| Answers | What is my balance?<br>How much is in the bank?<br>Can I pay for this today? |
| Fields and sources | Current balance and the time it was read, from Account Aggregator<br>Daily closing balances for this month, from Account Aggregator |
| Calculation | Balance today: the latest balance read from the bank.<br>Lowest this month: the smallest daily closing balance since the first of the month.<br>Highest this month: the largest daily closing balance since the first of the month. |
| Use when | Account Aggregator is connected. |
| Do not use when | Only SMS is connected. SMS does not give a reliable balance. |
| Partial or stale data | Always show the "as on" date and time.<br>If the balance is more than two days old, say it may have changed. |
| Actions | None |
| Next nudges | Show recent transactions<br>What charges did the bank take?<br>Will my balance cover my EMI? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | 5 · Balance card |

---

### 6 · Recent transactions

| Field | Details |
|---|---|
| Answers | What happened in my account?<br>Did that payment come in?<br>Show me my last transactions |
| Fields and sources | Transactions from the last seven days, from Account Aggregator<br>Transactions from the last seven days, from SMS |
| Calculation | Sort transactions newest first.<br>Show the six newest, then the "Show full statement" link. |
| Use when | There is at least one transaction in the last seven days. |
| Do not use when | No transactions in seven days. Answer in text instead. |
| Partial or stale data | Show where the data came from and when it was read. |
| Actions | Show full statement |
| Next nudges | Why was money deducted?<br>What came in this week?<br>Show my full statement |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | 6 · Recent transactions |

---

### 7 · Bank charges

| Field | Details |
|---|---|
| Answers | What is my bank charging me?<br>Why was money cut?<br>What is this unknown debit? |
| Fields and sources | Debits identified as bank charges in the last ninety days, from Account Aggregator<br>Charge alerts, from SMS |
| Calculation | Big number: add up all bank charges in the last ninety days.<br>List each charge with a plain name, what caused it and the date.<br>Tip line: take the single largest charge and say what would have avoided it. |
| Use when | There is at least one charge in the last ninety days. |
| Do not use when | There are no charges. Answer in text: "No bank charges in the last 90 days." |
| Partial or stale data | If the type of a charge is not recognised, show the bank's own description exactly as given. |
| Actions | None |
| Next nudges | How do I avoid the bounce charge?<br>Show my statement<br>What is my balance? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | 7 · Bank charges |

---

### 8 · In and out totals

| Field | Details |
|---|---|
| Answers | What came in and what went out?<br>What are my total credit and total debit?<br>Did I save anything this month? |
| Fields and sources | Credits and debits for the period, from Account Aggregator |
| Calculation | Came in: add up all credits in the period.<br>Went out: add up all debits in the period, leaving out transfers between the customer's own accounts.<br>Stayed with you: subtract went out from came in.<br>Comparison: work out the percentage change against the same days of the previous month. |
| Use when | At least seven days of bank data are available. |
| Do not use when | Only SMS is connected, because SMS misses many debits. |
| Partial or stale data | If the month is not complete, show the dates covered and leave out the comparison. |
| Actions | None |
| Next nudges | Where did my money go?<br>Where did it come from?<br>How does this compare to last month? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | 8 · In and out totals |

---

### B-42 · Where it came from

| Field | Details |
|---|---|
| Answers | Which app pays me most?<br>Where does my money come from?<br>How much came through PhonePe? |
| Fields and sources | Settlement credits labelled by payment provider, from Account Aggregator<br>Settlement alerts, from SMS |
| Calculation | Include only money that has actually settled into the bank.<br>Add up settlements for each payment app for the month.<br>Share for each app: divide that app's total by the total of all apps and multiply by 100.<br>The shares must add up to one hundred. |
| Use when | Settlements come from two or more payment apps. |
| Do not use when | Only one payment app is used. Answer in text instead. |
| Partial or stale data | The nudge "What do UPI payments cost a shop?" is answered as general knowledge with a source. The actual MDR and charges the shop paid, per app and per month, are not on Day 0: they are on the Roadmap, held back by settlement-level data reliable enough to compute charges.<br>Settlements from an app that is not recognised go under "Other UPI apps". |
| Actions | None |
| Next nudges | When was I busiest?<br>What do UPI payments cost a shop?<br>Who paid me the most? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | B-42 · Where it came from |

---

### 9 · Supplier payments

| Field | Details |
|---|---|
| Answers | What did I pay my suppliers?<br>Which supplier costs me most?<br>Did I pay Adarsh this month? |
| Fields and sources | Debits to payees identified as suppliers in the last thirty days, from Account Aggregator |
| Calculation | Include only payees identified as suppliers by name.<br>Add up the payments to each supplier over the last thirty days.<br>Sort suppliers by total, highest first.<br>Share line: add up the top two suppliers, divide by total supplier spend, and multiply by 100. |
| Use when | At least two named suppliers were paid in the last thirty days. |
| Do not use when | Payments cannot be matched to a supplier. Those stay in Top payees. |
| Partial or stale data | If it is not clear that a payee is a supplier, leave them out of this card. |
| Actions | None |
| Next nudges | Did I pay Adarsh this month?<br>What is planned this month?<br>Who do I pay the most? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | 9 · Supplier payments |

---

## C · Your bank account — trends

### 10 · Money in — trend

| Field | Details |
|---|---|
| Answers | How does this compare to last week?<br>How does this compare to last month?<br>How is money coming in day by day? |
| Fields and sources | Business credits by day, from Account Aggregator<br>Business credits by day, from SMS |
| Calculation | Add up business credits for each day, each week or each month, depending on the chosen view.<br>Chart only periods that are complete.<br>Comparison: work out the percentage change between the latest complete period and the one before it. |
| Use when | At least four complete periods exist for the chosen view. |
| Do not use when | Fewer than four complete periods. Use the Income card instead. |
| Partial or stale data | Never chart the current period while it is still in progress. |
| Actions | Day, week and month switch |
| Next nudges | Why was that week so strong?<br>Where did my money go?<br>How is this month going? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | 10 · Money in - trend |

---

### 11 · Money out — trend

| Field | Details |
|---|---|
| Answers | Am I spending more?<br>How does this month's spending compare to last month? |
| Fields and sources | Debits by day, from Account Aggregator |
| Calculation | Add up debits for each day, each week or each month, depending on the chosen view, leaving out transfers between the customer's own accounts.<br>Chart only periods that are complete.<br>Comparison: work out the percentage change between the latest complete period and the one before it. |
| Use when | At least four complete periods exist for the chosen view. |
| Do not use when | Only SMS is connected. |
| Partial or stale data | Never chart the current period while it is still in progress. |
| Actions | Day, week and month switch |
| Next nudges | Where did my money go?<br>What is planned this month?<br>How does money in compare? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | 11 · Money out - trend |

---

### 12 · Business transactions — trend

| Field | Details |
|---|---|
| Answers | How many customers paid me?<br>Which day was busiest? |
| Fields and sources | Business credits by day, from Account Aggregator<br>Business credits by day, from SMS |
| Calculation | Count the number of business credits, not their value, for each day, week or month.<br>Comparison: work out the percentage change in count between the latest complete period and the one before it. |
| Use when | At least seven days of data, with payments recorded one by one. |
| Do not use when | Payments arrive only as one daily settlement, because the count would be wrong. |
| Partial or stale data | Never chart the current period while it is still in progress. |
| Actions | Day, week and month switch |
| Next nudges | When was I busiest?<br>Who paid me the most?<br>How is money coming in this week? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | 12 · Business transactions - trend |

---

### 13 · Average balance trend

| Field | Details |
|---|---|
| Answers | What is my average balance?<br>Will a lender look at this?<br>Is my balance improving? |
| Fields and sources | Daily closing balances, from Account Aggregator |
| Calculation | For each month, add up every daily closing balance and divide by the number of days in that month.<br>Comparison: work out the percentage change against the previous month. |
| Use when | At least three complete months of balances are available. |
| Do not use when | Fewer than three complete months. |
| Partial or stale data | Always say this is a monthly average, not today's balance. |
| Actions | Day, week and month switch |
| Next nudges | What is my balance today?<br>Will a lender look at this?<br>How do I keep my balance higher? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | 13 · Average balance trend |

---

### 14 · Interest earned

| Field | Details |
|---|---|
| Answers | Did the bank pay me interest?<br>What did my savings earn?<br>Where did this credit come from? |
| Fields and sources | Credits identified as interest over the last twelve months, from Account Aggregator |
| Calculation | List each interest credit with its date.<br>Add up all interest credits over the last twelve months.<br>Show the interest rate only if the bank states it. Never work it out. |
| Use when | The account has received interest credits. |
| Do not use when | No interest credits, for example a current account. Answer in text instead. |
| Partial or stale data | If fewer than four quarters exist, show only the ones that do. |
| Actions | None |
| Next nudges | What is my average balance?<br>What is my balance today?<br>Show recent transactions |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | 14 · Interest earned |

---

### BS-01 · Bank statement — full view

| Field | Details |
|---|---|
| Answers | Show my statement<br>Show my full statement |
| Fields and sources | All transactions and the running balance for the chosen period, from Account Aggregator |
| Calculation | Money in: add up all credits in the period.<br>Money out: add up all debits in the period.<br>Net: subtract money out from money in.<br>Day total: for each day, subtract that day's debits from that day's credits. |
| Use when | The customer asks for the statement directly, or taps "Show full statement" on Recent transactions. |
| Do not use when | The customer asked a narrower question. Answer that first. |
| Partial or stale data | Show only the date range that is actually available, and say so. |
| Actions | Choose period<br>Filter money in or money out<br>Download |
| Next nudges | Why was money deducted?<br>Where did my money go?<br>What came in this month? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch. This is a full screen, not a card. |
| Figma | BS-01 · Bank statement - full view |

---

## D · Plan the season

### B-40 · Festival list

| Field | Details |
|---|---|
| Answers | When is the next festival?<br>What is coming up?<br>Which week will be busy? |
| Fields and sources | Festival dates for the customer's district, from the season calendar<br>Sales in the same week last year, from Account Aggregator and SMS |
| Calculation | Pick the next three festivals from today.<br>Days away: count the days from today to the festival date.<br>Change against a normal week: divide last year's sales in the festival week by sales in a normal week, subtract one, and multiply by 100. |
| Use when | The customer's location is known. |
| Do not use when | Location is unknown. Use state-level festivals and say so. |
| Partial or stale data | With less than twelve months of sales data, show the dates only and leave out the percentages. |
| Actions | Share this calendar (amounts hidden)<br>Remind me |
| Next nudges | How much should I stock?<br>Remind me before the festival<br>Share this calendar |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch. The festival calendar is useful with nothing connected. Last year's figures for the festival week are shown only when the user's own sales data exists. |
| Figma | B-40 · Festival list |

---

### B-41 · Stock plan

| Field | Details |
|---|---|
| Answers | How much should I stock?<br>What will the festival week cost me?<br>When do I need the cash? |
| Fields and sources | Supplier spending in a normal week and in last year's festival week, from Account Aggregator |
| Calculation | Normal week: average supplier spending in weeks without a festival.<br>Festival week: supplier spending in last year's festival week.<br>Extra stock at cost: subtract the normal week from the festival week.<br>Cash needed by: take the festival date and go back by the number of days the customer usually pays suppliers before a busy week. |
| Use when | Supplier spending is available for last year's festival. |
| Do not use when | No supplier history. |
| Partial or stale data | Always label the plan as an estimate. |
| Actions | Remind me |
| Next nudges | Will my balance cover it?<br>Remind me before the cash is needed<br>What is planned this month? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch. Shown only when the user's own sales data exists, and always labelled an estimate. |
| Figma | B-41 · Stock plan |

---

## E · What the bureau reported

### 15 · New loan detected

| Field | Details |
|---|---|
| Answers | Is there a new loan on my record?<br>I did not take this loan<br>What changed in my bureau file? |
| Fields and sources | Lender, loan type, date opened, amount sanctioned and EMI, from the credit bureau |
| Calculation | Compare the newest bureau report with the previous one.<br>A loan is new if it appears in the newest report and not in the previous one. |
| Use when | A new loan is found. |
| Do not use when | This is the customer's first bureau report, because every loan would look new. |
| Partial or stale data | Always show the date the bureau reported it. |
| Actions | This one is mine<br>I did not take this |
| Next nudges | How do I raise a dispute?<br>Who checked my credit?<br>Will this affect my score? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch. Part of the Monthly Bureau Update: the bureau is refreshed once a month for every user who has connected it, and changes are shown most important first. |
| Figma | 15 · New loan detected<br>Design conflict: The design says "we will raise a dispute with CRIF for you". Raising and tracking a bureau dispute in the app is not on Day 0; it is on the Roadmap. On Day 0, explain how to raise a dispute directly with the credit bureau and with the lender, as general knowledge with the source cited, and offer a person. |

---

### 16 · Overdue detected

| Field | Details |
|---|---|
| Answers | Have I missed a payment?<br>Why did my score drop?<br>What is overdue? |
| Fields and sources | Overdue amount and days late, from the credit bureau |
| Calculation | Show the overdue amount and days late exactly as the bureau reports them. |
| Use when | Any loan shows an overdue amount. |
| Do not use when | No loan is overdue. |
| Partial or stale data | Always show the date of the bureau report.<br>Say: "If you have already paid, it can take up to 45 days for the report to update." |
| Actions | Pay now, only for an InPrime loan<br>I already paid |
| Next nudges | What happens if I pay late?<br>Why did my score drop?<br>Remind me before the next due date |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch. Part of the Monthly Bureau Update. |
| Figma | 16 · Overdue detected<br>Design conflict: The design shows "Pay ₹550 now" on a Muthoot loan. Paying other lenders' EMIs from the chat is not on Day 0; it is on the Roadmap. On Day 0 the Pay button appears only on InPrime loans.<br>Design conflict: The design shows a "next reported to bureau" date. No data source gives this date. |

---

### 17 · Repayments marked

| Field | Details |
|---|---|
| Answers | Did my EMI reach the bureau?<br>Was my payment recorded?<br>Why has nothing changed? |
| Fields and sources | Payment status for each lender in the latest cycle, from the credit bureau |
| Calculation | Show one row per lender for the latest reporting cycle.<br>On-time streak: count the consecutive on-time payments up to the latest cycle. |
| Use when | Payment history is present in the bureau report. Expect this for only about 16 percent of accounts. |
| Do not use when | No payment history is reported. |
| Partial or stale data | If a lender has no status for the cycle, show "Not reported yet". |
| Actions | None |
| Next nudges | Why has nothing changed?<br>What is my score now?<br>Show my loans and cards |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch. Part of the Monthly Bureau Update. |
| Figma | 17 · Repayments marked |

---

### 18 · Loan closed

| Field | Details |
|---|---|
| Answers | Is my loan closed?<br>Did the bureau record it?<br>Where is my NOC? |
| Fields and sources | Closed status, closing date, total repaid and dues left, from the credit bureau |
| Calculation | Show each value exactly as the bureau reports it. |
| Use when | A loan's status has changed to closed. |
| Do not use when | The loan is still open. |
| Partial or stale data | If total repaid is missing, hide that row. |
| Actions | Ask for the No Objection Certificate. For an InPrime loan, raise a service request. |
| Next nudges | Is my score affected?<br>Show my closed loans<br>What is on my report now? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch. Part of the Monthly Bureau Update. |
| Figma | 18 · Loan closed |

---

## F · Moving your score

### B-43 · Score drop

| Field | Details |
|---|---|
| Answers | What is my score?<br>Why did it drop?<br>Is 749 good? |
| Fields and sources | Current score, previous score, report date and enquiries, from the credit bureau |
| Calculation | Change: subtract the previous score from the current score.<br>Cause line: use the bureau's top reason code, written in plain words. |
| Use when | The score has changed since the previous report. |
| Do not use when | This is the first report. Show the score without a change. |
| Partial or stale data | Always show the date the score was updated. |
| Actions | None |
| Next nudges | See what moved it<br>When will my score go back up?<br>Should I hold off on applying? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | B-43 · Score drop |

---

### 19 · Score improvement plan

| Field | Details |
|---|---|
| Answers | How do I improve my score?<br>What should I do first?<br>How long will it take? |
| Fields and sources | Reason codes, enquiry dates and overdues, from the credit bureau |
| Calculation | Pick at most three actions from the bureau reason codes.<br>Order the actions by how much they affect the score, biggest first, not by how easy they are.<br>Give each action a date by which to do it. |
| Use when | The score is below its last high, or the customer asks how to improve it. |
| Do not use when | There is no bureau report. |
| Partial or stale data | Always label any target as an estimate. |
| Actions | Remind me on the date |
| Next nudges | How long will it take?<br>What is pulling my score down?<br>Show my score over time |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch after the design is fixed. |
| Figma | 19 · Score improvement plan<br>Design conflict: The design shows points for each action (+14, +6, +3) and a target score of 772. Point figures are not allowed before compliance review. Show the actions and dates only. |

---

### B-19b · Score journey chart

| Field | Details |
|---|---|
| Answers | Am I getting there?<br>Show me my score over time<br>How long until 772? |
| Fields and sources | Score history, from the credit bureau<br>The customer's plan, from memory |
| Calculation | Draw a solid line through the actual scores from each bureau report.<br>Draw a dashed line for the plan. |
| Use when | At least three bureau reports exist. |
| Do not use when | Fewer than three reports. Two points are not a trend. |
| Partial or stale data | None. |
| Actions | None |
| Next nudges | What is left to do?<br>Why did my score drop?<br>Remind me of my next step |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch after the design is fixed. |
| Figma | B-19b · Score journey chart<br>Design conflict: The design says "+23 points to reach 772". Remove point figures until compliance review. |

---

### 20 · Explainer video

| Field | Details |
|---|---|
| Answers | Why does an enquiry hurt me?<br>What is credit utilisation?<br>Explain this to me again |
| Fields and sources | Video topic, language and length, from the video registry |
| Calculation | None. |
| Use when | The question matches the video's topic.<br>The video is returned beside the text answer. |
| Do not use when | It would replace the answer instead of adding to it.<br>The customer watched it in the last thirty days.<br>There is no version in the customer's language. |
| Partial or stale data | None. |
| Actions | Play |
| Next nudges | Not applicable on Day 0 |
| Plan | Free. No monetisation on Day 0. |
| Status | Not on Day 0. Credit score explainer videos are on the Roadmap: four short videos (score, payments, enquiries, recovery) in three languages, shown only when relevant. Held back by video production, each video with a stated reason for existing. |
| Figma | 20 · Explainer video |

---

### 21 · Full report entry point

| Field | Details |
|---|---|
| Answers | Show me my full report<br>Send me the PDF |
| Fields and sources | Number of accounts, total balance, total overdue and the report PDF, from the credit bureau |
| Calculation | Accounts: count all accounts on the report.<br>Balance: add up the balances of all active accounts.<br>Overdue: add up the overdue amounts of all accounts. |
| Use when | The bureau is connected. |
| Do not use when | There is no report. |
| Partial or stale data | Always show the report date. |
| Actions | Open the full report<br>Send me the report as PDF |
| Next nudges | Who checked my credit?<br>Show my loans and cards<br>Why is my score not higher? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | 21 · Full report entry point |

---

### B-39 · Band ladder (sheet)

| Field | Details |
|---|---|
| Answers | What score do I need?<br>What would the next band get me?<br>Is 749 good? |
| Fields and sources | Customer's score, from the credit bureau<br>Band ranges, from the credit bureau |
| Calculation | Find the band whose range contains the customer's score and highlight it. |
| Use when | The customer asks about bands, or taps the score meter. |
| Do not use when | There is no score. |
| Partial or stale data | None. |
| Actions | Okay, got it |
| Next nudges | How do I reach the next band?<br>Why is my score not higher?<br>What is my score? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | B-39 · Band ladder (sheet) |

---

## G · Your InPrime loan

### 22 · RO details (relationship manager)

| Field | Details |
|---|---|
| Answers | Who is my RO?<br>Who is handling my loan?<br>I want to talk to someone about my loan |
| Fields and sources | RO name, branch, phone number and office hours, from InPrime records |
| Calculation | None. |
| Use when | The customer has an InPrime loan and explicitly asks for their RO, or the conversation calls for it, for example a hardship or an overdue they want to discuss. |
| Do not use when | The customer has not asked and the conversation does not call for it. Never shown unprompted.<br>The customer has no InPrime loan. |
| Partial or stale data | No RO assigned: say so and offer the human escalation path.<br>Outside office hours: show the hours with the call option. |
| Actions | Call |
| Next nudges | Show my loan details<br>When is my next EMI?<br>Update my details |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch. RO details are shared only when the user asks for their RO, or when the conversation calls for it, with an option to call.<br>To confirm: whether a callback request is also offered. The master document lists only the option to call. |
| Figma | 22 · Relationship manager |

---

### 23 and 23b · Application status

| Field | Details |
|---|---|
| Answers | Where is my application?<br>Has it been approved?<br>When does the money come? |
| Fields and sources | Application stage, dates, decision, amount and rate, from the InPrime loan system |
| Calculation | Show four steps: application received, documents checked, credit decision, money in your account.<br>Mark each step done, in progress or expected, with its date.<br>When finished, show one of three end states: approved, disbursed or rejected. |
| Use when | The customer has an application. |
| Do not use when | There is no application. |
| Partial or stale data | If the current stage is unknown, show the last known stage with its date. |
| Actions | None |
| Next nudges | Why was I rejected?<br>When is my first EMI?<br>When does the money come? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | 23 · Application status<br>23b · Application status - the other three states |

---

### 24 · Next loan eligibility

| Field | Details |
|---|---|
| Answers | How much more can I borrow?<br>Can I get a top-up?<br>What is my limit? |
| Fields and sources | Indicative amount, rate and tenure, from credit policy rules<br>Amount already applied for, from InPrime records |
| Calculation | Indicative amount: as given by the credit policy rules for this customer.<br>EMI: use the EMI formula in B-38 with that amount, rate and tenure.<br>If part of the amount is already applied for, say how much. |
| Use when | An InPrime customer asks about borrowing more, or a loan makes real sense for what they are dealing with. |
| Do not use when | The customer has an overdue.<br>It would be the answer to a question about something else. |
| Partial or stale data | Always label it "Indication only". Never call it an approval. |
| Actions | See my top-up application |
| Next nudges | What would my EMI be?<br>Which InPrime loan fits me?<br>How do I apply? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | 24 · Next loan eligibility |

---

### 25 · Active InPrime loans

| Field | Details |
|---|---|
| Answers | What do I owe InPrime?<br>How many payments are left?<br>When does this loan end? |
| Fields and sources | Outstanding amount, sanctioned amount, EMIs paid, dates and status of each EMI, from InPrime records |
| Calculation | Still to pay: the outstanding amount from InPrime records.<br>Paid count: number of EMIs paid out of total EMIs.<br>Mark each EMI as on time, late or not yet due. |
| Use when | The customer has an active InPrime loan. |
| Do not use when | No active InPrime loan. |
| Partial or stale data | If the records are more than 24 hours old, show when they were read. |
| Actions | None |
| Next nudges | Show my schedule<br>Show closed loans<br>When is my next EMI? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | 25 · Active InPrime loans |

---

### B-37 · Loan details

| Field | Details |
|---|---|
| Answers | Tell me about this loan<br>What is my interest rate?<br>When is my next EMI? |
| Fields and sources | Loan amount, amount repaid, EMIs paid, next EMI, auto-pay status and loan terms, from InPrime records |
| Calculation | Repaid: add up all EMIs paid so far. |
| Use when | The customer has an active InPrime loan. |
| Do not use when | No active InPrime loan. |
| Partial or stale data | If auto-pay status is unknown, hide the auto-pay line. |
| Actions | Download statement |
| Next nudges | Show my schedule<br>What has this loan cost me so far?<br>When is my next EMI? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | B-37 · Loan details |

---

## H · What your credit costs

### B-36 · All my loans

| Field | Details |
|---|---|
| Answers | List every loan in my name<br>What leaves every month?<br>Show me my loans and cards |
| Fields and sources | Active and closed loans, from the credit bureau<br>EMI for InPrime loans, from InPrime records<br>EMI for other loans, from the credit bureau, or what the customer told us |
| Calculation | Every month: add up the EMIs of all active loans whose EMI is known.<br>If a loan's EMI is not known, list the loan, leave it out of the total, and say so. |
| Use when | The bureau is connected. |
| Do not use when | No loans are found. Answer in text instead. |
| Partial or stale data | Mark any EMI the customer told us as "you told us".<br>Keep closed loans collapsed until asked. |
| Actions | Show closed loans |
| Next nudges | What will these loans cost me in total?<br>How much am I paying every month?<br>Who checked my credit? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | B-36 · All my loans |

---

### B-33 · Rate list

| Field | Details |
|---|---|
| Answers | Which loan is most expensive?<br>Which should I clear first?<br>Am I being overcharged? |
| Fields and sources | Interest rate for each loan, from InPrime records, a sanction letter, or what the customer told us |
| Calculation | Use the stated yearly interest rate for each loan.<br>If only the EMI, loan amount and tenure are known, work out the yearly rate that makes these three agree.<br>Sort loans from highest rate to lowest. Our own loan stays in the list in its true position. |
| Use when | The rate is known or can be worked out for at least two loans. |
| Do not use when | Any loan's rate is unknown and cannot be worked out. |
| Partial or stale data | Show where each rate came from. |
| Actions | Show me the maths |
| Next nudges | Not applicable on Day 0 |
| Plan | Free. No monetisation on Day 0. |
| Status | Not on Day 0. "Which loan to clear first" is on the Roadmap: the real cost of each loan and the saving from clearing it, across every lender. Held back by legal sign-off on comparative advice. |
| Figma | B-33 · Rate list |

---

### B-34 · Interest over the term

| Field | Details |
|---|---|
| Answers | What will these loans cost me in total?<br>Which one is really costing me most? |
| Fields and sources | Remaining EMIs and outstanding principal, from InPrime records, the credit bureau, or what the customer told us |
| Calculation | For each loan: multiply the EMI by the number of EMIs left, then subtract the outstanding principal. The result is the interest still to pay.<br>Total: add up the interest still to pay across all loans. |
| Use when | The remaining tenure is known for each loan. |
| Do not use when | A loan pays interest only with no end date. Show its monthly interest instead. |
| Partial or stale data | If a loan's data is missing, name the loan and leave it out of the total. |
| Actions | None |
| Next nudges | What has my InPrime loan cost so far?<br>What if I close a loan early?<br>How much am I paying every month? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | B-34 · Interest over the term |

---

### B-35 · Interest split

| Field | Details |
|---|---|
| Answers | What has this loan cost me?<br>How much of it is interest?<br>How much have I paid back so far? |
| Fields and sources | Loan amount, EMI, tenure and amount paid so far, from InPrime records |
| Calculation | You will pay back: multiply the EMI by the total number of EMIs.<br>Extra you pay for borrowing: subtract the loan amount from what you will pay back.<br>Already paid: add up all EMIs paid so far. |
| Use when | The loan is an InPrime loan, or another loan whose full terms are known. |
| Do not use when | The loan's terms are incomplete. |
| Partial or stale data | None. |
| Actions | None |
| Next nudges | What if I close it early?<br>How much is left to pay?<br>Show my schedule |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | B-35 · Interest split |

---

## I · Your InPrime loan — repayment

### 26 · Loan details and schedule

| Field | Details |
|---|---|
| Answers | Tell me about this loan<br>Show me my repayment schedule<br>When does it end? |
| Fields and sources | Lender, purpose, amount sanctioned, rate, start date, end date and the repayment schedule with status, from InPrime records |
| Calculation | Show the six loan facts, then the next four instalments with their status. |
| Use when | The customer has an active InPrime loan. |
| Do not use when | No active InPrime loan. |
| Partial or stale data | If the records are more than 24 hours old, show when they were read. |
| Actions | Show all instalments |
| Next nudges | When is my next EMI?<br>Download my statement<br>Update my details |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | 26 · Loan details and schedule |

---

### 27 · Next repayment

| Field | Details |
|---|---|
| Answers | When is my EMI?<br>How much is due?<br>How will it be taken? |
| Fields and sources | Amount, due date, payment mode, bank account and mandate reference, from InPrime records |
| Calculation | Find the first unpaid instalment in the schedule. |
| Use when | An EMI is coming up. |
| Do not use when | An EMI is overdue. Use card 29 instead. |
| Partial or stale data | If mandate status is unknown, say "check your auto-pay". |
| Actions | Pay through BBPS instead<br>Remind me |
| Next nudges | Will my balance cover it?<br>Is auto-pay on?<br>Show my schedule |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | 27 · Next repayment |

---

### 28 · Last repayment

| Field | Details |
|---|---|
| Answers | Did my EMI go through?<br>When did I last pay?<br>How was it paid? |
| Fields and sources | Amount, date, payment mode, reference number and time cleared, from InPrime records |
| Calculation | Find the most recent paid instalment. |
| Use when | At least one payment has been made. |
| Do not use when | No payment has been made yet. |
| Partial or stale data | If a payment is still processing, say "processing", never "paid". |
| Actions | Download receipt |
| Next nudges | When is my next EMI?<br>Show my schedule<br>How much is left to pay? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | 28 · Last repayment |

---

### 29 · InPrime loan overdue

| Field | Details |
|---|---|
| Answers | My EMI did not go through<br>What happens if I miss it?<br>How much do I owe now? |
| Fields and sources | EMI, charges, due date, days late and the date it will be reported to the bureau, from InPrime records |
| Calculation | Total to pay now: add the overdue EMIs and the charges.<br>Days late: count the days from the due date to today. |
| Use when | The customer has an overdue InPrime EMI. |
| Do not use when | No overdue. |
| Partial or stale data | If a charge has not been confirmed yet, show it as "may apply". |
| Actions | Pay the amount, after confirming it with the customer<br>Show my RO's details |
| Next nudges | What happens if I pay late?<br>Why did my EMI bounce?<br>Remind me before the next due date |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch after the design is fixed. |
| Figma | 29 · InPrime loan overdue<br>Design conflict: The design says "your score drops by about 40 points". No point figures. Say the payment will be reported to the bureau as missed. |

---

## J · InPrime products

### 30a to 30e · Product cards — Smart, Super, Welcome, Winner, Star

| Field | Details |
|---|---|
| Answers | What loans do you give?<br>Which one is right for me?<br>What is a Winner Loan? |
| Fields and sources | Name, who it is for, amount range, tenure and use, from the product catalogue<br>Whether it is open to this customer, from InPrime records |
| Calculation | None. |
| Use when | The customer asks about a product, or a loan makes real sense for what they are dealing with. |
| Do not use when | It would be the answer to a question about something else.<br>The customer has an overdue. |
| Partial or stale data | Star Loan shows "Coming soon" with no apply option. |
| Actions | Check what I qualify for |
| Next nudges | Which one is right for me?<br>What would my EMI be?<br>How do I apply? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch. Star Loan is coming soon. |
| Figma | 30a · Smart Loan - product card<br>30b · Super Loan - product card<br>30c · Welcome Loan - product card<br>30d · Winner Loan - product card<br>30e · Star Loan - product card |

---

### 31 · Compare products

| Field | Details |
|---|---|
| Answers | Which loan should I take?<br>What else can I get?<br>Compare your loans |
| Fields and sources | All products, from the product catalogue<br>Which products are open to this customer, from InPrime records |
| Calculation | Order products by how well they fit the customer: running loan first, then open to you, then others.<br>Keep products that do not apply visible but greyed out. |
| Use when | The customer asks to compare InPrime loans. |
| Do not use when | The customer has not asked about loans. |
| Partial or stale data | If nothing is connected, show the products without fit labels. |
| Actions | Apply |
| Next nudges | What would my EMI be?<br>Check what I qualify for<br>What documents do I need? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | 31 · Compare products<br>Design conflict: "Which loan should I take?" must be answered by explaining fit, never by recommending that the customer borrow. |

---

### 32 · Apply entry point

| Field | Details |
|---|---|
| Answers | I want to apply<br>Where do I apply?<br>Start a new loan |
| Fields and sources | Documents needed, from the product catalogue |
| Calculation | None. |
| Use when | The customer asks to apply. |
| Do not use when | The customer has not asked to apply. |
| Partial or stale data | If the website is down, offer a callback. |
| Actions | Apply on inprime.in. Pass the app as the source. |
| Next nudges | What documents do I need?<br>What would my EMI be?<br>Which InPrime loan fits me? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | 32 · Apply entry point |

---

### B-38 · EMI calculator

| Field | Details |
|---|---|
| Answers | What would my EMI be?<br>What if I pay extra?<br>How much can I borrow? |
| Fields and sources | Loan amount, yearly interest rate and tenure in months, from the customer or the product defaults |
| Calculation | Monthly rate: divide the yearly interest rate by twelve, then by one hundred.<br>EMI: multiply the loan amount by the monthly rate and by (one plus the monthly rate) raised to the power of the number of months. Divide the result by (one plus the monthly rate) raised to the power of the number of months, minus one.<br>Paid over the tenure: multiply the EMI by the number of months.<br>Interest: subtract the loan amount from the amount paid over the tenure.<br>Run the calculation in the app so the answer changes instantly as the customer moves the sliders. |
| Use when | The customer asks about an EMI or what they can afford. |
| Do not use when | It would be shown to encourage borrowing. |
| Partial or stale data | Always label the result an estimate. The final rate is set after the credit check. |
| Actions | Check what I qualify for |
| Next nudges | Which InPrime loan fits this?<br>What if I pay it off early?<br>How do I apply? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | B-38 · EMI Calculator |

---

## K · Intelligent cards on landing, and system cards

### Next EMI — intelligent card

| Field | Details |
|---|---|
| Answers | When is my next EMI?<br>Is auto-pay on? |
| Fields and sources | Next instalment amount, due date and auto-pay status, from InPrime records |
| Calculation | Find the first unpaid instalment.<br>Days to go: count the days from today to the due date. |
| Use when | An InPrime EMI is due within seven days and auto-pay is on. |
| Do not use when | An EMI is overdue, or auto-pay is off. |
| Partial or stale data | If auto-pay status is unknown, hide the auto-pay line. |
| Actions | Remind me |
| Next nudges | Will my balance cover it?<br>How did my shop do this month?<br>Show my schedule |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | O-07 · Home — composer + deck<br>OB-W1 |

---

### EMI due, not covered

| Field | Details |
|---|---|
| Answers | Is my EMI covered? |
| Fields and sources | Amount, due date and auto-pay status, from InPrime records |
| Calculation | Show this card when the EMI is due within three days and auto-pay is off. |
| Use when | Auto-pay is off or cancelled and the EMI is due within three days. |
| Do not use when | Auto-pay is on.<br>The EMI is already paid. |
| Partial or stale data | If auto-pay status is unknown, treat the EMI as not covered and say so. |
| Actions | Remind me<br>Pay now |
| Next nudges | Will my balance cover it?<br>How do I turn on auto-pay?<br>Show my schedule |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | H-02 · Home — EMI due, not covered |

---

### Alert banner

| Field | Details |
|---|---|
| Answers | Is anything wrong? (shown without being asked) |
| Fields and sources | Overdues, due dates and auto-pay status, from InPrime records<br>Overdues on other loans, from the credit bureau |
| Calculation | Tier 1: money already missed.<br>Tier 2: money due and not covered.<br>Tier 3: something blocks a payment.<br>Show only the highest tier present.<br>If several items share that tier, count them, add up their amounts, and name the oldest in the second line. |
| Use when | Any tier 1, 2 or 3 item exists. |
| Do not use when | Only score changes, offers or festival notes exist. These never go in the banner. |
| Partial or stale data | A bureau overdue shows its report date.<br>When the last overdue clears, turn the banner green for the rest of the session. |
| Actions | Tap to open the answer with the payment action |
| Next nudges | Come from the answer the banner opens |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | BN-01 to BN-08<br>H-01 · Home — two loans overdue |

---

### Connect sheet

| Field | Details |
|---|---|
| Answers | Any question that needs data the customer has not connected |
| Fields and sources | Connector name, why it is needed, what it unlocks, what it reads, and the provider line<br>Day-0 connectors: InPrime loan records, credit bureau, Account Aggregator, SMS (including QR settlement messages)<br>Location and DigiLocker are not on Day 0; both are on the Roadmap |
| Calculation | None. |
| Use when | The question needs a connector that is not connected and has not been declined in this chat. |
| Do not use when | The customer declined this connector earlier in the same chat.<br>During onboarding. |
| Partial or stale data | If the provider is down, say "try again shortly" and do not show the sheet. |
| Actions | Connect<br>Not now |
| Next nudges | What is an Account Aggregator?<br>How do I stop it later?<br>What can InPrime see about me? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | 11 · Connections & permissions — bottom sheets |

---

### Monthly report card — intelligent card

| Field | Details |
|---|---|
| Answers | How did my shop do this month? |
| Fields and sources | Credits and debits, from Account Aggregator and SMS |
| Calculation | Money in: add up business credits this month.<br>Money out: add up debits this month, leaving out transfers between the customer's own accounts.<br>Stayed with you: subtract money out from money in.<br>Comparison: percentage change against last month, only if both months are complete. |
| Use when | Asked in the chat, with at least seven days of bank or SMS data.<br>On landing, as an intelligent card, for the previous complete month. A push notification also announces it once a month.<br>To confirm: how many days into the new month the card stays on landing. |
| Do not use when | Less than seven days of data. |
| Partial or stale data | If some accounts are not linked, label how many are included.<br>If the month is not complete, show the dates covered and leave out the comparison. |
| Actions | Share (amounts and personal details hidden unless the user opts in)<br>Send me this card every month |
| Next nudges | When was I busiest?<br>Where did my money go?<br>Who paid me the most? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | 04 · Thread — My shop + report card |

---

### Monthly Bureau Update — intelligent card

| Field | Details |
|---|---|
| Answers | What changed in my credit report this month?<br>Is anything new on my record?<br>Did my score move? |
| Fields and sources | This month's and last month's bureau reports for the user, from the credit bureau: score, new loans, overdues, repayments recorded, loans closed, enquiries |
| Calculation | Compare this month's report with last month's report.<br>List every change: score movement, new loan, new overdue, repayment recorded, loan closed, new enquiry.<br>Rank the changes by importance: a new loan the user may not recognise first, then a new overdue, then a score drop, then new enquiries, then repayments recorded and loans closed.<br>Show the most important change on the card, with a count of the others.<br>Score change: subtract last month's score from this month's score. |
| Use when | On landing, after the monthly refresh, for every user who has connected the bureau.<br>The user taps the monthly bureau update notification.<br>The user asks what changed in their report. |
| Do not use when | The bureau is not connected.<br>This is the user's first report, because there is nothing to compare. Show the score card instead. |
| Partial or stale data | Always show the date of each report.<br>If this month's refresh failed, keep last month's card and say the update is delayed.<br>If nothing changed, say "No changes in your report this month" in text. |
| Actions | See all changes<br>This loan is not mine (opens card 15) |
| Next nudges | Why did my score move?<br>Who checked my credit?<br>Show my loans and cards |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch. The bureau is refreshed once a month for every user who has connected it. |
| Figma | Not designed yet. The detailed change cards are 15 to 18 on the Artifacts Board. |

---

### Reminder due — intelligent card

| Field | Details |
|---|---|
| Answers | What did I ask you to remind me about? |
| Fields and sources | Reminder text, date and the chat it came from, from the reminders store |
| Calculation | Show reminders due today or overdue, earliest first. |
| Use when | A reminder the user set is due today or has passed without being marked done. |
| Do not use when | No reminder is due. |
| Partial or stale data | If the linked data changed, for example the EMI was already paid, say so and offer to clear the reminder. |
| Actions | Done<br>Remind me later |
| Next nudges | Show all my reminders<br>Remind me about something else<br>Stop one of these |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch |
| Figma | D-02 · Reminders |

---

## L · New Day-0 products

### Document Check result

| Field | Details |
|---|---|
| Answers | Is this loan offer genuine?<br>Is this message real?<br>Explain this letter to me<br>What will my EMI be on this? |
| Fields and sources | The photo or file the user sent (JPG, PNG or PDF up to 10 MB)<br>The model's general knowledge of genuine and fake loan offers<br>InPrime records, only to say whether a letter is from InPrime and whether its figures match the user's InPrime loan |
| Calculation | None by the model. Any figure read from the document is shown exactly as written in the document, with where it was read from. If the letter is from InPrime, code compares its figures with InPrime records. |
| Use when | The user sends a document and asks about it.<br>The user chooses the dedicated Document Check option. |
| Do not use when | The upload is not a document, for example a photo of the shop. Say so in text. |
| Partial or stale data | Blurry or cut off: ask for a retake.<br>Over 10 MB or a locked PDF: say so and ask for another file.<br>Cannot decide: give the verdict "not sure" with reasons, and offer a person. |
| Actions | Talk to a person (when the verdict is not sure) |
| Next nudges | How do I spot a fake loan offer?<br>Check another document<br>What should I do now? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch. Answered from the model's general knowledge, with its own dedicated option as well as in conversation. |
| Figma | UP-01 to UP-07 · upload flow<br>To confirm: the verdict card and the "not sure" state are not designed yet. |

---

### Service request

| Field | Details |
|---|---|
| Answers | I want to change my mobile number<br>Update my address<br>Change my bank account<br>What is the status of my request? |
| Fields and sources | The change the user asked for, read from the chat<br>Request reference and status, from InPrime's servicing system |
| Calculation | None. |
| Use when | An existing InPrime customer asks to change any of their details.<br>The user asks about a request already raised. |
| Do not use when | The user is not an InPrime customer.<br>The user only asked a question about their loan. Answer it in the chat instead. |
| Partial or stale data | Before raising, read the request back and ask the user to confirm.<br>If the servicing system is down, say the request could not be raised and offer to try again. |
| Actions | Confirm and raise<br>Edit |
| Next nudges | What is the status of my request?<br>Show my loan details<br>Who is my RO? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch. The app raises the request and notifies the user of status changes; what happens after the request is raised is handled outside the app. |
| Figma | Proposed artifacts · Update my details |

---

### Shareable card and shop poster

| Field | Details |
|---|---|
| Answers | Share this with another shopkeeper<br>Make a poster for my shop |
| Fields and sources | The card or content being shared<br>Shop name and trade, from what the user told us<br>Poster templates, from the Content Library |
| Calculation | None. On shared cards, amounts and personal details are hidden by default. If the user opts in to show amounts, round them to the nearest hundred. |
| Use when | The user taps share on a card, the festival calendar or a business knowledge answer.<br>The user asks for a poster. |
| Do not use when | The content contains another person's personal details. |
| Partial or stale data | No shop name: ask for it before making the poster. |
| Actions | Show amounts (opt in)<br>Share on WhatsApp<br>Save image |
| Next nudges | Make another poster<br>Share the festival calendar<br>How do I get more customers? |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch. Every share carries the app identity and an install link, and the install is attributed to the sharer. |
| Figma | Not designed yet. |

---

### Business Knowledge answer

| Field | Details |
|---|---|
| Answers | Will I pay charges on UPI payments?<br>How does GST work for my shop?<br>Which government schemes can I use?<br>Should I sell online? |
| Fields and sources | General business knowledge, from approved sources in the Content Library and the model's general knowledge |
| Calculation | None from the user's data. A figure that is a public rule, for example an MDR rate or a GST threshold, is quoted with its source and the date it applies from. |
| Use when | The question is about business, money rules or the user's trade in general, not about the user's own figures. |
| Do not use when | The question needs the user's own data. Use the matching data card, or the connect sheet. |
| Partial or stale data | Always say the answer is general knowledge, not the user's own data.<br>Cite the source.<br>If the rule may have changed, say when the source was last reviewed. |
| Actions | Share (amounts and personal details hidden) |
| Next nudges | How does this affect my shop?<br>Tell me more<br>Share this with another shopkeeper |
| Plan | Free. No monetisation on Day 0. |
| Status | Launch. Text only, no card. Detail page and design to be added. |
| Figma | Not designed yet. |
