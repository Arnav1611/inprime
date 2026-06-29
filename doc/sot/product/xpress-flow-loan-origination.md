# Xpress Flow Loan Origination

Canonical for product intent, screens, business rules, visible states, and acceptance criteria for the new loan application journey.

Owner: Arnav
Status: draft
Last updated: 2026-06-09

## Source Links

| Source | Link/path | Notes |
| --- | --- | --- |
| Rough documentation | Google Doc: https://docs.google.com/document/d/1RjWx3gUFbFS1ZXHuyM2ElMg1ltK7SCu__IaIKMfZocM/edit?usp=sharing | Covers product selection, applicant setup, KYC, serviceability, residence, family, BSA, disbursement, docs, BRE, offer, NACH, e-sign. |
| Figma | TBD | Add exact screen/frame links per module. |
| PRD | TBD | Add canonical requirement source. |
| Flow doc | TBD | Create `docs/sot/flows/xpress-flow-loan-origination.md`. |
| Tech doc | TBD | Create `docs/sot/tech/xpress-flow-loan-origination.md`. |
| Provider docs | TBD | Digitap, Digio, Karza, Equifax, CRIF, MSG91, Finflux as applicable. |

## Summary

The Loan Origination journey allows a Relationship Officer and downstream staff roles to create, verify, assess, approve, sign, and submit a loan application. The journey starts from Home Dashboard > New Loan Application, branches by selected product, and then progresses through applicant verification, household and credit checks, loan requirement capture, residence/family/bank data, BRE, offer acceptance, repayment mandate, and agreement e-sign.

Canonical role handoff:

1. RO owns the application work up to **Occupation Profiling**.
2. AM/PD owns **Occupation & Income Assessment through BRE**, including any intermediate assessment/supporting steps required before BRE.
3. AM/PD sends the file to the credit team after BRE.
4. Credit team reviews/approves and generates the loan offer.
5. RO contacts the customer after offer generation and completes customer-facing post-offer steps such as NACH/repayment preference and agreement/e-sign.
6. RO sends the file for disbursement after required post-offer steps are complete.
7. Operations/Opex disburses the file.

## Business Objective

- Capture loan application data in a guided, role-aware mobile flow.
- Enforce product-specific applicant and document requirements.
- Reduce manual errors by validating key inputs during data capture.
- Prepare a complete file for underwriting, repayment setup, legal signing, and disbursement.

## Users and Roles

| Role | Role in origination | Stage ownership from rough doc | Open questions |
| --- | --- | --- | --- |
| Relationship Officer | Starts application, captures applicant details, verifies mobile/KYC, and completes the application up to Occupation Profiling. | RO owns the pre-assessment customer/application capture block and returns after offer generation for customer-facing post-offer steps. | Confirm product-specific exceptions. |
| Area Manager | Performs PD himself or assigns PD person; owns assessment block where assigned. | AM/PD owns Occupation & Income Assessment through BRE. | Confirm AM vs PD assignment rules. |
| Credit Manager / PD | Conducts personal discussion, income assessment, intermediate assessment/supporting steps, and BRE before credit review. | Occupation & Income Assessment through BRE. | Confirm role code and screen access. |
| Credit Analyst | Reviews post-BRE file and generates sanction/offer after approval. | Backend credit review after AM/PD submits file. | Confirm whether analyst actions are inside Xpress Flow. |
| Operations | Handles final disbursement and closing checks. | Disburses after RO completes customer-facing post-offer steps and sends file for disbursement. | Need operations-stage screens. |

## High-Level Journey

| Step | Module | Purpose | Primary role | Visible completion/status from rough doc | Open questions |
| --- | --- | --- | --- | --- | --- |
| 1 | Product selection | Select Super/Welcome Loan, Smart Loan, or Micro LAP. | RO | Product choice stored and downstream steps configured. | Confirm live product list and naming. |
| 2 | Multi-applicant setup | Configure mandatory/optional applicant nodes by product. | RO | Product-specific step count and applicant requirements. | Confirm exact step counts in current app. |
| 3 | Applicant mobile verification | Capture mobile number, WhatsApp flag, language if applicable, OTP consent. | RO | `App1MobileVerified` / `AppInitiated` mentioned. | Confirm statuses and OTP provider. |
| 4 | Area serviceability | Validate pincode and micro-area against serviceability master. | RO | Area serviceable/unserviceable. | Confirm pincode source and bypass rules. |
| 5 | KYC verification | Complete required document verification. | RO | Any 2 KYCs rule mentioned. | Need full KYC rule review. |
| 6 | Household Credit-O-Meter | Aggregate bureau/household risk metrics. | RO/PD | `HHCreditMeterGenerated` mentioned. | Confirm bureau score/overdue rules. |
| 7 | Reapply review | Review existing InPrime loan history if applicant exists. | RO | RO adds remark and proceeds. | Need source and rules. |
| 8 | Loan requirement | Capture loan type, amount, tenure, purpose split, remarks. | RO | Loan requirement submitted. | Confirm product constraints. |
| 9 | Residence details | Select/add address and capture housing details/serviceability. | RO | Residence details submitted. | Confirm product-specific exceptions. |
| 10 | Family details | Capture household members, expenses, demographics. | RO | `FamilyDetailsSubmitted` mentioned. | Confirm required family fields. |
| 11 | Bank statement/BSA | Upload or ingest bank statements and review analysis. | RO | `BankStatementUploadSuccess` mentioned. | Confirm providers and edit permissions. |
| 12 | Occupation/income assessment | Capture field income and FOIR assessment. | AM/PD | Assessment done mentioned. | Need separate product doc. |
| 13 | Disbursement bank account | Capture verified account and penny-drop validation. | AM/PD | Part of AM/PD-owned assessment-to-BRE block. | Confirm penny-drop provider. |
| 14 | Additional documents | Optional upload of supporting docs before BRE. | AM/PD | Part of AM/PD-owned assessment-to-BRE block. | Confirm optionality and file limits. |
| 15 | BRE | Policy/BRE check before credit review. | AM/PD/system | `BREPolicyBlocked` on failure. | Confirm rules and queues. |
| 16 | Loan offer | Credit generates sanctioned offer; RO contacts customer to confirm/accept or request change where allowed. | Credit + RO | `LoanOfferAccepted` mentioned. | Confirm request-change flow. |
| 17 | NACH/repayment | Register repayment mandate or physical fallback. | RO | Valid mandate/reference required. | Confirm provider and acceptable modes. |
| 18 | Agreement e-sign | OSV upload, KFS review, Aadhaar e-sign, submit for disbursement. | RO | Submit for disbursement. | Confirm e-sign provider and co-borrower rule. |

