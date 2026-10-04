# scenarios.md

Worked customer situations that define what "personalised" means. Each scenario is a reference case for the chain and a test case for the evaluation set. Look up one scenario at a time. Never load the whole file.

## Rules these scenarios follow

| Rule | What it means in every scenario |
|---|---|
| Every user is on the free experience. | There is no paid plan and no usage allowance. |
| Intelligent cards are the central cards shown when the user lands on the app. They show facts that are due or have changed. | On landing, show only an upcoming or overdue EMI, the monthly report card, the most important bureau changes each month, or a reminder the user set. A thin strip shows anything overdue until it is resolved. |
| Three next nudges sit above the chat box, generated fresh on landing and after every answer. | Every scenario lists exactly three next nudges. Whenever advice would be relevant, one nudge invites the user to ask for it. |
| Answers are useful and comprehensive, yet simple and concise, with the cards that help, or none. | An answer may use headings, lists or a table, and more than one card. |
| Their data or general knowledge, always clear which. | Every answer says which parts come from the user's own data, with the date it was read, and which parts are general knowledge, with the source. |
| The assistant does not volunteer advice. | Intelligent cards state facts. Advice is given when the user asks. |
| The assistant recommends actions for the user's own money and business, and never strongly recommends another institution. | The assistant may say "clear the overdue first". It never says "take a loan from this lender". |
| Replies are text and cards only. | Voice input is converted to text and shown back before sending. |


---

## S1 · Nothing connected

| Field | Details |
|---|---|
| Customer situation | New user. Runs a kirana shop. Has just finished onboarding. |
| Language and script | Kannada, in Kannada script |
| Known financial facts and their sources | Name, occupation and shop name, from onboarding<br>No financial facts |
| Connected, declined and unavailable sources | Connected: none<br>Declined: none |
| Free or paid plan | Free |
| Recent conversation or action | None |
| What appears when the app opens | Greeting with the user's name<br>No intelligent card, because nothing is due or has changed<br>No numbers |
| Next nudges | What is my credit score?<br>How did my shop do this month?<br>Is this loan offer genuine? |
| What the customer asks | "What is my credit score?" |
| What the answer says and which card appears | Says the score can be fetched with one-time permission, and what the user will see: score, band, every loan in their name, who checked their credit.<br>Card: credit bureau connect sheet. Why first, then what it unlocks. Connect and Not now with equal weight. |
| Follow-ups offered | Why do you need my PAN?<br>Does checking lower my score?<br>What is a good credit score? |
| What must not be shown or claimed | An estimated score<br>Any figure<br>A request for PAN before consent |
| If data is missing, stale or the request fails | User taps Not now: explain what a credit score is as general knowledge, no card, and do not ask again in this chat.<br>Bureau not responding: say nothing was charged, retry, and message when the score is ready. |
| Why this is useful | A first answer in under a minute, and the user sees exactly what connecting unlocks before giving anything. |

---

## S2 · EMI approaching

| Field | Details |
|---|---|
| Customer situation | Existing InPrime customer. EMI of ₹12,450 due in 3 days. Auto-pay is on. |
| Language and script | Hindi, in Devanagari script |
| Known financial facts and their sources | EMI amount, due date and auto-pay status, from InPrime loan records, read today at 07:10<br>Balance of ₹18,240 in the Canara account, from Account Aggregator, read yesterday |
| Connected, declined and unavailable sources | Connected: InPrime loan records, credit bureau, Account Aggregator<br>Declined: SMS |
| Free or paid plan | Free |
| Recent conversation or action | Asked about income last week |
| What appears when the app opens | Intelligent card: Next EMI. ₹12,450 on 5 September, "Auto-pay is on. Nothing for you to do."<br>No strip, because nothing is overdue or uncovered. |
| Next nudges | Will my balance cover it?<br>How did my shop do this month?<br>Show my repayment schedule |
| What the customer asks | "Will my balance cover it?" |
| What the answer says and which card appears | Says yes: ₹18,240 was in the Canara account yesterday, more than the ₹12,450 EMI. Names the source and when it was read.<br>Cards: Balance card, then Next repayment. |
| Follow-ups offered | What else is due this month?<br>Remind me a day before<br>Is auto-pay on? |
| What must not be shown or claimed | "Don't worry"<br>A promise that the debit will succeed<br>Any figure the model wrote |
| If data is missing, stale or the request fails | Balance older than two days: show its date and say it may have changed.<br>Auto-pay status unknown: say so and offer Remind me.<br>Auto-pay is off: the intelligent card becomes "EMI due, not covered" with Remind me and Pay now. |
| Why this is useful | The one worry of the week is answered before it becomes a bounce. |

