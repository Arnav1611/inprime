# Top-Up Loan

Canonical for product intent, screen behavior, business rules, eligibility rules, acceptance criteria, and open questions for the Top-Up Loan journey in the staff app.

Owner: Arnav  
Status: draft  
Last updated: 2026-06-29

## Source Links

| Source | Link/path | Notes |
| --- | --- | --- |
| Rough app documentation | Google Doc: https://docs.google.com/document/d/1RjWx3gUFbFS1ZXHuyM2ElMg1ltK7SCu__IaIKMfZocM/edit?usp=sharing | Priority source for base app behavior and reusable loan journey stages. |
| EMI Structure | https://docs.google.com/spreadsheets/d/1tZ-7gF1OSnc2CVlFwol-ZZqmbGkdYwDAGIuYgPFWMZs/edit#gid=0 | Source for EMI structure; exact formula not copied into this doc. |
| High Level Process Flow | https://whimsical.com/top-up-loan-high-level-RduRXASmvDYuzTsjCjUnnX | High-level Top-Up process reference. |
| Leads screenshot | User-provided screenshot | Shows Top-up tab, lead cards, and actions. Do not reproduce customer PII in docs. |
| Loan Application Steps screenshot | User-provided screenshot | Shows Top-Up step checklist with reused/completed stages. |
| Loan Requirement screenshot | User-provided screenshot | Shows loan amount, tenure, EMI plan, remarks, and core loan utilisation. |
| Product-limit screenshot | User-provided screenshot, 2026-06-29 | Confirms Top-Up range Rs. 40,000 to Rs. 2 lakh. |
| Flow doc | `../flows/top-up-loan.md` | End-to-end sequencing, handoffs, API touchpoints, and state transitions. |
| Product variants doc | `xpress-flow-product-variants.md` | Cross-product comparison and amount-limit mismatch tracking. |

## Scope

This document covers the **Top-Up Loan** product journey for existing InPrime borrowers inside the staff app.

Out of scope:

- Fresh Super/Welcome Loan application.
- SMART Loan.
- Repeat Loan.
- MLAP / Micro LAP.
- Full tech/API implementation.
- Provider-specific documentation.
- Raw EMI formulas, raw bureau payloads, or customer PII.

## Summary

Top-Up Loan is a loan journey for existing borrowers who may be eligible for an additional loan based on repayment behavior, household credit quality, income, obligations, and current exposure. The journey starts from the **Leads** module, not from fresh New Loan Application product selection.

The app shows a **Top-up** tab in Leads. Each lead card shows basic existing-customer context such as product tag, last disbursement date, number of EMIs paid, and current InPrime OSP. Staff can call the customer, reject the Top-Up lead, start the application, or get direction.

Top-Up should reuse stable existing data where valid and only recollect or reassess data that changes over time or is required for the fresh top-up decision. Rework is not allowed for Top-Up.

## Business Objective

- Allow eligible existing borrowers to receive an additional loan without repeating the entire fresh onboarding journey.
- Reduce staff effort by reusing stable customer data from the existing loan.
- Reassess changing risk and affordability signals before offer generation.
- Capture loan requirement, current utilisation of the core loan, updated obligations, FOIR, and repayment readiness.
- Keep the journey reviewable for product, credit, operations, and engineering teams.

## Users And Roles

| Role | Product role in Top-Up journey | Open questions |
| --- | --- | --- |
| RO / Staff user | Views Top-Up leads, calls customer, rejects lead, starts application, completes customer-facing stages, and captures loan requirement. | Only RO can start the Top-Up application. |
| Existing borrower / Applicant 1 | Primary existing customer for whom Top-Up is being evaluated. | Applicant 1 always remains the same as the core loan. |
| Applicant 2 / Co-borrower | Existing co-borrower from the core loan. | Applicant 2 always remains the same as the core loan; a new co-borrower cannot be added. |
| Applicant 3 | Applicant 3 from the core loan, if present. | Applicant 3 remains the same as the core loan; a new Applicant 3 cannot be added. |
| AM / PD | AM can assign the case for PD to someone else or perform PD themselves. | Same as fresh loan unless a later Top-Up-specific rule differs. |
| Credit team | Reviews FOIR, bureau, obligations, ticket size, and final approval/rejection. | FOIR cutoff validated as 50%; calculation detail belongs in credit/tech docs. |
| Operations / Opex | Handles disbursement after agreement, repayment setup, and approval. | Confirm if same as fresh loan disbursement. |

## Entry Point

Top-Up starts from **Leads**:

1. Staff opens Leads.
2. Staff selects the **Top-up** tab.
3. Staff reviews Top-Up lead cards.
4. Staff opens the three-dot menu on a lead.
5. Staff chooses one of:
   - Call Customer.
   - Reject TopUp Lead.
   - Start Application.
   - Get Direction.

Lead card visible fields from screenshot:

| Field / element | Product meaning |
| --- | --- |
| Customer photo | Existing borrower profile image. |
| Loan/account identifier | Existing customer or loan reference shown on card. |
| Customer name | Existing borrower name. |
| Product tag | Example visible tags: Welcome, Super. |
| Mobile | Customer mobile number; do not copy raw values into docs. |
| Last Disb Date | Last disbursement date of existing/core loan. |
| No. of EMI's Paid | Number of EMIs completed. |
| Current InPrime OSP | Current outstanding principal/obligation with InPrime. |
| Verified/check icon | Signifies where/how the lead was generated. |

## Screen Inventory

| Step | Screen / module | Product purpose | Top-Up behavior |
| --- | --- | --- | --- |
| 0 | Leads - Top-up tab | Find eligible existing borrower leads. | Search, filter, review lead card, call customer, reject lead, start application, get direction. |
| 1 | Applicant 1 Profile | Reuse or resume primary borrower profile. | Applicant 1 is fixed from the core loan. Existing mobile, name, photo, KYC, and address may be reused unless stale/changed. Screenshot shows Resume. |
| 2 | Applicant 2 Profile | Reuse existing first co-borrower profile from core loan. | Applicant 2 remains the same as core loan; new co-borrower cannot be added. |
| 3 | Applicant 3 Profile (Optional) | Reuse existing second co-borrower profile from core loan where present. | Applicant 3 remains same as core loan if present; new Applicant 3 cannot be added. |
| 4 | Household Credit-O-Meter | Reassess household credit. | HH score used for Open/Limited ticket eligibility. |
| 5 | Loan Requirement | Capture requested Top-Up amount, tenure, remarks, and core loan utilisation. | Amount, tenure, EMI plan, remarks, and Core Loan Utilisation are visible. |
| 6 | Residence Details | Confirm or reuse residence data. | Screenshot shows Completed - View Details; change rules need confirmation. |
| 7 | Bank Statement Upload | Upload/analyse bank statement for income evaluation. | Changing data point; likely needs fresh assessment when income/age of assessment requires it. |
| 8 | Occupation Profiling | Confirm or reuse occupation data. | Screenshot shows Completed - View Details; redo rule depends on assessment expiry or occupation change. |
| 9 | Occupation & Income Assessment | AM/PD reassesses income, FOIR, and affordability. | Required for ticket classification and offer decision. |
| 10 | Disbursement Bank Account Details | AM/PD confirms account for disbursement. | Bank data can change; bank details may need service request/update. |
| 11 | Additional Documents | AM/PD captures supporting docs if required before BRE. | Exact Top-Up mandatory docs need confirmation. |
| 12 | Business Rule Engine (BRE) / Final BRE | AM/PD runs/checks final decision rules after income assessment. | Uses repayment behavior, HH score, income, FOIR, obligations, bureau, and ticket size. |
| 13 | Loan Offer Generation | Credit team generates offer. | EMI structure and eligible amount/tenure should reflect Top-Up rules. |
| 14 | NACH and Repayment Preference | RO registers or updates repayment mode with customer. | Existing NACH automation impact needs confirmation. |
| 15 | Agreement E-sign | RO coordinates agreement signing. | Signer rules need confirmation. |
| 16 | Disbursement | Track disbursement. | Same final status pattern as fresh loan unless Top-Up differs. |

## Detailed Product Flow

### 0. Leads - Top-Up

1. Staff opens Leads.
2. Staff selects **Top-up** tab.
3. App displays Top-Up leads with existing customer context.
4. Staff can search leads.
5. Staff can open lead actions:
   - Call Customer.
   - Reject TopUp Lead.
   - Start Application.
   - Get Direction.
6. If staff rejects lead, reason capture requirement needs confirmation.
7. If staff starts application, the app opens Loan Application Steps for Top-Up.

### 1. Applicant 1 Profile

1. Applicant 1 is the existing primary borrower.
2. Mobile number, name, photo, KYC, and address are generally stable/minimal-changing data points.
3. Applicant 1 always remains the same as the core loan.
4. App may show **Resume** when the profile is partially or already available.
5. If customer data has changed, updates may be handled through service requests such as Mobile Number Change or Address Change.
6. Exact stale-data and refresh rule is open.

