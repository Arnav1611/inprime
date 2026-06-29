# Xpress Flow Product Variants

Canonical for product-level differences between Super/Welcome Loan, SMART Loan, Micro LAP, and Top-Up Loan.

Owner: Arnav
Status: draft
Last updated: 2026-06-29

## Source Links

| Source | Link/path | Notes |
| --- | --- | --- |
| Rough documentation | Google Doc: https://docs.google.com/document/d/1RjWx3gUFbFS1ZXHuyM2ElMg1ltK7SCu__IaIKMfZocM/edit?usp=sharing | Sections on product selection, SMART Loan, Top-Up, and structural comparison. |
| Super Loan construct | `super-loan-product-construct.md` | Product overview, customer segment, features, repayment, offer. |
| Smart Loan construct | `smart-loan-product-construct.md` | Product overview, customer segment, features, repayment, offer. |
| SMART Loan application doc | `new-loan-application-smart-loan.md` | Product-level SMART Loan app flow and 17-step checklist. |
| MLAP application doc | `new-loan-application-mlap.md` | Product-level MLAP app flow, applicant construct, collateral/property rules, and 18-step checklist. |
| Top-Up Loan product doc | `top-up-loan.md` | Product-level Top-Up journey, lead entry, eligibility, ticket-size rules, and data reuse. |
| Repeat Loan product doc | `repeat-loan.md` | Product-level Repeat journey, eligibility, lead placement, settlement, and loan-count rules. |
| Figma | TBD | Add exact product selection and product-specific frames. |
| PRD | TBD | Add product-specific requirement docs. |
| Related product doc | `xpress-flow-loan-origination.md` | Main journey doc. |

## Summary

Xpress Flow branches the loan journey based on selected product. Product selection changes applicant requirements, step count, verification modules, role ownership, loan-purpose options, and post-sanction requirements.

## Product Comparison

| Product | Entry point | Mandatory applicant footprint | Key product behavior | Role ownership notes | Open questions |
| --- | --- | --- | --- | --- | --- |
| Super/Welcome Loan | New Loan Application product selection. | Applicant 1 and Applicant 2 mandatory; Applicant 3 optional. | Standard underwriting and automated bureau calls. Latest product-limit screenshot: Super Rs. 80,000 to Rs. 3 lakh; Welcome Rs. 80,000 to Rs. 1.5 lakh. | RO completes work till Occupation Profiling; AM/PD owns Occupation & Income Assessment through BRE; Credit generates/approves offer; RO completes NACH/e-sign; Operations/Opex disburses. | Credit cutoff and exact score labels still need confirmation. |
| SMART Loan | New Loan Application product selection. | Applicant 1 mandatory; Applicant 2 optional; Applicant 3 not visible. | Live in current staff app. 17-step SMART checklist, Prime Test, identity KYC before Business KYC, mandatory Business KYC, mandatory Bank & QR Statement, business-only loan requirement, nominee prerequisite when Applicant 2 skipped. Amount: Rs. 50,000 to Rs. 3 lakh. | Same general handoff: RO till Occupation Profiling, AM/PD through BRE, Credit offer, RO customer-facing post-offer steps, Operations disbursement. | Tech/API/status details stay in tech docs. |
| Micro LAP / MLAP | New Loan Application product selection. | Minimum 2 and maximum 4 applicants. Applicant 1 and Applicant 2 mandatory; Applicant 3 and 4 optional in checklist but become mandatory if they own the property. | Collateral-backed journey with property owner selection, property documents, MLAP BRE, Offer Finalization, NACH, OSV and Agreement, and Encore booking/client mapping. Amount: Rs. 4 lakh to Rs. 10 lakh. | RO captures app flow; AM/PD can request A3/A4 and owns assessment through BRE; Credit owns sanction/FOIR/LTV and offer approval; Ops owns document/disbursement handoff. | Age rules, property-document mandatory list, and Encore mapping failure handling need confirmation. |
| Top-Up Loan | Leads > Top-up tab. | Existing borrower; Applicant 1, Applicant 2, and Applicant 3 remain same as core loan; new co-borrower/applicant cannot be added. | Only RO can start application. AM can assign PD to someone else or do PD themselves. No rework is allowed for Top-Up. Reuses stable data, reassesses bureau, income, FOIR, bank/repayment where needed. Latest product-limit screenshot: Rs. 40,000 to Rs. 2 lakh. | RO, AM/PD, Credit, Operations | Tech/API mapping and detailed wallet-share calculation remain in tech/credit sources. |
| Repeat Loan | Leads > Top-up section currently, marked/tagged as Repeat. | Existing borrower; applicants remain same as existing loan for now. | Created by program manager or credit team. Requires 12 calendar months plus Rs. 40k OSP rule, otherwise 16 months standard. Core loan must be settled; Top-Up and Repeat can run simultaneously. No rework is allowed for Repeat. Amount: Rs. 40,000 to Rs. 3 lakh. | RO/AM can view leads; Credit/program owns lead creation; Ops handles settlement/disbursement. | Exact settlement accounting stays open for ops/tech validation. |

