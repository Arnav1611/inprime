# artifact-picker.md

> Owner: Admin. Fourth in the chain. Chooses **one** artifact, or none.
> This index reflects the 12 Sep design catalogue — 77 artifacts, IDs A-01 to A-77, plus 18 shared
> components C-01 to C-18. **It supersedes the 44-item "Artifacts" Notion page**, which predates the
> group-1-through-6 additions (A-52–77) and several renames. Reconcile that page before relying on it.

## Job

- Choose the artifact built for this use case. Artifacts are use-case specific, never generic
  containers — decided 8 Sep
- If nothing matches, return **none**. A card for *"is my data safe"* makes that answer worse, not better
- Never invent an artifact. Never merge two into one
- Two artifacts, only where a pairing is listed below. Never more than two
- **Only A-28, the EMI calculator, is interactive.** Everything else is display-only

## The index

### Understand my shop

| ID | Artifact | Use when | Source |
|---|---|---|---|
| A-01 | Income this month | How did my shop do this month | QR settlement, SMS |
| A-02 | Yesterday's takings | What came in yesterday | QR settlement, SMS |
| A-03 | Money out | Where did my money go | Account Aggregator, SMS |
| A-04 | Recurring debits | What else is being cut · what am I paying everywhere | Account Aggregator, SMS |
| A-05 | Where it came from | Total across all my QRs | QR settlement |
| A-06 | Month comparison | Compared to last month | QR settlement, SMS |
| A-07 | Sales by week | When was I busiest | QR settlement, SMS |
| A-08 | Sales by day | Which day is my best | QR settlement, SMS |
| A-09 | The year | Compared to last year · why is business slow | QR settlement, SMS |
| A-10 | When money lands | When does my QR money land | QR settlement |
| A-11 | Margin card | Am I actually making money | **No source — needs supplier data** |

### Plan the season

| ID | Artifact | Use when | Source |
|---|---|---|---|
| A-12 | Festival list | When is the next festival | Season calendar |
| A-13 | Stock plan | How much should I stock | Season calendar |

### Track my loans

| ID | Artifact | Use when | Source |
|---|---|---|---|
| A-14 | Loan card | When is my EMI · how much do I owe · payments left · when does this loan end · did my EMI go through | InPrime records |
| A-15 | All my loans | List every loan in my name | Credit bureau |
| A-16 | Loan details | Tell me about this loan | InPrime records |
| A-17 | EMI due this month | What am I paying every month | InPrime records |
| A-18 | Total owed | What is my total debt | InPrime + Credit bureau |
| A-19 | Repayment schedule | Show my repayment schedule | InPrime records — **the only table permitted anywhere** |
| A-20 | Payment calendar | When is everything due · when do I pay my supplier | InPrime records + customer-told (supplier date has no source) |
| A-21 | Document list | Where is my agreement · I need a statement or NOC | InPrime records |
| A-22 | Document check | Are my papers right | DigiLocker, InPrime records |

### Pay less, pay smarter

| ID | Artifact | Use when | Source |
|---|---|---|---|
| A-23 | Rate list | Which loan is most expensive · which should I clear first · am I overcharged | InPrime + Credit bureau |
| A-24 | Interest over the term | What will these loans cost in total | InPrime + Credit bureau |
| A-25 | Interest split | What has this loan cost me | InPrime records |
| A-26 | Closing amount | What to close it today | InPrime records |
| A-27 | Savings estimate | Can I move a loan somewhere cheaper | InPrime + Credit bureau |
| A-28 | **Calculator** — the only interactive artifact | What would my EMI be · what if I pay extra · how much can I borrow | InPrime records |

### Borrow more

| ID | Artifact | Use when | Source |
|---|---|---|---|
| A-29 | Eligibility card | How much loan can I get · top-up · remaining limit | InPrime records |
| A-30 | Options list | Where will I find that money · business is down · can I restructure | InPrime + Credit bureau |
| A-31 | Application tracker | Where is my application | InPrime records |
| A-32 | Checklist | What is pending from me · what documents do I need | InPrime records |
| A-33 | Scheme list | Schemes I qualify for · cheaper government loan | **No source — gap, see `sources.md`** |

### Understand my credit score

| ID | Artifact | Use when | Source |
|---|---|---|---|
| A-34 | Score meter | What is my score · is that good or bad | Credit bureau |
| A-35 | Score change | Why did it drop | Credit bureau |
| A-36 | Helping / hurting | What is hurting my score | Credit bureau |
| A-37 | Band ladder | What score do I need · what would the next band get me | Credit bureau |
| A-38 | Score line | Has my score improved | Credit bureau — **only after three checks** |
| A-39 | Report summary | Show my full report | Credit bureau |
| A-40 | Enquiry list | Who checked my credit | Credit bureau |

### Stay safe and on time

| ID | Artifact | Use when | Source |
|---|---|---|---|
| A-41 | Single transaction | What is this charge · why was extra money cut · an unknown debit | Account Aggregator, SMS |
| A-42 | Bounce risk | Will my EMI bounce | InPrime + Account Aggregator |
| A-43 | Fraud result | Is this message real | The message itself — not a customer data source |
| A-44 | Reminder strip | Pinned, not asked for | Whatever source holds the date being reminded |

### Get help

| ID | Artifact | Use when | Source |
|---|---|---|---|
| A-45 | Request card | Where is my request · where is my dispute · change my address or number | InPrime records |
| A-46 | Cover card | Do I have insurance · am I covered for hospital | **No source — gap, see `sources.md`** |
| A-47 | Callback card | I want to talk to someone | None — routes to a person |