---

## S3 · Overdue

| Field | Details |
|---|---|
| Customer situation | Two loans overdue: InPrime gold loan ₹8,730, 12 days late, and a Bajaj loan with ₹12,450 reported overdue |
| Language and script | English with Hindi words, in Latin script |
| Known financial facts and their sources | InPrime overdue, from InPrime loan records, read today<br>Bajaj overdue, from the credit bureau report dated 24 July |
| Connected, declined and unavailable sources | Connected: InPrime loan records, credit bureau<br>Not connected: Account Aggregator, SMS |
| Free or paid plan | Free |
| Recent conversation or action | Ignored an EMI reminder 12 days ago |
| What appears when the app opens | Strip: "2 loans overdue, ₹21,180, oldest is 12 days late".<br>Intelligent card: the InPrime overdue. |
| Next nudges | What should I pay first?<br>What does this do to my score?<br>Show my RO's details |
| What the customer asks | Taps the strip |
| What the answer says and which card appears | Two payments are late. Ours is ₹8,730, 12 days late. Bajaj shows ₹12,450 overdue on the credit report dated 24 July.<br>Recommends the action: clear the overdue amounts as soon as possible, because missed payments are reported to the bureau.<br>Cards: InPrime loan overdue, with Pay after confirming the amount. Overdue detected for Bajaj, with no Pay button. |
| Follow-ups offered | Pay the InPrime amount<br>I already paid Bajaj<br>Show my RO's details |
| What must not be shown or claimed | A threat, legal action or recovery language<br>A claim that the Bajaj loan is still unpaid today<br>A point figure for the score effect<br>A Pay button on the Bajaj loan. The app takes payment only for InPrime loans. |
| If data is missing, stale or the request fails | Payment fails: no double charge, offer retry.<br>"I already paid Bajaj": say the bureau can take up to 45 days to update, and remember what the user told us.<br>The user mentions hardship: show the RO's details with the option to call, and the human escalation path. |
| Why this is useful | One calm view of what is late and the single action to take. |

---

## S4 · Disputed bureau entry

| Field | Details |
|---|---|
| Customer situation | The monthly bureau refresh shows a new ₹50,000 personal loan the user says they never took. |
| Language and script | Kannada, in Kannada script |
| Known financial facts and their sources | New account, lender, date opened and amount, from this month's credit bureau report dated 2 August |
| Connected, declined and unavailable sources | Connected: credit bureau, SMS |
| Free or paid plan | Free |
| Recent conversation or action | Received the monthly bureau update notification and opened the app from it |
| What appears when the app opens | Intelligent card: Monthly Bureau Update, with "New loan in your name" as the most important change. |
| Next nudges | This loan is not mine<br>Who checked my credit?<br>Show my loans and cards |
| What the customer asks | "I never took this loan" |
| What the answer says and which card appears | Takes it seriously. Says the report shows this loan opened on 14 July, and that we cannot confirm fraud from here.<br>Explains how to dispute it directly with the credit bureau and with the lender, as general knowledge with the source cited.<br>Card: New loan detected. |
| Follow-ups offered | How do I raise a dispute?<br>Will this affect my score?<br>Talk to a person |
| What must not be shown or claimed | That it is fraud, or that it is not fraud<br>A promise that it will be removed<br>A point figure for the score effect<br>That the app will raise the dispute. The app explains how to dispute; it does not raise or track a dispute. |
| If data is missing, stale or the request fails | Lender name missing on the report: say so.<br>The user is an InPrime customer: offer their RO's details as well. |
| Why this is useful | A frightening discovery gets a calm, correct next step instead of silence. |

---