## SMART Loan Product Rules

| Rule | Source | Confidence | Notes |
| --- | --- | --- | --- |
| SMART Loan requires only one mandatory applicant. | Rough documentation | Medium | Co-borrower is optional; validate against current app. |
| Applicant 3 is hidden/disabled for SMART Loan. | Rough documentation | Medium | Confirm step index. |
| Prime Test is present before Business KYC in SMART Loan. | Arnav clarification | High | Final visible label confirmed as Prime Test. |
| Identity KYC requires any 2 documents from Aadhaar, PAN, Driving Licence, and Voter ID. | Arnav clarification | High | PAN or Form 60 is also required. |
| Business KYC supports GST, Shop and Establishment, Udyam, and Other Business KYC. | Rough documentation | Medium | Validate provider/API and exact labels. |
| SMART Loan uses 17 visible checklist steps in current draft. | SMART Loan application doc | Medium | Confirm whether Reapply Review is visible in current app/Figma. |
| Bank Statement is renamed Bank & QR Statement for SMART Loan. | SMART Loan phase 1 attachment + Arnav validation | High | Bank and QR statement are both mandatory. |
| Loan type is only Business Loan. | SMART Loan phase 1 attachment | High | Amount Rs. 50,000 to Rs. 3 lakh; tenure 3M to 36M. |
| Selecting GST/Shop/Udyam requires registration-number entry and automated verification. | Rough documentation | Low | Needs provider and tech validation. |
| Other Business KYC uses manual document/photo upload instead of automated lookup. | Rough documentation | Medium | Confirm accepted documents. |
| Loan Type is locked to Business Loan. | Rough documentation | Medium | Confirm UI behavior. |
| RO can reduce sanctioned principal but cannot exceed maximum approved amount. | Rough documentation | Medium | Confirm offer-generation controls. |
| Insurance nominee details are required in SMART Loan offer generation when Applicant 2 is skipped. | Rough documentation + screenshot | High | Required before InPrime Loan Offer; fields confirmed in SMART Loan product doc. |

## Super Loan Product Rules

| Rule | Source | Confidence | Notes |
| --- | --- | --- | --- |
| Super Loan is for Informal Prime customers. | Super Loan construct | High | Target customers have informal income, proven credit track record, and digital adoption. |
| Applicant count is minimum 2 and maximum 3. | Super Loan construct | High | Applicant 3 optional in current app docs. |
| Tenure is 6 to 36 months. | Super Loan construct | High | Confirm if all values are live in app. |
| Interest rate is 25% per annum fixed. | Super Loan construct | Medium | Confirm current pricing policy. |
| Processing fee is 2.5% + GST. | Super Loan construct | Medium | Confirm current fee policy. |
| Repayment is monthly EMI. | Super Loan construct | High | Repayment channels include NACH, UPI Autopay, online, BBPS, cash points. |

## Top-Up Loan Product Rules

| Rule | Source | Confidence | Notes |
| --- | --- | --- | --- |
| Top-Up is accessed through Leads module. | Rough documentation | Medium | Confirm lead status/eligibility trigger. |
| Only RO can start a Top-Up application. | Arnav clarification | High | AM/PD may be involved after assignment/review. |
| Customer must be an existing active borrower in good repayment standing. | Rough documentation | Low | Exact eligibility rule needed. |
| Applicant 1, Applicant 2, and Applicant 3 remain the same as the core loan. | Arnav clarification | High | New co-borrower/applicant cannot be added in Top-Up. |
| AM can assign PD to someone else or do PD themselves. | Arnav clarification | High | Same as fresh loan. |
| Residence geotag/photos can be changed but are not mandatory. | Arnav clarification | High | Applies in Top-Up Residence Details. |
| Top-Up lead card shows last disbursement date, EMIs paid, and current InPrime OSP. | Screenshot | High | Do not reproduce customer PII from screenshots. |
| Staff actions include Call Customer, Reject TopUp Lead, Start Application, and Get Direction. | Screenshot | High | Reject reason requirement needs confirmation. |
| Existing profile data is reused, confirmed, or refreshed rather than always recollected. | Screenshot + latest notes | Medium | Residence and occupation can show completed/view details in checklist. |
| Fresh bureau/HH score and income/FOIR assessment are part of Top-Up decisioning. | Latest notes | Medium | Exact APIs and formula need validation. |
| Assessment expires after 1 year. | Latest notes | High | Occupation/income reassessment should happen after expiry. |
| Product limit is Rs. 40,000 to Rs. 2 lakh. | Latest product-limit screenshot | High | Current product-limit value for documentation. |
| Top-Up FOIR cutoff is 50%. | Arnav validation | Medium | Calculation/source detail remains with credit/tech. |
| Top-Up eligibility requires 6 months/EMIs after core loan context. | Arnav validation | Medium | Exact data source remains in tech/credit docs. |

