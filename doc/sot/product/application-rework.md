# Application Rework

Canonical for product intent, role behavior, screens, rework ownership, editable scope, business rules, acceptance criteria, and open questions for **Application Rework** across loan products.

Owner: Arnav  
Status: draft  
Last updated: 2026-06-29

## Source Links

| Source | Link/path | Notes |
| --- | --- | --- |
| Rework notes from Arnav | Current Codex thread, 2026-06-23 | Priority source for this draft. |
| Rework screenshots | Current Codex thread, 2026-06-23 | NOVA Credit Queue/My Tasks, application review tabs, Rework tab, submit confirmation, mobile Application Assessment/Rework Summary/Application Stages. |
| All Loan Files product doc | `all-loan-files-case-queue.md` | Parent queue and lifecycle context. |
| Application Rework flow doc | `../flows/application-rework.md` | End-to-end sequencing and handoffs. |
| Application Rework runbook | `../runbooks/application-rework-handling.md` | Operational handling checklist. |
| New Loan Application - Super/Welcome | `new-loan-application-super-welcome.md` | Example downstream loan stage order. |

## Scope

This document covers the **Application Rework** feature for loan applications where credit, PD, or review users need RO/AM/PD users to correct or add application details before the loan can proceed.

The feature is applicable across loan types wherever the same application review and correction pattern is used.

Out of scope:

- Detailed API implementation.
- Provider-specific verification behavior.
- Credit policy decisioning logic.
- Full NOVA technical implementation.
- Raw customer PII, raw screenshots, or real production identifiers.

## Summary

Application Rework allows a reviewer to send a loan application back to the correct field/app owner for correction. The rework request specifies what needs to be changed, who should handle it, the reason, and the reviewer remark. The assigned owner sees the case as **Rework** in the staff app, opens the rework summary, corrects the requested stage, and resubmits the case for review. For **Occupation & Income Assessment**, the owner is AM/PD, not generic staff or RO.

Rework prevents the file from being rejected only because a correctable item is missing or wrong. It also prevents uncontrolled edits by making only the relevant application stage actionable. Rework is not allowed for Top-Up and Repeat.

## Business Objective

- Allow correctable application issues to be fixed without restarting the loan application.
- Give credit and review teams a structured way to request missing or corrected information.
- Give the assigned RO/AM/PD owner clear visibility into which stage needs correction and why.
- Preserve audit trail of who requested rework, who completed it, and what remark was given.
- Return the file to credit review after correction so decisioning can continue.

## Actors And Responsibilities

| Actor | Responsibility |
| --- | --- |
| RO | Creates the application and completes field/customer steps. Handles rework assigned back to RO where applicable, but does not own Occupation & Income Assessment. |
| AM | Can do PD himself or assign PD to another eligible person. May handle rework if assigned. |
| PD person | Reviews/edits permitted application stages during PD and completes occupation and income assessment. May receive rework. |
| Credit Analyst / Level 0 reviewer | Uses NOVA to accept/assign case, check every detail, edit permitted fields where edit icon is available, and send items for rework when correction is needed. |
| Credit Manager / Level 1 reviewer | Performs final checks after Level 0 and approves the loan for offer generation where eligible. |
| Operations / Opex | Handles ready-for-disbursement and disbursement steps after credit approval and final customer steps. |
| System | Shows queues, controls edit access, records rework status, routes file between staff app and NOVA, and stores audit trail. |

## Where Rework Fits In The Loan Journey

1. RO fills the loan application up to **Occupation Profiling**.
2. Application moves to PD.
3. AM either performs PD himself or assigns the case to a PD person.
4. PD person can make required changes in permitted stages from **Loan Requirement** to **Occupation Profiling**.
5. AM/PD person completes **Occupation & Income Assessment**.
6. AM/PD person runs/checks BRE and submits the case for credit review.
7. Credit team opens the case in **NOVA**.
8. Credit review happens in Level 0 and then Level 1.
9. If correction or extra documentation is needed, the reviewer sends the file for rework.
10. The assigned owner sees the case as **Rework** in All Loan Files/staff app and fixes the requested stage. Occupation & Income Assessment rework is handled by AM/PD.
11. Rework is resubmitted and the case returns to the same credit reviewer where possible; if that reviewer is unavailable or on holiday, it can move to another reviewer.
12. After approval, credit team generates the loan offer.
13. RO contacts the customer and completes final customer-facing steps such as offer confirmation, NACH/repayment preference, agreement/e-sign, and related post-offer tasks.
14. File becomes ready for disbursement.
15. Operations handles disbursement.

## Screen Inventory

### NOVA - Credit Queue

