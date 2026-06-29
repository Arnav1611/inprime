# Repeat Loan

Canonical for product intent, entry point, eligibility rules, lead visibility, loan-settlement behavior, business rules, acceptance criteria, and open questions for the Repeat Loan journey.

Owner: Arnav  
Status: draft  
Last updated: 2026-06-29

## Source Links

| Source | Link/path | Notes |
| --- | --- | --- |
| Stakeholder clarification | Arnav notes from product/credit stakeholders, 2026-06-22 | Priority source for Repeat Loan eligibility and lead behavior. |
| Top-Up/Repeat model note | User-provided attachment | Data/model context for Top-Up/Repeat universe and risk variables. |
| Product-limit screenshot | User-provided screenshot, 2026-06-29 | Confirms Repeat range Rs. 40,000 to Rs. 3 lakh. |
| Stakeholder eligibility fix note | Stakeholder clarification shared by Arnav, 2026-06-22 | OSP-below-40k-after-repayment logic was fixed after it broke tenure-percentage eligibility and pulled next-month eligible customers into the 10th Repeat cohort. |
| Top-Up Loan product doc | `top-up-loan.md` | Repeat follows a similar lead/application flow with different eligibility and settlement rules. |
| Leads product doc | `leads.md` | Repeat is currently visible under the Top-up section of Leads but marked as Repeat. |
| Product variants doc | `xpress-flow-product-variants.md` | Cross-product amount and entry-point comparison. |
| Flow doc | `../flows/repeat-loan.md` | End-to-end sequencing and handoffs. |
| Tech doc | TBD | Dileepan to map lead generation, status, APIs, settlement adjustment, and loan-account rules. |

## Scope

This document covers **Repeat Loan** for existing InPrime borrowers.

Out of scope:

- Fresh Super/Welcome Loan origination.
- Top-Up Loan details except where Repeat reuses the same flow.
- Full model-building methodology for Top-Up/Repeat risk model.
- Provider-specific documentation.
- Detailed API implementation.
- Raw customer or repayment data.

## Summary

Repeat Loan is an existing-customer loan journey similar to Top-Up. Like Top-Up, Repeat leads are created by the **program manager or credit team** and are visible to RO/AM in the **Leads** section.

Current app behavior: Repeat currently appears under the **Top-up** section of Leads, but the lead is marked/tagged as **Repeat**.

The main Repeat differences from Top-Up are:

- Repeat requires **12 calendar months** plus Rs. 40k OSP rule; otherwise 16 months standard.
- Repeat amount range is **Rs. 40,000 to Rs. 3 lakh**.
- Only **two loans** can exist for an applicant.
- If a borrower has a Super/Welcome core loan, they may take a Top-Up first.
- After the Repeat eligibility condition is met, the borrower must settle the core loan to take a Repeat Loan.
- If any OSP remains on the core loan, it can be reduced from the new Repeat Loan amount.
- Top-Up and Repeat can run simultaneously; the core loan must be settled for Repeat.
- Rework is not allowed for Repeat.

## Business Objective

- Retain good existing borrowers after sufficient repayment history.
- Offer a repeat loan to borrowers who have demonstrated at least 12 months of clean repayment behavior.
- Allow transition from old core loan to a new Repeat Loan while keeping loan-count rules controlled.
- Avoid incorrectly closing a young Top-Up loan that has not matured enough for settlement.
- Give RO/AM a clear lead to act on without creating duplicate borrower journeys.

## Users And Roles

| Role | Product role in Repeat Loan |
| --- | --- |
| Program Manager | Creates or triggers Repeat Loan lead pool. |
| Credit Team | Creates/approves Repeat lead eligibility and risk criteria. |
| RO | Views Repeat lead in Leads, contacts customer, starts application where permitted, and completes customer-facing stages. |
| AM | Views Repeat leads/files for reporting ROs and may monitor/coordinate action. |
| Existing borrower / Applicant 1 | Existing InPrime borrower eligible for Repeat based on repayment history and loan-count rule. |
| Applicant 2 / co-applicant | Reused from existing/core loan unless product confirms otherwise. |
| Credit/Backend | Reviews eligibility, bureau, obligations, OSP settlement, and final offer. |
| Operations / Opex | Handles settlement adjustment, disbursement, and loan-account closure/creation handoff. |
| System | Shows Repeat-tagged leads, validates eligibility, blocks invalid loan count, and routes statuses. |

