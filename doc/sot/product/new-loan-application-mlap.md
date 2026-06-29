# New Loan Application - MLAP / Micro LAP

Canonical for product intent, visible screen order, user-facing behavior, business rules, acceptance criteria, and open questions for the MLAP journey selected from **Home > New Loan Application**.

Owner: Arnav  
Status: draft  
Last updated: 2026-06-29

## Source Links

| Source | Link/path | Notes |
| --- | --- | --- |
| MLAP rough mobile/CRM flow | User-provided attachment | Priority source for current MLAP mobile and CRM behavior. |
| Xpress App V.20.0.0 PPT | User-provided PPT | Product construct, property checklist, operations handoff. |
| MLAP Product Training PPT | User-provided PPT | Product construct, applicant rules, value proposition, FOIR/LTV rules. |
| MLAP app screenshots | User-provided screenshots | Confirms visible 18-step checklist order. Do not reproduce customer PII. |
| MLAP mobile verification screenshot | User-provided screenshot | Confirms Applicant 1 existing-customer instruction and mobile OTP entry. |
| Property documentation screenshot | User-provided screenshot | Confirms property documentation selector options. |
| App design | https://www.figma.com/design/F4TByjJMRTVNC8wFp8gNUq/InPrime-LOS?node-id=16464-44840&t=5sxbiFHIvrrXaM7E-4 | Current MLAP app design reference. |
| Web design | https://www.figma.com/design/IyJk7N4pu3glJSKAyzUZH7/Web---InPrime-LOS?node-id=12973-31693&t=zrVkLKajJlU3yHcu-4 | CRM/LOS design reference. |
| Flow doc | `../flows/new-loan-application-mlap.md` | End-to-end sequencing, role handoffs, API touchpoints, state transitions. |
| Product variants doc | `xpress-flow-product-variants.md` | Cross-product comparison and amount limits. |

## Scope

This document covers the **MLAP / Micro LAP** new loan application journey selected through the staff app home screen option **New Loan Application**.

Out of scope:

- Super/Welcome Loan, SMART Loan, Top-Up Loan, and Repeat Loan details except for comparison.
- Full API implementation and code-path mapping.
- Provider-specific behavior.
- Raw customer data, raw provider payloads, production screenshots with PII, or sensitive configuration.
- Final operations runbook for physical document movement; this doc only captures the product-level handoff.

## Summary

MLAP means **Micro Loan Against Property**. It is a collateral-backed product for existing InPrime customers who need a higher ticket loan, usually for business, house, education, loan closure, or other approved purposes. MLAP is selected from **New Loan Application** and uses a visible 18-step checklist.

The flow is similar to the existing new loan application journey, but MLAP adds product-specific rules:

- Applicant 1 must be an existing InPrime customer and the main earning member.
- Minimum 2 applicants and maximum 4 applicants are allowed.
- Applicant 3 and Applicant 4 are optional in the visible checklist, but become mandatory if they are property owners/co-owners who must be included in the application.
- All property owners/co-owners must be part of the loan application, with no more than 4 co-owners.
- Loan amount range is Rs. 4 lakh to Rs. 10 lakh.
- Tenure range is 36 months to 96 months in multiples of 6.
- Property checklist and collateral documentation are part of the journey.
- MLAP uses a new MLAP BRE.
- Booking happens in Encore. Existing applicants should be mapped to existing Encore client IDs instead of creating duplicate clients.

## Business Objective

- Retain existing InPrime customers who may otherwise foreclose and borrow from another institution.
- Offer higher ticket funding up to Rs. 10 lakh against property.
- Reduce EMI burden through longer tenure where eligible.
- Capture property ownership, collateral documentation, income, FOIR, and LTV information in a reviewable journey.
- Keep the app flow aligned with CRM, credit, operations, and Encore booking needs.

## Users And Roles