## S5 · Incomplete bank history

| Field | Details |
|---|---|
| Customer situation | Has two bank accounts. Only one is linked. 22 days of data. |
| Language and script | Hindi, in Devanagari script |
| Known financial facts and their sources | Credits and debits from 9 to 30 September, from Account Aggregator, for the SBI account only<br>The second account is at a cooperative bank that is not on Account Aggregator |
| Connected, declined and unavailable sources | Connected: Account Aggregator (one of two accounts)<br>Declined: SMS<br>Unavailable: the cooperative bank account |
| Free or paid plan | Free |
| Recent conversation or action | Linked the bank 22 days ago |
| What appears when the app opens | No intelligent card, because the month's report card needs a complete month. |
| Next nudges | How did my shop do this month?<br>Where did my money go?<br>Connect my other bank |
| What the customer asks | "How did my shop do this month?" |
| What the answer says and which card appears | From 9 to 30 September, ₹64,300 came into the SBI account. Says plainly that the other bank and cash sales are not included.<br>Card: In and out totals, labelled "1 of 2 accounts", with the dates covered and no comparison with last month. |
| Follow-ups offered | Connect my other bank<br>Where did my money go?<br>When was I busiest? |
| What must not be shown or claimed | A figure for the full month<br>A comparison with last month<br>"Good month" or "bad month" |
| If data is missing, stale or the request fails | Fewer than seven days of data: answer in text with the dates covered.<br>Other bank not on Account Aggregator: say so; it cannot be linked.<br>Account Aggregator down: last data with its date. |
| Why this is useful | A real number the user can trust, with the gaps stated plainly. |

---

## S6 · Declined permission

| Field | Details |
|---|---|
| Customer situation | Declined Account Aggregator and SMS earlier in this chat. Credit bureau is connected. |
| Language and script | English, in Latin script |
| Known financial facts and their sources | Three loans and their EMIs, from the credit bureau report dated 24 July<br>InPrime EMI, from InPrime loan records |
| Connected, declined and unavailable sources | Connected: credit bureau, InPrime loan records<br>Declined: Account Aggregator, SMS |
| Free or paid plan | Free |
| Recent conversation or action | Tapped Not now on the bank connect sheet five minutes ago |
| What appears when the app opens | Unchanged |
| Next nudges | How much am I paying every month?<br>What is an Account Aggregator?<br>What can InPrime see about me? |
| What the customer asks | "Where did my money go this month?" |
| What the answer says and which card appears | Says spending cannot be seen without the bank. Gives what can be seen: loans take ₹15,180 a month.<br>Card: All my loans. No connect sheet. |
| Follow-ups offered | What will these loans cost me in total?<br>How do I connect my bank later?<br>When is my next EMI? |
| What must not be shown or claimed | The connect sheet again in this chat<br>An estimate of spending<br>Anything that makes the user feel wrong for declining |
| If data is missing, stale or the request fails | Asked again in a new chat: the connect sheet may be offered once. |
| Why this is useful | Declining is not a dead end. The user still gets something true and useful. |

---

## S7 · Business knowledge question

| Field | Details |
|---|---|
| Customer situation | Runs a medical shop. Has heard that UPI payments will start costing money. |
| Language and script | Hindi and English mixed, in Latin script |
| Known financial facts and their sources | Income through QR, from SMS settlement messages |
| Connected, declined and unavailable sources | Connected: SMS |
| Free or paid plan | Free |
| Recent conversation or action | None |
| What appears when the app opens | Intelligent card: monthly report card, if a complete month exists |
| Next nudges | How did my shop do this month?<br>Where does my money come from?<br>Is this loan offer genuine? |
| What the customer asks | "Will I pay charges on UPI payments now?" |
| What the answer says and which card appears | Explains the merchant discount rate rules as general knowledge: what is charged, on which payments, the cap, the exemption, and the date it applies from. Cites the source.<br>Says clearly this is general knowledge, not a calculation from their own payments.<br>No card. |
| Follow-ups offered | How does this affect my shop?<br>Where does my money come from?<br>Share this with another shopkeeper |
| What must not be shown or claimed | A figure for what this shop will pay. MDR is answered only as general knowledge, never calculated from the shop's own payments.<br>Advice to refuse a payment method |
| If data is missing, stale or the request fails | The rule may have changed: say when the source was last reviewed. |
| Why this is useful | A worrying rumour is answered correctly and simply, from a named source. |

