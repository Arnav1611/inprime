# InPrime artifact design — prompts

**How to run this.** Do not ask for all 31 artifacts in one message. You will get 31 shallow cards. Run the **preamble** plus **one group** per conversation, with the design file attached each time. Six runs.

---

## PREAMBLE — paste this first, every time

```
You are designing display artifacts for the InPrime assistant, a conversational app
for Indian shopkeepers. Artifacts are visual blocks that appear inside a chat thread,
below a one or two line answer.

VISUAL SOURCE OF TRUTH
The attached file is the design system. Extract and reuse its colours, type scale,
spacing, radii, card shell, pill, bar and callout styles exactly. Do not introduce a
new colour, font, shadow or corner radius. If something is missing, compose it from
existing tokens rather than inventing one.

WHO READS THIS
- Runs a small shop. Kirana, medical, mobile, textile, restaurant, hardware, salon, dairy
- Reads slowly. Reads English barely. Speaks Kannada, Hindi or English
- Holding the phone at a counter, one hand, customers watching
- May be using a money app for the first time
- Cares about money owed to them and money going out, more than about a score

RULES THAT GOVERN EVERY ARTIFACT
1.  Each artifact is built for one use case and carries fixed labels. Never a generic
    container reused across questions.
2.  Display only. Nothing is tappable except a single main button, and where stated,
    a row that opens a detail view.
3.  The artifact holds figures and their labels. Every explanation lives in the chat
    text above it. No explanatory sentences inside the card.
4.  Indian number grouping. Rs 1,04,200 never Rs 104,200.
5.  Labels must hold in Kannada and Hindi, which run about 40 percent longer. If a
    label only works in English, change the label. Do not shrink the type.
6.  One main button maximum. Yellow. Starts with a verb.
7.  Grey means not reported. It must never be mistaken for green.
8.  No emoji. No celebration. No exclamation marks. No urgency that a real date does
    not create.
9.  Every figure is sample data. Use realistic Indian amounts, lender names, shop names.
10. Never state or imply that credit is approved. Any pre-sanction figure is labelled
    indicative.

DATA REALITY — design only for fields that exist
- The credit bureau carries NO payment due dates at all. EMI amount is present on 27
  percent of accounts, credit limit on 2 percent, and 84 percent carry no payment
  history. Do not design a credit utilisation ring, a days-until-due counter, or a
  payment history strip for bureau loans unless the not-reported state dominates it.
- Account Aggregator coverage is thin for cooperative banks.
- Anything the sources cannot fill needs a designed state, not a blank.

FOUR STATES PER ARTIFACT — draw all four, side by side
1. Full        all data present
2. Partial     some fields missing, stated in place, never hidden
3. Not connected   what cannot be seen, what connecting unlocks, Connect and Not now
                   at equal visual weight
4. Failed      plain words, no error code, never loses what the customer typed

OUTPUT
- One self-contained HTML file. Inline CSS. No external assets.
- Phone-width frames, 360px content width, on a neutral board.
- Above each artifact, a label strip reading:
  artifact name | the question it answers | data source | state
- Group the frames under the section heading given below.
```

---

## GROUP 1 — Income and cashflow

```
Design 4 artifacts for section 1, Income and cashflow.

1. INCOME CARD — "How did my shop do yesterday / this week / this month"
   One large amount, period label, and a comparison against the previous day, week or
   month as an up or down pill. Same card serves three periods. Draw all three.
   Hide the pill entirely when there is no previous period to compare against.

2. PLANNED OUTFLOW — "What do I have to pay this month"
   Known outgo for the period ahead, largest first, each with the date it falls, and a
   total. Separate what is certain from what is estimated.

3. TOP PAYERS — "Who pays me the most"
   Name or number, amount, small bar, biggest first. Most will be unnamed UPI handles
   and phone numbers. Design for that as the normal case, not the exception.

4. TOP PAYEES — "Who do I pay the most"
   Same shape, opposite direction. Suppliers, rent, lenders.

3 and 4 share a shape but are separate artifacts with their own labels and their own
empty states.
```

---

## GROUP 2 — Bank statement

```
Design 11 artifacts for section 2, Bank statement.

1.  CURRENT BALANCE — one amount, the bank and last four digits, and when it was last
    refreshed. The refresh time matters more than it looks.
2.  RECENT TRANSACTIONS — last 8. Date, counterparty, amount, direction. A row opens a
    single transaction detail.
3.  BANK CHARGES — what the bank took and why, this period, with a total.
4.  MONEY IN VS MONEY OUT — two totals for the period and what stayed. Amounts under
    each side, never percentages.
5.  MONEY IN TREND — day on day, week on week, month on month. One artifact with a
    range switch, three ranges drawn.
6.  MONEY OUT TREND — same shape, same three ranges.
7.  BUSINESS VOLUME TREND — count and value of business transactions, same three ranges.
8.  SUPPLIER PAYMENTS — who, how much, when, this period.
9.  AVERAGE BALANCE TREND — line over months with the current average called out. This
    is the one lenders read. Say what it means in the label, not in a sentence.
10. INTEREST EARNED — a small amount, credited quarterly, very often zero.
    Design the zero state first and the populated state second.
11. FULL BANK STATEMENT — a full screen, not an in-thread artifact. Sticky period
    header, running balance, filter by in / out / charges, and a download.

5, 6 and 7 share one chart component and carry three different names.
```

