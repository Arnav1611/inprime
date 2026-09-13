# artifacts.md

The catalogue. **A lookup table, not an instruction file** — load the row, not the file. Picking
rules are in `artifact-picker.md`.

One artifact, one use case, its own fixed labels.

## Understand my shop

| ID | Artifact | Trigger | Data from |
|---|---|---|---|
| A-01 | Income this month | How did my shop do this month | QR, SMS |
| A-02 | Yesterday's takings | What came in yesterday | QR, SMS |
| A-03 | Money out | Where did my money go | AA, SMS |
| A-04 | Recurring debits | What else is being cut · what am I paying everywhere | AA, SMS |
| A-05 | Where it came from | Total across all my QRs | QR |
| A-06 | Month comparison | Compared to last month | QR, SMS |
| A-07 | Sales by week | When was I busiest | QR, SMS |
| A-08 | Sales by day | Which day is my best | QR, SMS |
| A-09 | The year | Compared to last year · why is business slow | QR, SMS |
| A-10 | When money lands | When does my QR money land | QR |
| A-11 | Margin card | Am I actually making money | **No connector** |

## Plan the season

| ID | Artifact | Trigger | Data from |
|---|---|---|---|
| A-12 | Festival list | When is the next festival | Season calendar |
| A-13 | Stock plan | How much should I stock | Season calendar |

## Track my loans

| ID | Artifact | Trigger | Data from |
|---|---|---|---|
| A-14 | Loan card | When is my EMI · how much do I owe · payments left · when does it end | InPrime |
| A-15 | All my loans | List every loan in my name | Bureau |
| A-16 | Loan details | Tell me about this loan | InPrime |
| A-17 | EMI due this month | What am I paying every month | InPrime |
| A-18 | Total owed | What is my total debt | InPrime + bureau |
| A-19 | Repayment schedule | Show my repayment schedule | InPrime · full-screen |
| A-20 | Payment calendar | When is everything due | InPrime + customer-told · grid view |
| A-21 | Document list | Where is my agreement · I need a statement or NOC | InPrime |
| A-22 | Document check | Are my papers right | DigiLocker, InPrime |

## Pay less, pay smarter

| ID | Artifact | Trigger | Data from |
|---|---|---|---|
| A-23 | Rate list | Which is most expensive · which to clear first · am I overcharged | InPrime + bureau |
| A-24 | Interest over the term | What will these loans cost in total | InPrime + bureau |
| A-25 | Interest split | What has this loan cost me | InPrime |
| A-26 | Closing amount | What to close it today | InPrime |
| A-27 | Savings estimate | Can I move a loan somewhere cheaper | InPrime + bureau |
| A-28 | **Calculator** | What would my EMI be · what if I pay extra · how much can I borrow | InPrime · **the only interactive artifact** |

## Borrow more

| ID | Artifact | Trigger | Data from |
|---|---|---|---|
| A-29 | Eligibility card | How much can I get · top-up · remaining limit | InPrime · marked indicative |
| A-30 | Options list | Where will I find that money · business is down · can I restructure | InPrime + bureau |
| A-31 | Application tracker | Where is my application | InPrime · vertical steps |
| A-32 | Checklist | What is pending from me · what documents do I need | InPrime |
| A-33 | Scheme list | Schemes I qualify for · cheaper government loan | **No connector** |

## Credit score

| ID | Artifact | Trigger | Data from |
|---|---|---|---|
| A-34 | Score meter | What is my score · is that good or bad | Bureau |
| A-35 | Score change | Why did it drop | Bureau · ranked reasons, see `score.md` |
| A-36 | Helping / hurting | What is hurting my score | Bureau |
| A-37 | Band ladder | What score do I need · what would the next band get me | Bureau |
| A-38 | Score line | Has my score improved | Bureau · only after three checks |
| A-39 | Report summary | Show my full report | Bureau · full-screen scrollable PDF |
| A-40 | Enquiry list | Who checked my credit | Bureau |
| A-69 | Score improvement plan | What should I do to improve my score | Bureau · see `score.md` |
| A-70 | Score factor explainer | Why does this affect my score | Explainer library |

## Stay safe and on time