## Entry Point

Repeat starts from **Leads**, similar to Top-Up.

Current behavior:

1. Program manager or credit team creates/identifies Repeat leads.
2. RO/AM opens Leads.
3. Repeat lead appears currently under the **Top-up** section.
4. Lead is marked/tagged as **Repeat**.
5. RO/AM reviews the lead and proceeds using the same broad actions as Top-Up, such as call customer or start application, if permitted.

Target behavior to confirm:

- Repeat may need a separate Leads tab later, or it may continue inside Top-up with a Repeat tag.

## Screen Inventory

Because Repeat works similarly to Top-Up, the expected screen sequence currently follows the Top-Up loan application checklist unless product/design confirms a separate Repeat checklist.

| Step | Screen / module | Repeat behavior |
| --- | --- | --- |
| 0 | Leads - Top-up section / Repeat tag | Repeat leads visible to RO/AM, currently inside Top-up section. |
| 1 | Applicant 1 Profile | Existing borrower profile reused/confirmed. |
| 2 | Applicant 2 Profile | Existing co-applicant reused/confirmed unless product confirms a different rule. |
| 3 | Applicant 3 Profile (Optional) | Reused/handled like Top-Up if present. |
| 4 | Household Credit-O-Meter | Reassess household credit and bureau context. |
| 5 | Loan Requirement | Capture Repeat amount, tenure, remarks, and settlement/OSP context. |
| 6 | Residence Details | Reuse/confirm/update residence if needed. |
| 7 | Bank Statement Upload | Upload/analyse current bank statement if required. |
| 8 | Occupation Profiling | Reuse/confirm/update occupation if required. |
| 9 | Occupation & Income Assessment | AM/PD reassesses current income/FOIR if required. |
| 10 | Disbursement Bank Account Details | AM/PD confirms account for disbursement. |
| 11 | Additional Documents | AM/PD captures supporting docs if required before BRE. |
| 12 | BRE / Final Decision | AM/PD runs/checks Repeat eligibility and decisioning after income assessment. |
| 13 | Loan Offer Generation | Credit team generates Repeat offer after settlement/eligibility rules. |
| 14 | NACH and Repayment Preference | RO registers/confirms repayment mode with customer. |
| 15 | Agreement E-sign | RO coordinates agreement signing. |
| 16 | Disbursement | Track disbursement and settlement adjustment. |

## Eligibility Rules

| Rule | Repeat Loan behavior | Source / confidence |
| --- | --- | --- |
| Lead generation | Repeat leads are created by program manager or credit team. | Stakeholder clarification / High |
| Lead visibility | RO/AM can see Repeat leads in Leads. | Stakeholder clarification / High |
| Current tab placement | Repeat currently appears under Top-up section of Leads and is marked as Repeat. | Stakeholder clarification / High |
| EMI seasoning | 12 calendar months plus Rs. 40k OSP rule; otherwise 16 months standard. | Arnav validation / High |
| Bounce rule | 12 months should be paid without bounce. | Stakeholder clarification / High |
| Amount | Rs. 40,000 to Rs. 3 lakh. | Latest product-limit screenshot / High |
| Max loan count | Only two loans can be there for an applicant. | Stakeholder clarification / High |
| Core loan settlement | After 12 months of core loan, borrower has to settle core loan to get Repeat. | Stakeholder clarification / High |
| Core OSP adjustment | If OSP remains in core loan, it can be reduced from new Repeat Loan amount. | Stakeholder clarification / High |
| Top-Up settlement | Top-Up and Repeat can run simultaneously; core loan must be settled for Repeat. | Arnav validation / High |
| OSP threshold / cohort timing | Customers should not enter the current Repeat cohort only because they will fall below Rs. 40,000 OSP after this month's repayment if tenure-percentage eligibility is only reached next month. | Stakeholder eligibility fix note / Medium; needs BRE rule |

## Repeat Vs Top-Up