### Before and while the assistant works

System states, not use-case artifacts. All four are drawn from `connector.md`'s stop conditions.

| ID | Artifact | Shown when |
|---|---|---|
| A-48 | Consent card | Before any connector is read |
| A-49 | Working on it | Any fetch over two seconds |
| A-50 | Could not do it | Any failure |
| A-51 | Nothing to show yet | Any empty state |

### G1 · Income and cashflow

| ID | Artifact | Use when | Source | State drawn |
|---|---|---|---|---|
| A-52 | Income card | How did my shop do yesterday / this week / this month | Account Aggregator | Full · three periods |
| A-53 | Planned outflow | What do I have to pay this month · what is due this week | Account Aggregator + InPrime | Full · certain and estimated separated |
| A-54 | Top payers | Who pays me the most | Account Aggregator | Full · unnamed handles are the norm |
| A-55 | Top payees | Who do I pay the most | Account Aggregator | Full |

### G2 · Bank statement

| ID | Artifact | Use when | Source |
|---|---|---|---|
| A-56 | Account balance | What is my balance right now | Account Aggregator |
| A-57 | Recent transactions | What came in and went out recently | Account Aggregator |
| A-58 | Bank charges | What has the bank charged me | Account Aggregator |
| A-59 | Credit and debit summary | How much came in versus went out — day, week, month | Account Aggregator |
| A-60 | Business transactions | How many payments moved through the account | Account Aggregator |
| A-61 | Supplier payments | How much did I pay my suppliers | Account Aggregator |
| A-62 | Average balance trend | Is my balance growing or shrinking | Account Aggregator — 6 months |
| A-63 | Interest earned | How much interest did the bank pay me | Account Aggregator |
| A-64 | Full bank statement | Show me the whole statement | Account Aggregator — whole-screen view, not in-thread |

### G3 · Bureau alerts

**Not answers to a question — these are pushed when bureau data changes**, not chosen by the picker
in response to an ask. Each needs a detection timestamp; the bureau lags up to 45 days.

| ID | Artifact | Fires when | Source |
|---|---|---|---|
| A-65 | New loan detected | A loan appears that the customer did not expect | Credit bureau |
| A-66 | Overdue detected | A loan on the bureau shows overdue | Credit bureau |
| A-67 | Payment marked | A payment is recorded | Credit bureau |
| A-68 | Loan closed | A loan closes | Credit bureau |

### G4 · Bureau and score

| ID | Artifact | Use when | Source |
|---|---|---|---|
| A-69 | Score improvement plan | What should I do to improve my score | Credit bureau — **direction and words, never invented points** |
| A-70 | Score factor video | Why does this affect my score | Editorial content library |

### G5 · Existing InPrime loan

| ID | Artifact | Use when | Source |
|---|---|---|---|
| A-71 | Relationship manager | Who do I contact about my loan | InPrime |
| A-72 | Application status | Where is my loan application | InPrime |
| A-73 | Next repayment | When is my next EMI, how will it be paid | InPrime — mode stated (NACH or BBPS) |
| A-74 | Last repayment | Did my last EMI go through, how | InPrime |
| A-75 | Loan overdue | Is my InPrime loan overdue | InPrime |

### G6 · InPrime products

| ID | Artifact | Use when | Source |
|---|---|---|---|
| A-76 | Product list | What loans does InPrime offer | InPrime |
| A-77 | Apply entry point | How do I apply | InPrime — single action, hands off to inprime.in/apply-loan |

## Components — patterns, not artifacts

The picker never selects these directly. Code composes them inside whichever artifact calls for
them.

`C-01` Up/down pill · `C-02` Split bar · `C-03` Stat pair · `C-04` Payment squares ·
`C-05` Collapsed row · `C-06` Progress bar · `C-07` Change before/after · `C-08` Status pill ·
`C-09` Green callout · `C-10` Blue callout · `C-11` Amber callout — weigh · `C-12` Amber callout — fix ·
`C-13` Red callout · `C-14` Main button · `C-15` Reminder button · `C-16` Connect prompt ·
`C-17` Share and download · `C-18` Follow-up questions

## The two-artifact pairs

| Question | First | Second |
|---|---|---|
| Which should I clear first | A-23 Rate list | Amber weigh callout |
| Why did my score drop | A-35 Score change | Amber fix callout |
| When was I busiest | Stat pair | A-07 Sales by week |
| Am I being overcharged | A-23 Rate list | A-27 Savings estimate |
| Business is down | A-30 Options list | A-47 Callback card |
| Am I covered for hospital | A-46 Cover card | A-33 Scheme list, if there is a gap |

## Return none for

- Does checking my score lower it
- Is this free, how do you earn
- Why do you need my PAN or my SMS
- Is my data safe
- Who are you, are you a person
- What is a credit score · how does interest work · do I need GST
- Can I skip a month · will someone come to my shop
- Why was I rejected
- Anything the guardrail let through as borderline

## Two open items

1. **A-33 and A-46 have no source.** Until `sources.md`'s gaps are closed, the picker can name them,
   but the connector will always report them as not connected
2. **A-65–68 are alerts, not question-driven picks.** They need their own trigger path outside the
   `intent → connector → picker` chain this file otherwise describes. Do not force them through the
   normal flow while drafting `story.md`