## Repeat Loan Product Rules

| Rule | Source | Confidence | Notes |
| --- | --- | --- | --- |
| Repeat leads are created by program manager or credit team. | Stakeholder clarification | High | RO/AM see the lead after creation. |
| Repeat is currently shown under Top-up section of Leads but marked as Repeat. | Stakeholder clarification | High | UI may need clearer separation later. |
| Repeat requires 12 months EMI paid without bounce. | Stakeholder clarification | High | Exact data source needs tech validation. |
| Repeat amount is Rs. 40,000 to Rs. 3 lakh. | Latest product-limit screenshot | High | Current product-limit value for documentation. |
| Only two loans can exist for one applicant. | Stakeholder clarification | High | Edge cases across core, Top-Up, and Repeat need mapping. |
| Core loan must be settled to get Repeat after 12 months. | Stakeholder clarification | High | OSP can be reduced from Repeat amount. |
| Active Top-Up should not be settled through Repeat if only 6 months old or less. | Stakeholder clarification | Medium | Final threshold and rule wording need confirmation. |

## MLAP Product Rules

| Rule | Source | Confidence | Notes |
| --- | --- | --- | --- |
| MLAP means Micro Loan Against Property. | MLAP Product Training PPT | High | Product is collateral/property backed. |
| Entry point is Home > New Loan Application > MLAP/Micro LAP. | Rough MLAP flow | High | Selected like other new loan product variants. |
| Applicant count is minimum 2 and maximum 4. | Training PPT | High | Applicant 3 and 4 are optional in checklist but depend on property ownership. |
| Applicant 1 must be an existing InPrime customer and main earning member. | Rough MLAP flow + screenshot | High | Non-existing mobile number should be blocked with error. |
| Applicant 1 age is 21 to 55. | Rough MLAP flow + PPT | High | Other applicant age rules need final reconciliation. |
| All property owners/co-owners must be part of the application. | Training PPT | High | More than 4 owners makes the case not possible in training example. |
| Loan amount is Rs. 4 lakh to Rs. 10 lakh. | Training PPT + Arnav clarification | High | Already reflected in pricing docs. |
| Tenure is 36M to 96M in multiples of 6. | Rough MLAP flow + PPT | High | Display should show months and years/months. |
| Loan purposes include Business, House, Loan Closure, Education, and Other. | Rough MLAP flow + PPT | High | Sub-purposes documented in MLAP product doc. |
| MLAP uses a new MLAP BRE. | Rough MLAP flow | Medium | Tech/code validation needed. |
| MLAP booking happens in Encore and existing applicants should map to existing Encore clients. | Arnav clarification | Medium | Detailed implementation belongs in tech docs. |

## Product Amount Limits

| Product | Amount limit | Source | Confidence |
| --- | --- | --- | --- |
| Super Loan | Rs. 80,000 to Rs. 3 lakh | Latest product-limit screenshot | High |
| Welcome Loan | Rs. 80,000 to Rs. 1.5 lakh | Arnav clarification | High |
| Top-Up Loan | Rs. 40,000 to Rs. 2 lakh | Latest product-limit screenshot | High |
| Repeat Loan | Rs. 40,000 to Rs. 3 lakh | Latest product-limit screenshot | High |
| MLAP / Micro LAP | Rs. 4 lakh to Rs. 10 lakh | Arnav clarification | High |
| SMART Loan | Rs. 50,000 to Rs. 3 lakh | Arnav clarification | High |
| Festival Loan | Rs. 25,000 to Rs. 40,000 | Latest product-limit screenshot | Medium; separate product doc not yet created |

## Product-Specific Open Questions

| Question | Owner | Needed from | Status |
| --- | --- | --- | --- |
| What are the official product names and labels shown in current app? | Arnav | Product/design | Partially resolved: MLAP label confirmed as `mlap`; remaining labels need Figma/current app validation. |
| Are Super Loan and Welcome Loan separate flows or one combined card? | Arnav | Product/manager | Resolved: same flow; limits differ. |
| What are the exact age and ownership-trigger rules for MLAP Applicant 2, Applicant 3, and Applicant 4? | Arnav | Product/credit | Open |
| Is MLAP OSV and Agreement upload-only, e-sign, or both? | Arnav | Product/operations | Resolved by Arnav: both. |
| Which MLAP property documents are mandatory, conditional, or optional? | Arnav | Credit/operations/legal | Open |
| Which products are live today and which are future/planned? | Arnav | Product/manager | Open |
| What is the final Top-Up amount range and tenure matrix? | Arnav | Product/credit | Partially resolved: amount Rs. 40,000 to Rs. 2 lakh; tenure from screenshot/policy still to document in tech/credit detail. |
| Which existing Top-Up fields are reused, editable, or require service request updates? | Arnav/Dileepan | Product/engineering | Open |
| What are the exact SMART Loan business KYC document options? | Arnav | Product/compliance | Open |
| What are the exact product-wise tenure boundaries? | Arnav | Product/credit | Open |