| Role / actor | Product role in MLAP |
| --- | --- |
| RO / Staff user | Starts New Loan Application, selects MLAP, captures applicant and loan details, uploads documents, and completes customer-facing steps. |
| Applicant 1 | Mandatory existing InPrime customer, main earning member, and loan end user. Age: 21 to 55. |
| Applicant 2 | Mandatory co-applicant/spouse of Applicant 1 where applicable. Age rule needs final confirmation because sources differ. |
| Applicant 3 | Optional in checklist, but becomes mandatory if needed to include property owner/co-owner. AM/PD can request A3. |
| Applicant 4 | Optional in checklist, but becomes mandatory if needed to include property owner/co-owner. AM/PD can request A4. |
| AM / PD | Reviews/requests additional applicants and performs PD/review handoff as per status and role rules. |
| Credit team | Reviews income, FOIR, LTV, property value, legal/valuer inputs, and proposed sanction. |
| Operations | Handles original document handoff, agreement collection, OSV, and final disbursement marking. |
| Encore / Finflux systems | Encore is used for MLAP booking; existing mapped clients should not be duplicated. Detailed implementation belongs in tech docs. |

## Visible 18-Step Checklist

| Step | Visible screen label | Visible description / purpose |
| --- | --- | --- |
| 1 | Applicant 1 Profile | Current Step - Provide Primary Borrower Profile Details. |
| 2 | Applicant 2 Profile | Provide 1st Co-borrower Profile Details. |
| 3 | Applicant 3 Profile (Optional) | Provide 2nd Co-borrower Profile Details. |
| 4 | Applicant 4 Profile (Optional) | Provide 3rd Co-borrower Profile Details. |
| 5 | Household Credit-O-Meter | View the Household Credit-O-Meter and basic eligibility. |
| 6 | Loan Requirement | Fill out the loan requirement details. |
| 7 | Family Details | Provide Family Details of the Household. |
| 8 | Residence Details | Provide Communication address and Resident Details. |
| 9 | Bank Statement Upload | Upload and analyse bank statement for evaluating income. |
| 10 | Occupation Profiling | Please add a brief about the Major Occupations. |
| 11 | Income Assessment | Add occupations of applicant and complete Income Assessment. |
| 12 | Disbursement Bank Account Details | Provide Primary Borrower Bank Account details for loan disbursement. |
| 13 | Upload Additional Documents | Provide any additional documents to support application. |
| 14 | Decisioning & Offer | View Final Loan Offer. |
| 15 | Offer Finalization | View Final Loan Offer. |
| 16 | NACH Registration | Provide Repayment Preference and register on E-NACH. |
| 17 | OSV and Agreement | View Loan Documents and complete E-Sign. |
| 18 | Disbursement | View Disbursement Status. |

## Detailed Product Flow

### 0. Product Selection

1. Staff logs into the staff app.
2. Staff opens **New Loan Application** from the home screen.
3. Staff selects **Micro LAP / MLAP**.
4. The MLAP checklist opens with 18 visible steps.

### 1. Applicant 1 Profile

1. Applicant 1 must be an existing InPrime customer.
2. Applicant 1 should be the main earning member of the household.
3. Mobile verification uses the same base flow, but the screen shows MLAP-specific guidance: "Please input existing customer of InPrime as applicant 1 who is a major earning member of the household".
4. If the mobile number is not an existing InPrime customer, show error: "The mobile number you entered is not an existing InPrime Customer, kindly check the contact number".
5. Area serviceability follows the existing loan flow.
6. There is no Prime Test for MLAP.
7. KYC follows the existing KYC flow.
8. Age restriction: 21 to 55.
9. Lead-level data should pre-populate where available:
   - KYC is non-editable, but new KYC can be added.
   - Live photo must be captured.
   - Existing address is shown, and a new address can be added.
   - Existing BSA can be refreshed, deleted, or added.
   - Existing income can be edited, deleted, or added.

### 2. Applicant 2 Profile

1. Applicant 2 is mandatory.
2. Mobile number, relationship, and KYC flow follow the existing flow.
3. If Applicant 2 is new to InPrime, the app should show: "New Applicant This is not an existing InPrime applicant. You will need to do complete KYC to add new applicant."
4. CTAs: **Go Back** and **Proceed to KYC**.
5. Age restriction is open because sources differ:
   - Rough flow says 18 to 80.
   - Training PPT says 21 to 60 if earning member and 18 to 80 if not earning.

### 3. Applicant 3 Profile (Optional)

1. Applicant 3 is optional in the visible checklist.
2. Skip option should be available.
3. AM/PD should have a **Request A3** option.
4. Applicant 3 becomes required if Applicant 3 is a property owner/co-owner needed in the application.
5. Age restriction is open because sources differ between rough flow and training PPT.

### 4. Applicant 4 Profile (Optional)