| Area | Top-Up Loan | Repeat Loan |
| --- | --- | --- |
| Lead creation | Program/credit/system-generated existing-customer lead. | Program manager or credit team creates Repeat leads. |
| Current Leads placement | Top-up tab. | Currently under Top-up section but marked Repeat. |
| EMI requirement | Latest notes say 6 EMIs should be completed. | 12 calendar months plus Rs. 40k OSP rule; otherwise 16 months standard. |
| Amount | Rs. 40,000 to Rs. 2 lakh. | Rs. 40,000 to Rs. 3 lakh. |
| Core loan | Top-Up can be taken on existing Super/Welcome core loan. | Core loan must be settled after 12 months to create Repeat. |
| OSP handling | Current OSP affects eligibility/offer. | Remaining core loan OSP can be deducted from Repeat disbursement/amount. |
| Top-Up loan handling | Top-Up may continue as a second loan. | Top-Up cannot be settled early through Repeat if only 6 months or less. |
| Max active loans | Needs final rule with Top-Up. | Only two loans can exist for applicant. |

## Loan Count And Settlement Logic

Working interpretation from stakeholder input:

1. Applicant may have a Super/Welcome core loan.
2. Applicant may take a Top-Up on top of that core loan if eligible.
3. Only two loans can exist for one applicant.
4. Once the core loan has completed 12 months clean repayment, applicant may be eligible for Repeat.
5. To create Repeat, the core loan has to be settled.
6. If core loan OSP is pending, the pending OSP can be adjusted/reduced from the new Repeat Loan amount.
7. If the applicant also has a Top-Up loan, Top-Up and Repeat can run simultaneously; the core loan must be settled for Repeat.

This area needs credit/operations validation because it affects disbursement amount, settlement accounting, and customer communication.

## Data / Risk Signals

The Top-Up/Repeat model note says the Top-Up/Repeat universe used variables from:

- BSA-based variables for core and Top-Up/Repeat.
- Bureau-based variables for core and Top-Up/Repeat.
- Obligation-based variables for core and Top-Up/Repeat.
- Income-based variables for core loan.
- Core loan funnel and repayment variables, including loan type and EMI count.
- Drift variables from core loan to Top-Up/Repeat.

Model top features included `coreloan_noofemipaid`, bureau vintage, max DPD, current exposure, obligations, and drift variables. Product docs should not copy model formulas as policy until credit confirms which variables are live decision rules.

## Retention Eligibility Automation Note

Stakeholder feedback says the retention loan eligibility process is still manual in places. A recent fix was required because added logic to calculate which customers would have **OSP below Rs. 40,000 this month after repayment** broke the **tenure-percentage eligibility flow**. This allowed some customers who would become eligible only next month into the current **10th Repeat cohort**.

Product implication:

- Repeat and Top-Up eligibility should not depend on separate team-owned code snippets or manual cohort calculations.
- Eligibility should be automated through BRE or another single canonical decisioning layer.
- OSP threshold, repayment timing, tenure-percentage eligibility, EMI count, bounce history, and cohort month should be evaluated in one consistent rule set.
- The app/lead generation should show a customer as Repeat-eligible only when the canonical eligibility rule says they are eligible for the current cohort.

This matters because retention products are now at a larger business scale, and manual eligibility creates duplicate effort, inconsistent logic across teams, and avoidable cohort errors.

## Business Rules