## Product Selection Rules

| Product | Applicant requirement from rough doc | Downstream behavior | Confidence | Open questions |
| --- | --- | --- | --- | --- |
| Super/Welcome Loan | Minimum 2 applicants: Primary Borrower + Co-Borrower. Applicant 3 optional. | Standard underwriting and automated bureau calls. | Medium | Confirm whether Super and Welcome are one product or separate products. |
| Smart Loan | Minimum 1 applicant. Applicant 2 optional. Applicant 3 hidden/disabled. | Business KYC, business-only loan requirement, RO sends for PD after Step 9. | Medium | Confirm current step count and exact optional co-borrower rule. |
| Micro LAP | Minimum 2 applicants plus optional additional applicants. | Adds asset/property collateral verification after residence checks. | Low | Rough doc wording says "2 applicants + 2 optional"; validate. |

## Key Product Rules

| Area | Rule | Source | Confidence | Notes |
| --- | --- | --- | --- | --- |
| Applicant age | Applicant 1 must be at least 22 years old. Applicant 2 must be at least 18 years old. | Rough documentation | Medium | Confirm if product-specific. |
| Mobile verification | Applicant mobile number must be 10 digits and verified by OTP. | Rough documentation | Medium | Confirm OTP length and consent language. |
| Duplicate mobile | Existing active file or rejection in last 90 days blocks OTP generation. | Rough documentation | Low | Needs policy and code validation. |
| Area serviceability | 6-digit pincode is checked against operational serviceability master. | Rough documentation | Medium | Confirm micro-area rule. |
| KYC | Any 2 KYC documents are required. | Rough documentation | Low | Full KYC section was large; needs dedicated validation. |
| Bureau score | Score below 600 triggers manual underwriting review or block path. | Rough documentation | Low | Confirm product-specific bureau policy. |
| Overdue amount | Non-zero current unpaid overdue can reject/block application. | Rough documentation | Low | Needs credit policy review. |
| Loan amount | Loan amount must be in multiples of 5,000. | Rough documentation | Medium | Confirm product exceptions. |
| Loan purpose split | Itemized purpose total must equal target loan amount unless product-specific min/max applies. | Rough documentation | Medium | Vehicle has min/max mentioned. |
| Family members | Applicants cannot be added again as family members. | Rough documentation | Medium | Confirm duplicate matching method. |
| Family expenses | Blank expense fields are not accepted; enter 0 where none. | Rough documentation | Medium | Confirm all required expense fields. |
| Additional docs | Step can be skipped with zero documents. | Rough documentation | Medium | Confirm product/role exceptions. |
| File upload | Allowed file types: `.png`, `.jpg`, `.jpeg`, `.pdf`; max size 10 MB. | Rough documentation | Medium | Confirm current app limits. |
| BRE | Any failed BRE rule disables Proceed and moves to exception queue. | Rough documentation | Low | Needs tech and credit policy validation. |
| Offer acceptance | Credit team generates offer; RO confirms the offer with customer. Confirming offer locks loan terms and unlocks NACH registration. | Rough documentation | Medium | Confirm request-change behavior. |
| NACH | Proceed requires a valid digital mandate or uploaded physical mandate. | Rough documentation | Medium | Confirm accepted modes and provider. |
| E-sign | OSV upload and borrower/co-borrower e-sign are required before submit for disbursement. | Rough documentation | Medium | Confirm single-applicant products. |

## Screen Inventory