1. Applicant 4 is optional in the visible checklist.
2. Skip option should be available.
3. AM/PD should have a **Request A4** option.
4. Applicant 4 is used for an additional house/property owner where applicable.
5. Maximum applicant count is 4; if property ownership requires 5 applicants, the case is not possible as per training example.

### 5. Household Credit-O-Meter

1. Household Credit-O-Meter follows the existing loan flow.
2. It should show household credit and basic eligibility.
3. Credit policy details, score interpretation, and reject thresholds need confirmation for MLAP.

### 6. Loan Requirement

MLAP loan requirement captures purpose, amount, tenure, remarks, property ownership, and property documentation.

Loan amount and tenure rules:

| Field | Rule |
| --- | --- |
| Loan amount | Rs. 4 lakh to Rs. 10 lakh. |
| Tenure | 36M to 96M in multiples of 6. |
| Tenure options | 36, 42, 48, 54, 60, 66, 72, 78, 84, 90, 96 months. |
| Tenure display | Show months with years/months, e.g. 42 months (3 Years 6 Months). |
| Remarks | Same as existing loan flow. |

Loan purpose options:

| Category | Sub-purpose |
| --- | --- |
| Business Loan | Purchase of small machinery; Working capital; Purchase of furniture fixture; Purchase of commercial property; Construction of commercial property; Renovation/Extension of Business Premise. |
| House Loan | House Renovation/Construction; Furniture and Fixtures. |
| Loan Closure | Closure of formal lending; Closure of informal lending. |
| Education Loan | School/College Fees; Tuition Fees; Hostel Fees; Other Education Expense. |
| Other | Other. |

Property ownership and collateral rules:

- All house/property owners must be part of the loan application.
- Property should be owned by no more than 4 co-owners.
- Co-owners should be blood relatives of Applicant 1, with allowed relationships including parents, siblings, children, and in-laws where spouse is part of application.
- At least one co-owner residing in the same house is mentioned in training examples; final rule needs confirmation.
- Property owner selection should use A1 to A4 checkboxes.
- Property photographs: rough notes say add 2 more photographs, total 5, all mandatory. Confirm final app rule.

Property documentation selector visible in screenshot:

| Visible option | Notes |
| --- | --- |
| DEED (Purchase; Sales; Gift; Partition) | Screenshot wording. |
| KHTHA (11A; 11B or revenue) | Screenshot spelling; training PPT also references Khata/Khatha. Confirm final label. |
| TAX PAID - latest financial year | Latest tax paid receipt. |
| EC (Encumbrance Certificate) - 13 years | Training PPT says latest 13 years and not older than 30 days from application date. |
| Any sort of Affidavit | Exact accepted affidavit types need confirmation. |
| Family tree certificate | Confirm when mandatory. |

Training PPT also lists these property documents:

- Latest Sale Deed / Title Deed with document reference number.
- Khata Certificate / 7/12 / Patta with document reference number.
- E-Khatha.
- Encumbrance certificate for latest 13 years.
- Latest tax paid receipt.
- Indemnity certificate if property document does not have the indemnity clause.

### 7. Family Details

1. Family and demographic details follow the existing flow.
2. Family data should be added new for MLAP even when applicant data is pre-populated.
3. Household relationship rules matter because applicant ownership and income/obligation calculations depend on who stays in the same house.

### 8. Residence Details

1. Residence Details follow the Super Loan flow.
2. Existing address can be shown and a new address can be added.
3. Property address, property owner residing address, and applicant residence address may differ; final validation rules need confirmation.

### 9. Bank Statement Upload

1. Bank statement flow follows the existing flow.
2. Existing BSA can be refreshed.
3. Delete and add functionality should be available.
4. If name match is below threshold, current open point says the app returns to bank statement screen without showing a clear message; this needs product and tech confirmation.

### 10. Occupation Profiling

1. Occupation profiling follows Super Loan behavior.
2. Occupation selection should populate as per Super Loan.
3. Across all products and screens, replace borrower/co-borrower terminology with applicant labels such as A1 - Applicant Name.
4. Occupation data should show the latest income data, with edit/delete/add behavior where applicable.

### 11. Income Assessment