### 2. Applicant 2 Profile

1. Applicant 2 profile appears in the Top-Up checklist.
2. Applicant 2 always remains the same as the core loan.
3. A new co-borrower cannot be added in Top-Up.
4. Existing co-borrower data may be reused or refreshed based on policy/service-request rules.

### 3. Applicant 3 Profile (Optional)

1. Applicant 3 is visibly optional in the step list.
2. If the core loan has Applicant 3, Applicant 3 remains the same in Top-Up.
3. A new Applicant 3 cannot be added in Top-Up.
4. If the core loan does not have Applicant 3, staff should be able to leave it optional according to the existing checklist behavior.

### 4. Household Credit-O-Meter

1. Household credit is reassessed for Top-Up eligibility.
2. HH score is used in ticket classification:
   - Open ticket size: HH score 650 or above.
   - Limited ticket size: HH score 600 to 650.
3. Exact rejection behavior below 600 needs confirmation.

### 5. Loan Requirement

Visible fields from screenshot:

| Field | Required? | Notes |
| --- | --- | --- |
| Loan purpose/category | Yes | Screenshot shows category tiles; Vehicle selected in example. Confirm allowed Top-Up purposes. |
| Loan Amount | Yes | Product limits differ by eligibility class; see Ticket Size Rules. |
| Loan Tenure | Yes | Visible options include 3M, 4M, 5M, 6M, 12M, 18M, 24M, 30M, 36M; Top-Up rule currently says 6M to 24M, with 12M or 18M called out. |
| EMI Plan | System-generated | Example format: EMI Plan will be amount x months. |
| Remarks | Yes | Free-text staff remarks. |
| Core Loan Utilisation | Yes | Staff enters how core loan amount has been utilised. |
| Core Loan Amount | System/context | Visible below utilisation field. |

### 6. Residence Details

1. Residence Details can appear as completed and view-only if reused from existing loan.
2. Address is a minimal-changing data point, but Address Change exists as a service request.
3. Staff has the option to change geotag/photos, but it is not mandatory when existing residence details are reused.

### 7. Bank Statement Upload

1. Bank data is a continuously changing data point.
2. Bank statement upload/analysis is used for income and affordability evaluation.
3. Confirm accepted upload methods and minimum statement period for Top-Up.

### 8. Occupation Profiling

1. Occupation may appear as completed if reused from existing loan.
2. Occupation can change and may need redo if loan is given after a year or if staff/customer reports occupation change.
3. Assessment expires after 1 year, so income/occupation assessment should be redone after expiry.

### 9. Occupation & Income Assessment

1. AM/PD completes the income assessment and captures current income and FOIR.
2. Thresholds from latest Top-Up notes:
   - Open ticket size: income Rs. 40,000 or above.
   - Limited ticket size: income below Rs. 40,000.
3. Wallet share and obligations closed in the span of 8 months should be considered.
4. FOIR cutoff is 50%; detailed formula/source belongs in credit/tech docs.

### 10. Disbursement Bank Account Details

1. AM/PD confirms whether bank details may be reused or changed.
2. Bank Details Change exists as a service request.
3. Fresh penny-drop/name match is mandatory for Top-Up disbursement account validation.

### 11. Additional Documents

1. AM/PD collects additional docs only if required by credit, address/bank change, or policy.
2. Exact mandatory Top-Up document list is open.

### 12. BRE / Final Decision

1. AM/PD runs/checks final decisioning after Occupation & Income Assessment.
2. Final decision should consider:
   - EMIs completed.
   - HH score.
   - Income.
   - FOIR.
   - Open or Limited ticket size classification.
   - Current InPrime OSP.
   - Wallet share and obligations closed in the last 8 months.
   - Assessment age.
3. Red/yellow/green handling should follow the base final BRE/review model unless Top-Up has separate rules.

### 13. Loan Offer Generation

1. Credit team generates the Top-Up offer after BRE/review approval.
2. Offer should reflect eligible ticket size and tenure.
3. EMI structure should reference the EMI Structure sheet.
4. If latest approved amount differs from requested amount, confirm whether RO can edit amount/tenure before final submission or only confirm with customer.

### 14. NACH and Repayment Preference

1. RO confirms repayment preference with the customer.
2. Repayment preference can change and has a service request path.
3. Existing mandate may or may not be reusable.
4. NACH automation impact is open.

### 15. Agreement E-sign

1. Agreement/e-sign follows the final accepted Top-Up offer.
2. Confirm which applicants must sign.