---

## S8 · Document check

| Field | Details |
|---|---|
| Customer situation | Received a loan offer by WhatsApp asking for a ₹1,999 processing fee before release |
| Language and script | Kannada, in Kannada script |
| Known financial facts and their sources | None needed |
| Connected, declined and unavailable sources | Connected: none |
| Free or paid plan | Free |
| Recent conversation or action | Chose the dedicated Document Check option |
| What appears when the app opens | Greeting. No intelligent card. |
| Next nudges | Is this loan offer genuine?<br>Explain a letter to me<br>How do I spot a fake loan offer? |
| What the customer asks | Sends a photo of the offer: "Is this genuine?" |
| What the answer says and which card appears | Gives a verdict with reasons, from general knowledge: genuine lenders do not ask for a fee before a loan is paid out, and the sender is not a registered lender's official number.<br>States that this is not an InPrime letter.<br>Card: Document Check result. |
| Follow-ups offered | What should I do now?<br>How do I report this?<br>Check another document |
| What must not be shown or claimed | A certain verdict when the evidence is unclear<br>The user's personal details read from the document, repeated back without need |
| If data is missing, stale or the request fails | Photo blurry or cut off: ask for a retake.<br>Cannot decide: verdict "not sure", with reasons, and offer a person.<br>File over 10 MB or locked: ask for another file. |
| Why this is useful | Protection from the most common fraud aimed at small shopkeepers, in one photo. |

---

## S9 · Service request

| Field | Details |
|---|---|
| Customer situation | Existing InPrime customer has a new mobile number |
| Language and script | English, in Latin script |
| Known financial facts and their sources | Current mobile number and loan, from InPrime loan records |
| Connected, declined and unavailable sources | Connected: InPrime loan records |
| Free or paid plan | Free |
| Recent conversation or action | None |
| What appears when the app opens | Intelligent card: Next EMI, if one is due within seven days |
| Next nudges | When is my next EMI?<br>Update my details<br>Show my loan details |
| What the customer asks | "I want to change my mobile number" |
| What the answer says and which card appears | Reads the request back: change mobile number from the current number to the new number. Asks the user to confirm.<br>After confirmation, raises the service request and shares the reference.<br>Card: Service request. |
| Follow-ups offered | What is the status of my request?<br>Show my loan details<br>Who is my RO? |
| What must not be shown or claimed | That the change is already done<br>A date for completion that the servicing system has not given |
| If data is missing, stale or the request fails | Servicing system down: say the request could not be raised and offer to try again.<br>Status changes later: notify the user. What happens after the request is raised is handled outside the app. |
| Why this is useful | A change that used to need a branch visit or a call is raised in one message. |

---

## S10 · Sharing with another shopkeeper

| Field | Details |
|---|---|
| Customer situation | Runs a textile shop. Liked the festival calendar and wants a poster for a Diwali sale. |
| Language and script | Kannada, in Kannada script |
| Known financial facts and their sources | Shop name and trade, from onboarding |
| Connected, declined and unavailable sources | Connected: SMS |
| Free or paid plan | Free |
| Recent conversation or action | Asked "When is the next festival?" |
| What appears when the app opens | Unchanged |
| Next nudges | Make a poster for my shop<br>Share the festival calendar<br>How much should I stock? |
| What the customer asks | "Make a Diwali sale poster for my shop" |
| What the answer says and which card appears | Creates a poster with the shop name and the festival, in the user's language.<br>Card: Shareable card and shop poster, with Share on WhatsApp and Save image. |
| Follow-ups offered | Make another poster<br>Share the festival calendar<br>How do I get more customers? |
| What must not be shown or claimed | Any amount or personal detail on the poster unless the user opts in |
| If data is missing, stale or the request fails | No shop name: ask for it first. |
| Why this is useful | A reason to show the app to the shop next door. Every share carries the app identity and an install link, and the install is attributed to the sharer. |