| Element | Product behavior |
| --- | --- |
| Page | All Loan Files. |
| Role selector | Shows role such as Credit Analyst. |
| Tabs | Credit Queue, My Tasks, All Applications, Co-lending Queue. |
| Credit Queue table | Shows files waiting for credit assignment/review. |
| Table columns visible in screenshot | Application ID, Office, Applicant Name, Credit Queue Date, Application Date, Loan Amount, Loan Purpose, Loan Type. |
| Search/filter | Search and Filters controls are visible. |

### NOVA - My Tasks

| Element | Product behavior |
| --- | --- |
| My Tasks tab | Shows files assigned to the logged-in reviewer. |
| Assignment toast | Shows success message after assignment. |
| Task card | Shows application/customer summary and current review state. |
| Visible chips | Credit Assessment, Level 0. |
| Main action | View application. |
| Card fields visible in screenshot | Application date, credit queue date/aging, office, loan purpose, loan type, loan amount, assigned to, assessed by, RO name, HH obligation. |

### NOVA - Application Review

| Element | Product behavior |
| --- | --- |
| Header | Shows application/customer identifier and current label such as Backend Credit Review. |
| Review tabs | Loan Application Details, BRE Summary, Bureau Summary, Bank Statement Analysis, Income & FOIR, Other Docs, Rework. |
| Loan Application Details | Shows application, applicant, KYC, bureau, and other submitted information. |
| Edit icons | Credit reviewer can edit fields where edit icon is available. |
| Detail buttons | KYC/bureau rows can show Details actions. |
| Bureau Co-pilot | Visible assistant/action button in the review screen. Final product scope needs confirmation. |

### NOVA - Rework Tab

| Element | Product behavior |
| --- | --- |
| FOS Rework section | Lists rework items to be sent to field/staff app. |
| Credit Rework section | Lists credit-side rework items where applicable. |
| Table columns | Rework Type, To, Reason, Date & Time, Remark, Review, Action. |
| Review status | Pending while the rework item is not completed. |
| Actions | Edit and Delete before submission where permitted. |
| Submit for Rework | Sends the selected rework items to RO/AM/PD for correction. |
| Confirmation modal | Asks confirmation before submission. Visible copy: "Are you sure? You want to submit for rework? Case will be assigned to RO or AM for Rework." |

### Staff App - Application Assessment

| Element | Product behavior |
| --- | --- |
| Page | Application Assessment. |
| Tabs | My PD, CM Queue, All PD. |
| Search/filter | Search bar and filter icon visible. |
| File card | Shows application ID, customer name, mobile, created date, last updated date, RO name, PD name, branch name, product tag. |
| Rework badge | Red **Rework** badge appears when the file has pending rework. |

### Staff App - Rework Detail

| Element | Product behavior |
| --- | --- |
| Header | Shows application/customer identifier. |
| Tabs | Rework Summary and Application Stages. |
| Rework Summary | Shows PD name and rework cards. |
| Rework card | Shows rework type, reason, and status. |
| Pending status | Yellow **Pending** while not completed. |
| Success status | Green **Success** after completion/submission. |
| Application Stages | Shows loan checklist with requested stage marked **Rework Required**. |
| Backend Comment | Shown inside the target screen so the user knows what to fix. |

## Rework Types

The screenshot confirms at least:

| Rework type | Meaning |
| --- | --- |
| Income Assessment | Reviewer asks AM/PD to correct/revisit income assessment. |

There is no separate fixed rework-type taxonomy at the product level. Wherever an edit icon exists in NOVA, that option/stage can be sent for rework. The rework goes to the person responsible for the particular step.

## Business Rules

| Rule | Behavior | Status |
| --- | --- | --- |
| Rework can apply to any loan type. | The same correction pattern can be used across loan products. | Source-backed. |
| Top-Up/Repeat exception. | Rework is not allowed for Top-Up and Repeat. | Arnav validated. |
| RO completes application up to Occupation Profiling before PD. | After this, the file moves into PD/application assessment flow. | Source-backed. |
| AM can do PD or assign PD. | AM can assign someone else or himself for PD. | Source-backed. |
| PD can edit permitted pre-assessment stages. | PD can make changes from Loan Requirement to Occupation Profiling if needed. | Source-backed. |
| AM/PD owns assessment through BRE before credit review. | AM/PD completes Occupation & Income Assessment and runs/checks BRE before submitting to credit. | Source-backed. |
| Credit review is done in NOVA. | Mention only NOVA platform where required. | Source-backed. |
| Credit review has Level 0 and Level 1. | Level 0 checks every detail and can edit/send rework; Level 1 performs final checks and approves the loan for offer generation. | Arnav validated. |
| Credit can edit where edit icon exists. | Fields with edit icon can be modified during review. | Screenshot-backed. |
| Credit can send rework for missing/extra documents or corrections. | Wherever edit icon exists in NOVA, that option can be sent for rework. Rework is assigned to RO/AM based on who owns the step. | Arnav validated. |
| Assigned owner sees Rework in staff app. | Case appears with Rework badge and Rework Summary/Application Stages. Occupation & Income Assessment rework is AM/PD-owned. | Screenshot-backed. |
| Rework request highlights the target stage. | Requested stage shows Rework Required in Application Stages. | Screenshot-backed. |
| Backend comment must be visible on target screen. | User sees reviewer comment before making correction. | Screenshot-backed. |
| Rework status changes after completion. | Rework Summary changes from Pending to Success after completion. | Screenshot-backed. |
| Credit generates offer after successful review. | RO contacts the customer and completes NACH/repayment/agreement steps afterward. | Source-backed. |
| Operations owns final disbursement activity. | After Ready for Disbursement, operations performs its work. | Source-backed. |