---

## GROUP 3 — Bureau alerts

```
Design 4 alerts for section 3, Active loans from bureau.

These are NOT artifacts the assistant picks in answer to a question. They are pushed
when the bureau data changes. Each needs four things: what changed, when it was
detected, what it means in one line, and what to do about it.

Design one shared alert shell, then four variants.

1. NEW LOAN DETECTED — lender, amount, date opened. Must carry a "this is not mine"
   path that starts a dispute.
2. OVERDUE DETECTED — lender, amount, how long. The most sensitive one. State what is
   true, do not threaten, do not manufacture urgency.
3. PAYMENT MARKED — the only good-news variant. Do not celebrate it.
4. LOAN CLOSED — lender, closed date, and whether an NOC is available.

Severity by colour: red for overdue, blue for new and closed, green for payment marked.
Each alert says when it was detected, because bureau data lags by up to 45 days.
```

---

## GROUP 4 — Bureau and score

```
Design 3 things for section 4, Bureau and score improvement.

1. SCORE IMPROVEMENT PLAN — actions ranked by effect. Each action carries what to do,
   by when, and the expected effect.
   IMPORTANT: the bureau publishes no point values. Never show "+40 points" or any
   numeric prediction. Show direction, size in words (small, moderate, large) and
   expected timing. Design the artifact so it reads as useful without a number.

2. SCORE EXPLAINER VIDEO — how a short video sits inside a chat thread. Design the
   in-thread card: thumbnail, length, what it explains, and how it expands. Do not
   design the player.

3. FULL BUREAU REPORT — a full screen. Four summary tiles at the top, accounts below,
   closed accounts collapsed, download at the end. Reference layout:
   https://www.figma.com/design/Rkw2CcFD8Awj6o4aYW8nix/InPrime?node-id=1011-1507

Note for 3: the report must show a not-reported state on every field the bureau leaves
empty, and there are many.
```

---

## GROUP 5 — Existing InPrime loan

```
Design 8 artifacts for section 5, Existing InPrime loan.

1. RELATIONSHIP MANAGER — name, initials or photo, number, call and WhatsApp actions,
   and the hours they are available. Says what happens if they do not pick up.
2. APPLICATION STATUS — In progress, Approved, Disbursed, Rejected. One artifact, four
   states, all drawn. Rejected must say what happens next and when they can reapply,
   not just the word.
3. NEXT LOAN ELIGIBILITY — amount, rate, tenure. Clearly and visibly marked indicative,
   not a promise, not an approval.
4. ACTIVE INPRIME LOANS — stacked cards. Lender mark, outstanding, progress, EMI, start
   date. Closed loans collapsed.
5. FULL LOAN DETAILS AND REPAYMENT SCHEDULE — a full screen. Details above, then the
   schedule as 4 columns: number, date, amount, status. This is the only table permitted
   anywhere in the product.
6. NEXT REPAYMENT — amount, date, and the account NACH will debit, OR BBPS if that is
   the mode. The artifact must make clear which of the two applies, because the customer
   has to do nothing in one case and something in the other.
7. LAST REPAYMENT — amount, date, the mode it came through, and a receipt.
8. INPRIME LOAN OVERDUE — amount, days late, charges so far, and one clear way to pay
   now. Describe what is true. Do not warn, do not threaten.
```

---

## GROUP 6 — InPrime products

```
Design 2 things for section 6, InPrime products.

1. PRODUCT CARD, five variants — Super Loan, Smart Loan, Winner Loan, Champion Loan,
   Micro-LAP. Each carries who it is for, amount range, tenure, and one benefit.
   They must be comparable at a glance when stacked in a thread. Same fields in the
   same order on all five.
   No product is recommended. Nothing is marked best or popular.

2. APPLY ENTRY POINT — hands off to inprime.in/apply-loan. Says what happens next, what
   they will need, and that it leaves the app.
```

---

## Four traps in this list

| # | Trap | What to do |
|---|---|---|
| 1 | **Score predictions with numbers.** 4.1 asks for predictions. The bureau publishes no point values, and the grounding doc already forbids invented points | Direction and words, never a number. Confirm with compliance before it is built |
| 2 | **The bureau alerts are not artifacts.** They are push events with a trigger, a detection time and an action | Design them as a separate alert shell, not through the artifact picker |
| 3 | **Three trend artifacts share one chart.** 2.5, 2.6, 2.7 | One component, three names, three sets of labels. Do not merge them into a generic "trend chart" |
| 4 | **Two full screens are hiding in an artifact list.** 2.11 and 5.5, plus 4.3 | These are screens, not in-thread blocks. Brief them separately or they will come back card-sized |

## Not in this list, and probably should be

- **Chit fund or committee contributions** — very common in this segment, no source holds it, and it competes directly with EMI dates
- **Cash sales** — everything here is bank and QR. A shop taking half its money in cash will see an income card that is wrong, and will not trust anything else
- **GST filing status** — named in the survey topics, absent here