### 16. Disbursement

1. Disbursement status should be shown after agreement and repayment readiness.
2. Final owner and failure handling should align with existing disbursement runbook unless Top-Up differs.

## Ticket Size And Eligibility Rules

| Rule area | Open ticket size | Limited ticket size | Notes |
| --- | --- | --- | --- |
| Amount | Rs. 40,000 to Rs. 2 lakh | Rs. 40,000 to Rs. 2 lakh unless credit gives a separate limit | Latest product-limit screenshot is canonical for product-limit docs. |
| EMIs completed | 6 EMIs should be completed | 6 EMIs should be completed unless product confirms otherwise | Source says 6 EMIs completed. |
| HH score | 650 or above | 600 to 650 | Behavior below 600 needs confirmation. |
| Income | Rs. 40,000 or above | Below Rs. 40,000 | Confirm if income is household income or assessed eligible income. |
| Tenure | As per latest product-limit / policy screenshot | As per latest product-limit / policy screenshot | Detailed tenure matrix to be carried in credit/tech docs. |
| Assessment expiry | 1 year | 1 year | Full eligibility expires after 1 year. |

## Data Reuse And Refresh Rules

| Data area | Change category | Product handling |
| --- | --- | --- |
| Bureau | Continuously changing | Fresh bureau/credit view should be used for Top-Up. |
| Mobile number | Minimal changing | Reuse unless Mobile Number Change service request exists. |
| Name | Minimal/no change | Reuse from existing customer profile unless correction flow exists. |
| Photo | Minimal/no change | Reuse unless updated capture is required. |
| KYC | Minimal/no change | Reuse unless expired, invalid, or policy requires refresh. |
| Address | Minimal changing | Reuse unless Address Change service request exists. |
| Bank details | Changing | Confirm or update through Bank Details Change. |
| Occupation | Changing | Reuse if current; redo if changed or assessment expired after 1 year. |
| Family details | Changing | Addition of family details can happen through service request. |
| NACH / repayment preference | Changing | May require new registration or repayment preference change. |

## Related Service Requests

| Service request | Why it matters for Top-Up |
| --- | --- |
| Mobile Number Change | Customer contact/authentication may need update before Top-Up. |
| Address Change | Residence details may need refresh. |
| Bank Details Change | Disbursement/repayment account may need update. |
| Repayment Preference Change | Existing repayment setup may not be usable for Top-Up. |
| Addition of Family Details | Household assessment may need update. |
| Claim Insurance | Existing policy/loan context may affect customer handling. |
| Others | Catch-all support path; final allowed reasons need confirmation. |

## Business Rules And Validations

| Area | Rule / validation | Status |
| --- | --- | --- |
| Entry point | Top-Up starts from Leads > Top-up tab. | Screenshot confirmed. |
| Application start | Only RO can start a Top-Up application. | Arnav clarified. |
| Lead actions | Staff can Call Customer, Reject TopUp Lead, Start Application, and Get Direction. | Screenshot confirmed. |
| Existing borrower | Top-Up is for existing borrowers/leads, not fresh applicants. | Source confirmed. |
| Applicant continuity | Applicant 1, Applicant 2, and Applicant 3 remain the same as the core loan; new co-borrower/applicant cannot be added. | Arnav clarified. |
| Minimum EMI seasoning | 6 EMIs should be completed. | Source confirmed. |
| Open ticket | Rs. 50,000 to Rs. 3 lakh, HH score 650+, income Rs. 40,000+. | Latest note; amount conflict open. |
| Limited ticket | Rs. 50,000 to Rs. 1 lakh, HH score 600-650, income below Rs. 40,000. | Latest note. |
| Assessment expiry | Assessment expires after 1 year. | Source confirmed. |
| Loan requirement | Core Loan Utilisation is mandatory on Loan Requirement screen. | Screenshot confirmed. |
| Residence geotag/photo | Staff can change geotag/photos, but this is not mandatory in Residence Details. | Arnav clarified. |
| FOIR | FOIR is part of Top-Up assessment. | Source confirmed; exact cutoff open. |
| Wallet share | Obligations closed in the span of 8 months must be considered. | Source confirmed; exact calculation open. |
| FOIR | FOIR cutoff is 50%. | Validated by Arnav; detailed formula belongs in credit/tech docs. |
| Rework | Rework is not allowed for Top-Up. | Validated by Arnav. |
| Agreement signer | Applicant 1 signs Top-Up agreement. | Validated by Arnav. |

## User-Visible States