| Rule | Product behavior | Status |
| --- | --- | --- |
| Repeat is existing-customer only. | Lead should be generated from existing borrower base. | Confirmed by stakeholder context. |
| Repeat lead creation is centralized. | Program manager or credit team creates Repeat leads. | Confirmed. |
| RO/AM visibility. | RO/AM can see Repeat leads. | Confirmed. |
| Current UI placement. | Repeat appears in Top-up Leads section with Repeat tag. | Confirmed current behavior. |
| EMI clean history. | 12 calendar months plus Rs. 40k OSP rule; otherwise 16 months standard. | Confirmed; exact source field needs tech validation. |
| Max loans. | Applicant cannot have more than two loans. | Confirmed; edge cases need validation. |
| Core settlement. | Core loan must be settled to create Repeat after 12 months. | Confirmed; settlement flow needs ops validation. |
| Core OSP deduction. | Remaining core loan OSP can be deducted from Repeat Loan. | Confirmed; accounting flow needs ops/tech validation. |
| Top-Up and Repeat simultaneous. | Top-Up and Repeat can run simultaneously; core loan must be settled. | Confirmed by Arnav. |
| Rework | Rework is not allowed for Repeat. | Confirmed by Arnav. |
| Eligibility automation. | Repeat/Top-Up retention eligibility should be automated through BRE or one canonical rule engine. | Recommended by stakeholder after cohort logic issue. |
| OSP-below-40k cohort rule. | Customers should not enter the current Repeat cohort only because they will fall below Rs. 40,000 OSP after this month's repayment if tenure-percentage eligibility is reached next month. | Needs final BRE/product rule. |

## Acceptance Criteria

- Program manager or credit team can identify/create Repeat leads.
- RO/AM can see Repeat leads in Leads.
- Current UI shows Repeat under the Top-up section with a clear Repeat tag.
- Repeat eligibility checks for 12 months EMI paid without bounce.
- Repeat amount outside Rs. 40,000 to Rs. 3 lakh is blocked.
- Application cannot proceed if loan-count rule would exceed two loans for the applicant.
- If core loan OSP remains, system/operations can show and adjust the OSP against the Repeat Loan amount.
- Top-Up loan is not settled through Repeat when it does not meet the required seasoning rule.
- Repeat application follows the Top-Up-style journey unless a separate Repeat checklist is confirmed.
- Rejection/ineligibility reasons are captured when Repeat cannot proceed.

## Mismatches Or Gaps

| Issue | Impact | Status |
| --- | --- | --- |
| Repeat currently appears under Top-up Leads section but is a separate product. | Staff may confuse Top-Up and Repeat unless tag is clear. | Open |
| Earlier docs only captured Repeat amount, not flow/eligibility. | Product docs were incomplete. | Resolved by this draft; needs validation. |
| Earlier note said active Top-Up should not be settled through Repeat if only 6 months old or less. Latest clarification says Top-Up and Repeat can run simultaneously while core loan must be settled. | Product docs should use latest clarification. | Updated |
| Only two loans can exist for applicant, but interaction between core, top-up, and repeat needs edge-case mapping. | System may allow invalid combinations if not clearly defined. | Open |
| OSP-below-40k logic broke tenure-percentage eligibility and pulled some next-month eligible customers into the 10th Repeat cohort. | Repeat lead generation can include customers too early if eligibility logic is split across manual/code processes. | Fixed in current logic; BRE automation recommended. |

## Open Questions

| Question | Owner | Needed from | Status |
| --- | --- | --- | --- |
| Should Repeat get its own Leads tab, or remain under Top-up with Repeat tag? | Arnav | Product/design | Open |
| What exact field/source proves 12 months EMI paid without bounce? | Dileepan | Engineering/data/credit | Open |
| Is "12 months EMI paid" equal to 12 EMIs paid, 12 calendar months, or both? | Arnav | Credit/product | Resolved: 12 calendar months. |
| What is the exact settlement formula when core loan OSP is reduced from Repeat Loan? | Arnav + Dileepan | Operations/finance/engineering | Partially resolved: 12 months + Rs. 40k OSP, otherwise 16 months standard; accounting formula needs ops/tech. |
| What final rule controls whether an active Top-Up can or cannot be settled during Repeat? | Arnav | Credit/operations | Resolved: Top-Up and Repeat can run simultaneously; core loan must be settled. |
| Can Applicant 2/3 change in Repeat, or must applicants remain same as core/Top-Up? | Arnav | Product/credit | Resolved for now: same as loan. |
| What is the canonical BRE rule for OSP below Rs. 40,000, repayment timing, tenure-percentage eligibility, and cohort inclusion? | Arnav + Dileepan | Credit/product/engineering | Partially resolved: 12 months + Rs. 40k OSP, otherwise 16 months standard; tech implementation still needed. |
| Who owns the single source of truth for retention-product eligibility until BRE automation is live? | Arnav | Product/credit/program | Resolved: credit team. |