| Screen/module | Purpose | Entry point | Main actions | User-visible states | Figma link |
| --- | --- | --- | --- | --- | --- |
| Product selection | Choose product vertical. | Home > New Loan Application. | Select product card. | Product selected, unavailable product TBD. | TBD |
| Step index/checklist | Shows mandatory/optional/locked/completed steps. | After product selection. | Fill details, view details, update. | Locked, active, WIP, completed. | TBD |
| Mobile verification | Verify applicant mobile and consent. | Applicant profile step. | Generate OTP, verify OTP, resend OTP. | Invalid mobile, duplicate mobile, OTP verified. | TBD |
| Area serviceability | Validate residence pincode/micro-area. | Applicant verification step. | Enter pincode, micro-area, next. | Serviceable, unserviceable. | TBD |
| KYC/Aadhaar verification | Capture and verify identity documents. | Applicant profile. | Upload/scan/select documents. | Pending, verified, failed. | TBD |
| Credit-O-Meter | Show household bureau/risk summary. | After applicant checks. | Review metrics, apply/proceed. | Pass, review, reject/block. | TBD |
| Reapply review | Show existing InPrime loan summary. | Existing applicant detected. | Add remark, proceed. | Existing history found. | TBD |
| Loan requirement | Capture amount, tenure, purpose. | Loan requirement step. | Select loan type, enter amount, split purpose. | Invalid amount, incomplete split, ready. | TBD |
| Residence details | Capture current address and housing details. | Residence step. | Select/add address, capture photo, choose ownership. | Serviceable, ownership-specific fields. | TBD |
| Family details | Capture household members, expenses, demographics. | Family step. | Add/delete member, enter expenses, demographics. | Empty state, member added, delete confirmation. | TBD |
| Bank statement/BSA | Upload statements and review bank analysis. | Bank statement step. | Upload via AA/ePDF/net banking/passbook, edit transaction type, add remark. | No upload, processing, successful, failed, analysis completed. | TBD |
| Disbursement bank account | Capture beneficiary account and verify. | Post-assessment step. | Add account, enter IFSC/account, validate. | IFSC valid/invalid, account match/mismatch, penny-drop success/fail. | TBD |
| Additional documents | Optional upload of supporting documents. | After disbursement account. | Upload/delete/skip documents. | Empty, uploaded, file rejected. | TBD |
| BRE | Final rule check. | After additional docs. | Review rules, proceed if passed. | Passed, failed, processing. | TBD |
| Loan offer | View pending review or sanctioned pricing. | After credit review. | Apply, request change, confirm. | Under review, active sanction, accepted. | TBD |
| Repayment/NACH | Create digital/physical mandate. | After offer acceptance. | Confirm bank, create mandate, retry, upload physical mandate. | Pending, error, mandate created. | TBD |
| Agreement e-sign | Upload OSV, review KFS, e-sign, submit. | After NACH. | Refresh status, upload OSV, e-sign, submit. | Document generation in progress, OSV uploaded, e-sign pending/completed. | TBD |

## Acceptance Criteria

- RO can start a new loan application from the home dashboard.
- Product selection configures the correct applicant requirements and step checklist.
- Mandatory applicant age, mobile, KYC, and serviceability rules block progression when failed.
- Optional steps are clearly marked and can be skipped only where product rules allow.
- Loan amount and purpose split validation prevent invalid financing requests.
- Residence, family, bank statement, and disbursement details show clear empty, success, failure, and blocked states.
- BRE clearly displays passed/failed rule categories and blocks progression on failure.
- Offer acceptance requires explicit confirmation and then locks terms.
- NACH registration cannot proceed without a valid digital mandate or physical fallback upload.
- Agreement e-sign cannot submit for disbursement until all required applicants/signatures are complete.

## Mismatches or Contradictions

| Issue | Sources that disagree | Impact | Status |
| --- | --- | --- | --- |
| Product step counts vary across rough doc sections. | Product selection/multi-applicant sections vs later module numbering. | Flow doc may be wrong if not validated against current app. | Open |
| SMART Loan applicant requirement wording says minimum 1 applicant but also says "Primary Borrower + Co-Borrower" in one table. | Rough documentation internal wording. | Confuses mandatory co-borrower rule. | Open |
| Some technical/provider/API details appear in product rough doc. | Manager rules say detailed API truth belongs in tech/provider docs. | Need Dileepan to move/validate. | Open |

## Open Questions

| Question | Owner | Needed from | Status |
| --- | --- | --- | --- |
| What is the exact current step list for each product? | Arnav/Dileepan | Product + engineering | Open |
| Which modules are live, partially live, or planned? | Arnav | Product/manager | Open |
| What are the canonical status codes shown in the app versus stored in backend? | Arnav/Dileepan | Engineering | Open |
| What are the exact product-wise tenure limits for Super, Welcome, Smart, MLAP, Top-Up, and Repeat? | Arnav | Credit/product | Open |
| Which KYC documents count toward the "Any 2 KYCs" rule? | Arnav | Product/compliance | Open |
| Which providers power OTP, KYC, bureau, BSA, penny-drop, NACH, and e-sign? | Dileepan | Engineering | Open |
| What is the approved copy for all warning/error states? | Arnav | Product/design | Open |
| Which screenshots/recordings can be safely linked without PII? | Arnav | Manager/security | Open |