| State | Meaning | Trigger |
| --- | --- | --- |
| Top-Up lead visible | Customer appears in Leads > Top-up tab. | System identifies or assigns Top-Up lead. |
| Lead action menu open | Staff can choose call/reject/start/get direction. | Staff opens three-dot menu. |
| Application started | Top-Up application checklist opens. | Staff taps Start Application. |
| Step completed | Existing/reused or newly completed step is marked complete. | Step data accepted. |
| Step pending/resume | Step requires staff action. | Existing data incomplete, stale, or update required. |
| Offer generated | Eligible Top-Up offer is shown. | BRE/credit decision completes. |
| Lead rejected | Top-Up lead is rejected. | Staff selects Reject TopUp Lead and submits required reason. |

## Acceptance Criteria

- Staff can open Leads and select the Top-up tab.
- Top-Up lead cards show existing borrower context without exposing unnecessary sensitive data outside the app.
- Staff can call customer, reject Top-Up lead, start application, and get direction from lead action menu.
- Only RO can start the Top-Up application.
- Starting a Top-Up opens the Loan Application Steps checklist.
- Applicant 1, Applicant 2, and Applicant 3 remain the same as the core loan.
- New co-borrower/applicant cannot be added in Top-Up.
- Applicant/profile/residence/occupation data can be reused where valid and marked completed/viewable.
- Residence Details allows geotag/photo change but does not make it mandatory.
- Loan Requirement captures loan amount, tenure, remarks, and Core Loan Utilisation.
- EMI plan is displayed after amount and tenure selection.
- Ticket-size eligibility considers EMIs completed, HH score, income, FOIR, wallet share, current OSP, and assessment age.
- Assessment older than 1 year routes to redo income/occupation assessment.
- Repayment/NACH handling is confirmed before disbursement.
- Product doc links unresolved contradictions instead of hiding them.

## Mismatches Or Contradictions

| Issue | Impact | Status |
| --- | --- | --- |
| Earlier product amount limit references differed. Latest product-limit screenshot says Top-Up is Rs. 40,000 to Rs. 2 lakh. | Pricing, eligibility, and validation can be wrong if old limits are used. | Updated to latest screenshot. |
| Screenshot shows tenure options including 3M, 4M, 5M, 6M, 12M, 18M, 24M, 30M, 36M, while latest rule says tenure is 6M to 24M and mentions 12M or 18M. | UI may show options that are not valid for Top-Up. | Open. |
| Product variants summary says Top-Up skips KYC/residence/occupation, while screenshot shows those steps in checklist with some completed states. | Better wording is reuse/confirm existing data, not fully skip all steps. | Updated in Top-Up doc; variants doc should reference this. |

## Open Questions

| Question | Owner | Needed from | Status |
| --- | --- | --- | --- |
| What is the final Top-Up amount range? | Arnav | Product/credit | Resolved: Rs. 40,000 to Rs. 2 lakh as per latest product-limit screenshot. |
| Are Open and Limited ticket sizes two user-visible categories or internal credit classifications? | Arnav | Product/credit | Open |
| Is the 6-EMI completion rule mandatory for both Open and Limited ticket sizes? | Arnav | Product/credit | Open |
| What is the exact FOIR cutoff/formula for Top-Up eligibility? | Arnav + Dileepan | Credit/engineering | Partially resolved: cutoff is 50%; formula/source remains credit/tech. |
| How is wallet share calculated for obligations closed in the last 8 months? | Arnav + Dileepan | Credit/engineering | Open: refer Notion/source file. |
| Which Top-Up checklist steps are always required versus reused/view-only? | Arnav | Product/design | Open |
| Does Top-Up require fresh KYC if existing KYC is older than a threshold? | Arnav | Product/compliance | Open |
| Does Top-Up require fresh residence photo/geotag if address has not changed? | Arnav | Product/operations | Resolved: staff can change geotag/photos, but it is not mandatory. |
| What happens to Top-Up eligibility if HH score is below 600? | Arnav | Product/credit | Open |
| Can Applicant 2 or Applicant 3 be added/changed during Top-Up? | Arnav | Product/credit | Resolved: Applicant 1, Applicant 2, and Applicant 3 remain same as core loan; new co-borrower/applicant cannot be added. |
| Which applicants must sign the Top-Up agreement? | Arnav | Product/legal | Resolved: Applicant 1. |
| Can existing NACH be reused, or is fresh repayment registration mandatory? | Arnav + Dileepan | Product/operations/engineering | Resolved: yes, existing NACH can be reused. |