## Editable Scope

| Stage / area | Who can change | Current understanding |
| --- | --- | --- |
| Loan Requirement | AM/PD during PD or rework | AM/PD can edit only the particular option allotted for rework, nothing else. |
| Residence/Family/Bank/Occupation stages | AM/PD where rework targets the stage | AM/PD can edit the assigned rework step only. |
| Occupation Profiling | AM/PD | AM/PD can edit till Occupation Profiling steps that were done by RO when assigned. |
| Occupation & Income Assessment | AM/PD | Confirmed rework type from screenshot; not owned by RO/generic staff. |
| Submitted fields in NOVA | Credit reviewer | Editable where edit icon is present. |
| Post-offer NACH/agreement/disbursement | RO/Operations depending on step | Rework rules after offer need confirmation. |

## Acceptance Criteria

- Credit user can view unassigned cases in NOVA Credit Queue.
- Credit user can assign a case to self and see it in My Tasks.
- NOVA My Tasks shows review level, loan type, amount, office, assigned user, assessed by, RO name, and HH obligation where available.
- Credit user can open View Application and inspect Loan Application Details, BRE Summary, Bureau Summary, Bank Statement Analysis, Income & FOIR, Other Docs, and Rework.
- Credit user can edit only fields where edit action is available.
- Credit user can create one or more rework items with rework type, assignee, reason, remark, and review status.
- Submit for Rework shows confirmation before assigning the case to RO/AM.
- Staff app shows Rework badge on affected application cards.
- Rework Summary shows each requested rework item and its Pending/Success status.
- Application Stages highlights the exact stage requiring rework.
- Target screen shows Backend Comment before the user edits.
- After correction and continue/submit, the rework item changes to Success.
- After all required rework is completed, the case returns to credit review.
- Rework audit trail captures requester, assignee, reason, remark, status, timestamp, and completion actor.

## Mismatches / Gaps

| Issue | Impact | Status |
| --- | --- | --- |
| Earlier doc treated rework as a separate type list. | Product and QA may look for a fixed list that does not exist. | Updated: edit-icon options in NOVA can be sent for rework. |
| Exact role permissions for RO vs AM vs PD rework were unclear. | Could expose or hide correction actions incorrectly. | Updated: rework goes to responsible owner for that step; user can edit only assigned option. |
| Level 0 and Level 1 decision rights were under-specified. | Credit workflow may be under-specified. | Updated with Level 0 and Level 1 responsibilities. |
| Exact status mapping between NOVA and staff app is unknown. | Engineering and product docs need shared lifecycle names. | Open |
| Whether rework can happen after offer generation is unclear. | Post-offer correction behavior needs rule clarity. | Open |

## Open Questions

| Question | Owner | Needed from | Status |
| --- | --- | --- | --- |
| What is the complete list of rework types available to credit analyst/manager? | Arnav | Credit/product | Resolved: no separate type list; wherever edit icon exists in NOVA, that option can be sent for rework. |
| Which rework types can be assigned to RO, AM, PD, or credit? | Arnav + Dileepan | Product/credit/engineering | Resolved at product level: rework is assigned to RO/AM based on who was responsible for that step. |
| What exact stages can PD edit before credit review? | Arnav | Product/credit | Resolved: AM/PD can edit till Occupation Profiling steps done by RO, and during rework only the particular allotted option. |
| What are the exact Level 0 and Level 1 responsibilities and decision rights? | Arnav | Credit | Resolved: Level 0 checks details and can rework/edit; Level 1 final-checks and approves for offer generation. |
| What are the final rework statuses: Pending, Success, Rejected, Closed, or others? | Arnav + Dileepan | Product/engineering | Open |
| Can multiple rework items be open at the same time for one application? | Arnav + Dileepan | Product/engineering | Resolved: yes. |
| What happens if RO/AM disagrees with a credit rework remark? | Arnav | Product/operations | Resolved at product level: loan remains pending; disagreement is not expected in normal operations. |
| What SLA should apply to rework completion and credit re-review? | Arnav | Operations/business | Open |