1. Income assessment follows the existing flow.
2. CRM Income and FOIR page should allow Credit to input proposed loan amount, tenure, EMI, and FOIR.
3. Training PPT says household should have minimum income of Rs. 4 lakh per annum.
4. Income considered: major/prime supplementary income of applicants residing in the same house as final loan end user.
5. Obligations considered: all applicants residing in the same house as final loan end user.
6. FOIR/LTV decision rules from training PPT:
   - Loan can be sanctioned up to 70% of property value.
   - Existing unsecured exposure should be less than property value.
   - FOIR + LTV should be less than or equal to 110%.
   - Max FOIR: 50% for income Rs. 33.3k to Rs. 40k.
   - Max FOIR: 60% for income above Rs. 40k.

### 12. Disbursement Bank Account Details

1. Disbursement bank account details follow the existing flow.
2. Confirm whether only Applicant 1 account is allowed or if other applicant accounts are allowed for MLAP.
3. Confirm whether bank account name matching is mandatory for MLAP.

### 13. Upload Additional Documents

1. Additional documents follow the existing flow.
2. Property-specific documents should be captured through the property checklist and/or additional document upload, depending on final app design.
3. Final mandatory vs optional document list needs confirmation.

### 14. Decisioning & Offer

1. MLAP uses a new MLAP BRE.
2. Decisioning should consider applicant construct, property ownership, bureau, income, FOIR, LTV, legal/valuer inputs, and property documents.
3. CRM Loan Application Details, BRE, BSA, Income and FOIR are same as existing unless MLAP-specific rules override.
4. Rework, status handling, and role-based access restrictions remain the same basis status and role.

MLAP rejection reasons listed in rough flow:

- High bounces in bank account.
- High alcohol/gambling transactions in bank account.
- Property documents not available.
- Income stability cannot be verified.
- Low income household.
- Business ownership cannot be established.
- House owner not a part of application.
- High FOIR.
- Low property valuation.
- Rejected as per legal report.
- Rejected as per valuer report.
- MOTD could not be created.
- Customer not interested.
- Others.

### 15. Offer Finalization

1. Offer finalization should collect only:
   - Loan amount.
   - Tenure.
   - Repayment date.
2. Remove other fields like insurance and EMI from staff input for current phase.
3. Loan amount and tenure are non-editable because they come from credit sanctioned details.
4. Interest rate is around 22% to 24% declining.
5. Pricing/charges from PPT:
   - Login fee: Rs. 5,000 + GST.
   - Processing fee: 2% + GST.
   - Insurance: Applicant 1 mandatory; Applicant 2 case-to-case.
   - Disbursement: maximum 2 tranches.

### 16. NACH Registration

1. NACH Registration follows the existing flow.
2. CRM should show NACH recommendation similar to SMART Loan flow.
3. Confirm whether MLAP has any mandate rules different from Super/Welcome.

### 17. OSV and Agreement

1. OSV follows the existing flow.
2. Screenshot says "View Loan Documents and complete E-Sign".
3. Current validated behavior is both OSV/agreement upload and e-sign where applicable.
4. Operations process says AM scans original documents and shares over email, loan agreement is shared after originals, signed agreement and OSV are couriered to HO.

### 18. Disbursement

1. Disbursement screen shows disbursement status.
2. Ops **Mark As Disbursed** should mark the case as disbursed and move the file to the disbursed bucket.
3. Maximum 2 tranches are allowed for disbursement where foreclosure of existing InPrime/other loans is involved.

## Encore And Client Mapping Rules

Product-level truth:

- MLAP loans are booked on Encore.
- For Micro LAP, new clients may be created directly in Encore.
- If MLAP is given to an existing unsecured loan client, the customer may already have client IDs in both Finflux and Encore.
- As clients are migrated, the same Finflux clients should already be available in Encore.
- For any existing applicant in an MLAP application, no new Encore client should be created. The same Encore client should be mapped to the loan account using the Clients Mapping source.

Detailed API, entity, and failure-handling truth belongs in `../tech/` and should be owned by Dileepan.

## Business Rules