| ID | Artifact | Trigger | Data from |
|---|---|---|---|
| A-41 | Single transaction | What is this charge · why was extra money cut | AA, SMS |
| A-42 | Bounce risk | Will my EMI bounce | InPrime + AA |
| A-43 | Fraud result | Is this message real | The message itself |
| A-44 | Reminder strip | Pinned, not asked for | Whichever connector holds the date |

## Get help

| ID | Artifact | Trigger | Data from |
|---|---|---|---|
| A-45 | Request card | Where is my request · where is my dispute · change my address | InPrime |
| A-46 | Cover card | Do I have insurance · am I covered for hospital | **No connector** |
| A-47 | Callback card | I want to talk to someone | Routes to a person |

## System states

| ID | Artifact | Shown when |
|---|---|---|
| A-48 | Consent card | Before any connector is read |
| A-49 | Working on it | Any fetch over two seconds |
| A-50 | Could not do it | Any failure |
| A-51 | Nothing to show yet | Any empty state |

## Income and cashflow

| ID | Artifact | Trigger | Data from |
|---|---|---|---|
| A-52 | Income card | How did my shop do yesterday / this week / this month | AA · three periods, one card |
| A-53 | Planned outflow | What do I have to pay this month · what is due this week | AA + InPrime · certain and estimated kept apart |
| A-54 | Top payers | Who pays me the most | AA · unnamed handles are normal |
| A-55 | Top payees | Who do I pay the most | AA |

## Bank statement — expandable, one section at a time

| ID | Artifact | Trigger | Data from |
|---|---|---|---|
| A-56 | Account balance | What is my balance right now | AA |
| A-57 | Recent transactions | What came in and went out recently | AA |
| A-58 | Bank charges | What has the bank charged me | AA |
| A-59 | Credit and debit summary | How much came in versus went out | AA · day, week, month |
| A-60 | Business transactions | How many payments moved through the account | AA |
| A-61 | Supplier payments | How much did I pay my suppliers | AA |
| A-62 | Average balance trend | Is my balance growing or shrinking | AA · six months |
| A-63 | Interest earned | How much interest did the bank pay me | AA · often zero |
| A-64 | Full bank statement | Show me the whole statement | AA · full-screen scrollable |

## Alerts — pushed, never picked

| ID | Artifact | Fires when |
|---|---|---|
| A-65 | New loan detected | A loan appears the customer did not expect. Carries a "this is not mine" path |
| A-66 | Overdue detected | A loan shows overdue |
| A-67 | Payment marked | A payment is recorded |
| A-68 | Loan closed | A loan closes. States whether an NOC is available |

Every alert carries its detection time. Bureau data lags.

## Our loan and our products

| ID | Artifact | Trigger | Data from |
|---|---|---|---|
| A-71 | Relationship manager | Who do I contact about my loan | InPrime |
| A-72 | Application status | Where is my loan application | InPrime · vertical steps |
| A-73 | Next repayment | When is my next EMI, how will it be paid | InPrime · states NACH or BBPS |
| A-74 | Last repayment | Did my last EMI go through, how | InPrime |
| A-75 | Loan overdue | Is my loan overdue | InPrime |
| A-76 | Product list | What loans do you offer | Product catalogue · nothing marked best or popular |
| A-77 | Apply entry point | How do I apply | Product catalogue · leaves the app |

## Components — patterns, never picked directly

Up/down pill · Split bar · Stat pair · Payment squares · Collapsed row · Progress bar ·
Change before/after · Status pill · Green callout · Blue callout · Amber callout (weigh) ·
Amber callout (fix) · Red callout · Main button · Reminder button · Connect prompt ·
Share and download · Follow-up questions

## Pairs — the only cases where two artifacts are allowed

| Question | First | Second |
|---|---|---|
| Which should I clear first | A-23 Rate list | Amber callout, weigh |
| Why did my score drop | A-35 Score change | Amber callout, fix |
| Am I being overcharged | A-23 Rate list | A-27 Savings estimate |
| Business is down | A-30 Options list | A-47 Callback card |
| Am I covered for hospital | A-46 Cover card | A-33 Scheme list, if there is a gap |