| Rule | Product behavior | Status |
| --- | --- | --- |
| MLAP entry point | Staff selects MLAP from Home > New Loan Application. | Confirmed from rough flow. |
| Applicant count | Minimum 2, maximum 4. | Confirmed by PPT. |
| Applicant 1 | Must be existing InPrime customer and main earning member. | Confirmed by rough flow and screenshot. |
| Applicant 1 age | 21 to 55. | Confirmed. |
| Applicant 2 | Mandatory. | Confirmed by applicant construct. |
| Applicant 3/4 | Optional in checklist, but mandatory if the person is a property owner/co-owner required in the application. | Validated by Arnav. |
| Property owners | All property owners/co-owners must be part of application. | Confirmed by PPT. |
| Max co-owners | Property should be owned by no more than 4 co-owners. | Confirmed by PPT. |
| Amount | Rs. 4 lakh to Rs. 10 lakh. | Confirmed. |
| Tenure | 36M to 96M in multiples of 6. | Confirmed. |
| Prime Test | No Prime Test for MLAP. | Confirmed by rough flow. |
| BRE | New MLAP BRE is used. | Confirmed by rough flow. |
| Dedupe | No dedupe on disbursed loans; same lead cannot have more than 1 WIP case of any product; new lead ID should not be created for same user. | Needs engineering validation. |
| Encore mapping | Existing MLAP applicants should map to existing Encore clients instead of creating duplicates. | Needs tech validation. |

## Mismatches And Open Points

| Issue | Impact | Status |
| --- | --- | --- |
| Rough flow says Applicant 2/3/4 age is 18 to 80, while training PPT says 21 to 60 if earning and 18 to 80 if non-earning. | Wrong applicant validation if unresolved. | Open |
| Screenshot says OSV and Agreement completes E-Sign, while rough flow says Agreement E-sign is only upload. | Agreement step could be misunderstood. | Updated: current validated behavior is both. |
| Property selector screenshot says "KHTHA", while PPT says Khata/Khatha. | Visible copy and documentation taxonomy need final spelling. | Open |
| Visible checklist has 18 steps, while rough flow lists more granular hidden/substeps. | Product docs should use visible 18-step order and list hidden substeps under each step. | Resolved approach |
| Interest rate differs in older sources. | Pricing/offer docs need current credit-approved rule. | Updated to around 22%-24%; final exact rate source remains credit-owned. |
| Product selection note says "2 options" but lists Super/Welcome, Smart, and Micro LAP. | Product selection count/labels need cleanup. | Open |

## Acceptance Criteria

- Staff can select MLAP from Home > New Loan Application.
- App shows the MLAP 18-step checklist in the documented visible order.
- Applicant 1 mobile verification blocks non-existing InPrime customers with the documented error message.
- Applicant 1 cannot proceed unless the customer is an existing InPrime customer and age rule passes.
- Applicant 2 is mandatory.
- Applicant 3 and Applicant 4 are skippable unless property ownership rules require them.
- Loan amount outside Rs. 4 lakh to Rs. 10 lakh is blocked.
- Tenure outside 36M to 96M or not in multiples of 6 is blocked.
- Loan purpose supports Business Loan, House Loan, Loan Closure, Education Loan, and Other categories with listed sub-purposes.
- Property owner selection and property documentation capture are available in the MLAP journey.
- Decisioning uses MLAP-specific BRE.
- Offer Finalization does not allow staff to edit sanctioned amount and tenure.
- Existing applicants are not duplicated in Encore when a valid client mapping exists.
- Ops Mark As Disbursed moves the file to the disbursed bucket.

## Open Questions

| Question | Owner | Needed from | Status |
| --- | --- | --- | --- |
| What final age rule applies to Applicant 2, Applicant 3, and Applicant 4? | Arnav | Product/credit | Open |
| When exactly do optional Applicant 3 and Applicant 4 become mandatory because of property ownership? | Arnav | Credit/product | Resolved: if they are property owners/co-owners who must be included in the application. |
| Which property documents are mandatory, conditional, or optional? | Arnav | Credit/operations/legal | Open |
| Is MLAP agreement step upload-only, e-sign, or both? | Arnav | Product/operations | Resolved: both. |
| What is the final MLAP interest-rate rule: fixed 24% or 22%-24% negotiation? | Arnav | Credit/product | Partially resolved: around 22%-24%; exact current credit-approved rule still should be linked. |
| What user-visible message should show when bank statement name match is below threshold? | Arnav + Dileepan | Product/engineering | Open |
| What happens if existing Encore client mapping is missing or conflicting? | Dileepan | Engineering/operations | Open |
| Which MLAP statuses and rejection reasons are visible to RO, AM, PD, Credit, and Ops? | Arnav + Dileepan | Product/engineering | Open |
