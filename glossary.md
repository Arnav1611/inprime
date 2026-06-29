# Glossary

Canonical for shared product, business, operational, and engineering vocabulary used in the internal source of truth.

Owner: Arnav  
Status: draft  
Last updated: 2026-06-29  
Primary source areas: New Loan Application, Staff Login, Home Dashboard, Leads, All Loan Files, Rework, Tech Support Tickets, Loan Pricing, Product Variants, RBAC, Product Constructs

## Usage Notes

- This glossary should reduce confusion across product, flows, tech, and provider docs.
- If a term is not confirmed, keep it as draft and add it to Open Terminology Questions.
- Do not add customer PII, raw provider payloads, secret values, or production screenshots.
- Product docs own product meaning and business usage. Tech docs own implementation details.

## Core Product Terms

| Term | Meaning | Source area | Confidence | Notes |
| --- | --- | --- | --- | --- |
| Staff App | Internal application used by InPrime staff for login, loan application work, dashboards, and support actions. | Rough documentation | Medium | Confirm official app name and whether "Xpress Flow" is the app name or module name. |
| Xpress Flow | Internal flow/app documented by Arnav for staff-side loan and operational workflows. | Rough documentation | Medium | Confirm canonical spelling and scope. |
| PRD | Product Requirements Document describing feature intent, scope, business rules, and acceptance criteria. | Manager brief | High | Product docs should link canonical PRDs when available. |
| Figma | Design source for screens, UI states, and user-visible behavior. | Manager brief | High | Link exact frames where possible, not only the file-level link. |
| Feature Intent | The reason a feature exists and the product outcome it should support. | Manager brief | High | Product docs should state this clearly. |
| Screen Inventory | List of screens, entry points, actions, states, and Figma references for a feature. | Manager brief | High | Owned in product docs. |
| Business Rule | Product rule that controls validation, eligibility, status change, visibility, or user action. | Manager brief | High | Should be written without implementation assumptions. |
| Acceptance Criteria | Reviewable conditions used to decide whether the feature is complete and working as expected. | Manager brief | High | Keep testable and specific. |
| Flow | End-to-end sequence of user actions, system actions, handoffs, statuses, and exceptions. | Manager brief | High | `flows/` owns sequencing and handoffs. |
| Actor | Person or system participating in a flow. | Manager brief | High | Examples: staff user, RO, applicant, support team, backend system. |
| API Touchpoint | API involved in a user or system journey. | Manager brief | High | Flow docs may mention touchpoints; detailed API truth belongs in `tech/`. |
| State Transition | Change from one meaningful status/state to another after a user or system action. | Manager brief | High | Flow docs should capture trigger and resulting status. |
| Source Material | PRD, Figma, repo file, existing doc, runbook, stakeholder clarification, or approved summary used as evidence. | Manager brief | High | Every meaningful doc should cite source material. |
| Open Question | Known unknown that should be confirmed instead of guessed. | Manager brief | High | Use this whenever product intent, Figma, and code are unclear. |
| Mismatch | Difference between product intent, Figma, existing documentation, or implemented behavior. | Manager brief | High | Document explicitly instead of hiding it. |

## Roles And Users

| Term | Meaning | Source area | Confidence | Notes |
| --- | --- | --- | --- | --- |
| Staff User | Internal user who logs into the staff app to perform assigned work. | Staff Login | Medium | Confirm role types and permission groups. |
| RO | Relationship Officer. Staff role involved in borrower interaction, loan application initiation, field/customer workflows, and post-offer customer follow-up. | Loan Application | High | In the general loan flow, RO works till Occupation Profiling, then later handles NACH/e-sign/customer-facing post-offer steps after credit offer generation. |
| AM | Area Manager. Staff role that can view files of reporting ROs, coordinate area-level actions, do PD himself, or assign PD to another eligible person where allowed. | RBAC / Rework | High | AM/PD owns Occupation & Income Assessment through BRE in the general flow. |
| PD | Personal Discussion role/capability for assigned PD offices. | RBAC / Rework | High | AM/PD person handles Occupation & Income Assessment through BRE and sends the file to credit. |
| CM | Credit Manager / credit role mentioned in role lifecycle activities. | RBAC | Low | Confirm official expansion and permissions. |
| Applicant | Customer/borrower whose loan application is being created. | Loan Application | High | Applicant 1 is the primary applicant unless product confirms otherwise. |
| Applicant 1 | Primary applicant/borrower in the Super/Welcome Loan application flow. | Loan Application | High | Mandatory in the current loan application flow. |
| Applicant 2 | Co-applicant captured after Applicant 1 in the Super/Welcome Loan flow. | Loan Application | High | Mandatory for Super/Welcome; optional for SMART; for Top-Up/Repeat, existing applicants remain from the core loan. |
| Applicant 3 | Completely optional additional applicant captured after Applicant 2 when applicable. | Loan Application | High | Can be skipped without reason. |
| Co-applicant | Additional person linked to the loan application for eligibility or household assessment. | Loan Application | Medium | Confirm exact product rule. |
| Support Tech Team | Internal team/person responsible for triaging and resolving staff-raised support tickets. | Tech Support Tickets | High | RO/AM can reopen tickets if the issue persists. |
| Credit Analyst | Credit user who reviews loan files in NOVA, especially Level 0 review. | Rework / Credit Review | High | Can accept/assign a case, review details, edit where permitted, and send rework where allowed. |
| Credit Team | Team that reviews credit files, owns credit decisions, and generates/approves loan offers where applicable. | Loan Application / Rework | High | Credit generates/approves offer after AM/PD completes BRE. |
| Operations / Opex | Operations function that handles ready-for-disbursement and disbursement actions after final customer steps are complete. | Loan Application | Medium | User clarified Opex/operations triggers disbursement; official expansion/name still needs confirmation. |
| Product Stakeholder | Person who can confirm product intent, business rules, and expected user behavior. | Manager brief | High | Add stakeholder names in `stakeholders.md`. |
| Engineering Stakeholder | Person who can confirm APIs, code paths, implementation rules, and logs. | Manager brief | High | Dileepan to validate. |

## Feature Terms

| Term | Meaning | Source area | Confidence | Notes |
| --- | --- | --- | --- | --- |
| New Loan Application | Staff app feature used to create a new loan application from product selection through application completion or rejection. | Loan Application | High | Product variants documented so far include Super/Welcome, SMART, and MLAP. |
| Super Loan | Loan product type included in New Loan Application documentation. | Loan Application | High | Current documented amount range is Rs. 80,000 to Rs. 3 lakh. |
| Welcome Loan | Loan product type included in current New Loan Application documentation scope. | Loan Application | High | Amount range: Rs. 80,000 to Rs. 1.5 lakh. |
| Festival Loan | Product variant shown in the latest product-limit screenshot. | Product Variants | Medium | Amount range: Rs. 25,000 to Rs. 40,000; detailed flow is not yet documented. |
| Leads | Staff app module used to view, search, filter, contact, reject, create, or convert lead records. | Leads | High | Top-Up Loan starts from Leads > Top-up tab. |
| Lead Card | Card-style record shown in Leads with customer/product/context fields and action menu. | Leads | High | Do not reproduce real customer names/mobile numbers in docs. |
| My Leads | Leads manually added and managed by an RO through the plus button for self-sourced field leads. | Leads | High | Sorted by planned visit date. |
| Digital Leads | Leads imported from marketing/campaign/call-centre sources, including WhatsApp Credit-O-Meter and contact-centre leads. | Leads | High | Uses Prime/Bureau star indicators. |
| Retarget Leads | Deprecated lead concept for old rejected applications that might have been re-approached later. | Leads | High | Latest validation says Retarget is no longer in use; retained only as historical reference. |
| Lead Source | Source channel for a lead, such as Customer Referral, Doorstep Brochure, Canopy Marketing, Van Marketing, Contact Centre, or WhatsApp COM. | Leads | High | Contact Centre and WhatsApp COM are default upload sources, not manual dropdown values. |
| Lead Dedupe | Mobile-number based duplicate check used during manual lead add and CRM upload. | Leads | High | Mobile number is primary dedupe key. |
| Lead Reallocation | AM action to move a lead to another active RO within the same AO. | Leads | High | Also applies during RO resignation/assigned RO changes. |
| WhatsApp COM | WhatsApp Credit-O-Meter lead source/campaign flow. | Leads | High | If it appears as COM later, it appears in My Leads only as COM lead. |
| Customer Referral | Lead source where staff selects customer referral and then captures referred-by name and mobile number. | Leads | High | Referral details are entered after selecting the Customer Referral source. |
| Top-Up Loan | Loan product for eligible existing borrowers, accessed through Leads > Top-up tab. | Product Variants | High | Current documented amount range is Rs. 40,000 to Rs. 2 lakh; no rework is allowed for Top-Up. |
| Top-Up Lead | Existing-borrower lead shown in the Leads Top-up tab with customer, core-loan, EMI-paid, and OSP context. | Top-Up Loan | High | Staff can call, reject, start application, or get direction. |
| Open Ticket Size | Top-Up eligibility class for stronger profiles. | Top-Up Loan | Medium | Earlier notes mention 6 EMIs completed, HH score 650+, and income Rs. 40,000+; current product limit is Rs. 40,000 to Rs. 2 lakh. |
| Limited Ticket Size | Top-Up eligibility class for lower income or mid HH-score profiles. | Top-Up Loan | Medium | Earlier notes mention income below Rs. 40,000 and HH score 600-650; current product limit is Rs. 40,000 to Rs. 2 lakh. |
| OSP | Outstanding principal / outstanding exposure shown in Top-Up lead context. | Top-Up Loan | Medium | Confirm official expansion used in app: screenshot shows Current InPrime OSP. |
| Core Loan Utilisation | Required Loan Requirement field where staff captures how the existing/core loan amount has been used. | Top-Up Loan | High | Visible on Top-Up Loan Requirement screenshot. |
| FOIR | Fixed Obligation to Income Ratio used to assess repayment capacity. | Top-Up / Repeat / Credit | Medium | Current known cutoffs: Top-Up 50%, Repeat 55%; detailed formula belongs to credit/tech docs. |
| Wallet Share | Share of customer obligations/exposure considered during Top-Up assessment. | Top-Up Loan | Low | Latest note references obligations closed in the span of 8 months; calculation needs confirmation. |
| Repeat Loan | Existing-customer loan product for borrowers eligible after clean repayment history, currently shown under Leads > Top-up section but marked as Repeat. | Repeat Loan | High | Current documented amount range is Rs. 40,000 to Rs. 3 lakh; no rework is allowed for Repeat. |
| Core Loan | Original Super/Welcome or base loan from which Top-Up/Repeat eligibility may be assessed. | Top-Up/Repeat | Medium | For Repeat, core loan must be settled and remaining OSP may be adjusted from Repeat amount. |
| EMI Bounce | Failed or bounced EMI payment used in Repeat eligibility and risk checks. | Repeat Loan | Medium | Repeat requires 12 months EMI paid without bounce. |
| Retention Loan | Existing-customer product such as Top-Up or Repeat used to retain borrowers with additional/new credit after repayment history. | Top-Up/Repeat | Medium | Stakeholder note recommends automating retention eligibility through BRE. |
| Repeat Cohort | Batch/group of customers considered for Repeat eligibility in a given cycle. | Repeat Loan | Medium | A recent 10th cohort issue involved customers whose eligibility should have started next month. |
| Tenure-Percentage Eligibility | Eligibility rule based on how much of the original loan tenure/repayment cycle has been completed. | Repeat Loan | Low | Earlier manual retention eligibility logic caused cohort issues; exact formula needs credit/engineering validation. |
| Repeat Eligibility | Repeat Loan rule requiring 12 calendar months plus Rs. 40k OSP condition, otherwise 16 months standard. | Repeat Loan | High | Core loan must be settled; Top-Up and Repeat can run simultaneously. |
| MLAP / Micro LAP | Micro Loan Against Property; collateral-backed product variant selected from New Loan Application. | Product Variants / MLAP | High | Amount range: Rs. 4 lakh to Rs. 10 lakh; tenure 36M to 96M. |
| Property Owner | Person who owns or co-owns the property offered for MLAP collateral. | MLAP | High | All property owners/co-owners must be part of the MLAP application. |
| Property Documentation | Documents captured for MLAP collateral review, such as deed/title deed, Khata/Khatha, tax paid receipt, encumbrance certificate, affidavit, and family tree certificate. | MLAP | Medium | Final mandatory/conditional list needs confirmation. |
| LTV | Loan to Value, used in MLAP decisioning to compare sanctioned loan amount with property value. | MLAP | Medium | Training PPT says loan can be sanctioned up to 70% of property value. |
| MOTD | Mortgage by deposit of title deeds / mortgage creation step referenced in MLAP rejection and operations flow. | MLAP/operations | Low | Confirm official expansion and process owner. |
| Encore | LMS/system used for MLAP booking. | MLAP/tech | Medium | Existing applicants should map to existing Encore clients where mapping exists. |
| Finflux | Existing LMS/core system referenced for client IDs and migration/mapping to Encore. | MLAP/tech | Medium | Detailed integration truth belongs in tech/provider docs. |
| Clients Mapping | Mapping source used to connect existing Finflux clients to Encore clients for MLAP booking. | MLAP/tech | Medium | Exact owner and failure handling need engineering/operations validation. |
| SMART Loan | Business-oriented loan product variant with business KYC and nominee requirements. | Product Variants | High | Amount range: Rs. 50,000 to Rs. 3 lakh. |
| Business KYC | SMART Loan stage used to capture business identity through GST, Shop & Establishment, Udyam, or Other Business KYC. | SMART Loan | High | Comes after identity KYC and Prime Test; at least one Business KYC is mandatory for credit bureau check. |
| Bank & QR Statement | SMART Loan statement stage containing Bank Statement and QR Statement sub-stages. | SMART Loan | High | Both are required in Phase 1 per SMART attachment. |
| QR Statement | SMART Loan statement input for business QR/digital collections. | SMART Loan | High | Mandatory in current SMART Loan flow. |
| Other Business KYC | Manual Business KYC route for business documents when API-based GST/Shop/Udyam is not used. | SMART Loan | Medium | Final dropdown list needs validation. |
| Applicant 2 Skipped | SMART Loan state where optional co-applicant is skipped. | SMART Loan | High | Insurance Nominee Details become prerequisite before loan offer because there is no co-borrower. |
| Insurance Nominee Details | SMART Loan form collected before InPrime Loan Offer when Applicant 2 is skipped / there is no co-borrower. | SMART Loan | High | Required fields: nominee name, gender, DOB, marital status, relationship with applicant, and mobile number. |
| Informal Prime Customer | Target customer segment for Super Loan, generally informal economy households with proven credit track record and digital adoption. | Super Loan | Medium | Product/credit to validate exact segment rules. |
| Pre-closure | Operational process where customer closes loan before normal maturity after approval, debit, LMS closure, and NOC sharing. | Runbooks | Medium | Current runbook drafted for Super Loan. |
| NOC | No Objection Certificate shared after successful pre-closure/loan closure. | Runbooks | Medium | Confirm template and delivery channel. |
| AO | Area Office. Used for staff assignment, movement, and pre-closure email details. | RBAC/operations | Medium | Confirm exact system field name. |
| Product Selection | Step where the staff user selects the loan product before starting the application flow. | Loan Application | Medium | Confirm exact screen name. |
| Target Segment Checklist | Eligibility checklist used early in the loan application journey. | Loan Application | Medium | Rough doc also references Prime Test. |
| Prime Test | Eligibility/target segment check used in the loan application flow before SMART Business KYC. | Loan Application / SMART Loan | High | Final visible label confirmed as Prime Test. |
| Area Serviceability | Check that determines whether the applicant's area can be serviced. | Loan Application | Medium | Confirm data inputs and failure handling. |
| KYC | Know Your Customer information and checks required during onboarding/application. | Loan Application | High | Product docs should capture visible steps; provider details belong outside product. |
| Identity KYC | Applicant identity verification using approved identity documents. | Loan Application | Medium | SMART Loan requires any 2 from Aadhaar, PAN, Driving Licence, and Voter ID. |
| Form 60 | Declaration used where PAN is not provided/available. | Loan Application | Medium | In SMART Loan, PAN or Form 60 is required. |
| Aadhaar Validation | Step where Aadhaar details are validated for an applicant. | Loan Application | Medium | Do not document raw Aadhaar data. |
| Aadhaar Data Fetch | Step where Aadhaar-linked applicant information is fetched after successful validation. | Loan Application | Medium | Provider-specific truth belongs in provider docs. |
| OSV | Original Seen and Verified, a verification step for customer-provided documents. | Loan Application | Medium | Confirm how OSV is shown in the app. |
| Additional Documents | Supporting documents captured after Aadhaar/KYC steps. | Loan Application | Medium | Confirm required document list. |
| Profile Image | Applicant photo captured during the application journey. | Loan Application | Medium | Confirm capture and retake rules. |
| Profile Verify | Verification step after profile image capture. | Loan Application | Medium | Confirm exact user-visible behavior. |
| Credit Bureau Check | Credit check performed for an applicant during the loan journey. | Loan Application | Medium | Product docs should describe user-visible outcome only. |
| AIP | Approval in Principle or preliminary approval stage after required checks. | Loan Application | Low | Confirm official expansion and decision meaning. |
| Household Credit-O-Meter | Household-level credit assessment step shown in the loan journey. | Loan Application | Medium | Confirm exact display name and interpretation. |
| Loan Requirement | Screen/step where requested loan need, amount, or related details are captured. | Loan Application | Medium | Confirm exact fields. |
| Loan Purpose | Reason for which the applicant wants the loan. | Loan Application | Medium | Confirm allowed values. |
| Loan Pricing Generator | Internal pricing module used to estimate or generate loan pricing values such as EMI, fees, insurance, and disbursement amount. | Loan Pricing | Medium | App docs may call this Loan Pricing Calculator. |
| Loan Pricing Calculator | Visible dashboard/module label for the pricing tool. | Loan Pricing | Medium | Confirm final naming with product/design. |
| EMI | Equated Monthly Instalment shown or calculated as part of loan pricing. | Loan Pricing | Medium | Formula/source needs confirmation. |
| ROI | Rate of Interest used in pricing or offer calculation. | Loan Pricing | Low | Confirm exact label and whether shown to staff. |
| Net Disbursement Amount | Amount expected to be disbursed after fees, insurance, or deductions if applicable. | Loan Pricing | Low | Confirm formula and display rules. |
| Residence Details | Applicant household/residence details captured during the flow. | Loan Application | Medium | Confirm mandatory fields. |
| Family Details | Family/household information captured during the flow. | Loan Application | Medium | Confirm mandatory fields and relation options. |
| Occupation Entry | Employment or occupation information captured for the applicant. | Loan Application | Medium | Confirm whether this applies to each applicant or household. |
| Income Assessment | Product step where income information is evaluated. | Loan Application | Medium | Confirm formulas and visible decision rules with product/tech. |
| Disbursement Bank Account | Bank account details used for loan disbursement. | Loan Application | High | Must be handled carefully as sensitive financial data. |
| Final BRE Run | Final business rules/eligibility evaluation before final offer or backend review. | Loan Application | Medium | Confirm exact trigger and visible status. |
| BRE | Business Rules Engine or automated decisioning logic. | Loan Application | Medium | Confirm official expansion and where product rules end versus tech logic starts. |
| Final Loan Offer | Final offer presented after approval checks. | Loan Application | Medium | Confirm offer fields and acceptance rules. |
| Offer Expiry | Time after offer generation when the offer is no longer valid. | Loan Application | High | Current validated rule: offer expires 7 days after generation. |
| Repayment Registration | Step where repayment mode/mandate setup is completed. | Loan Application | Medium | Product doc should capture visible path only. |
| NACH | Repayment mandate method used for automated debit. | Loan Application | Medium | Provider/bank integration details belong outside product. |
| UPI Autopay | UPI-based repayment registration option. | Loan Application | Medium | Confirm availability and fallback rules. |
| Document E-Sign | Digital signing step for loan agreement or related documents. | Loan Application | Medium | Provider-specific truth belongs in provider docs. |
| Ready for Disbursement | State where application is approved and ready for disbursement processing. | Loan Application | Medium | Confirm exact status label. |
| Disbursement | Loan amount transfer process after approval and signing. | Loan Application | High | Product docs should describe visible states and operational outcomes. |
| Opex | Operations team/function that triggers disbursement in the current loan flow. | Loan Application | Medium | Confirm official internal expansion/name. |
| Staff Login | Feature that allows internal staff users to authenticate and enter the staff app. | Staff Login | High | Current login method is phone number plus 6-digit OTP verification. |
| Home Dashboard | First authenticated staff workspace after successful login, containing navigation cards such as New Loan Application, All Loan Files, Tech Support Tickets, Leads, Loan Pricing Calculator, and InPrime Leaderboard. | Staff Login / Home Dashboard | High | Current validated order is New Loan Application, All Loan Files, Tech Support Tickets, Leads, Loan Pricing Calculator, InPrime Leaderboard. |
| Dashboard Card | Home-screen navigation option that routes staff to a module such as Leads or All Loan Files. | Home Dashboard | High | Current validation says listed cards are accessible. |
| InPrime Leaderboard | Dashboard module for staff or team performance ranking. | Home Dashboard | Medium | User confirmed it is visible/live; metric definitions still need confirmation. |
| Mobile OTP Login | Login method where a staff user's mobile number is verified through a 6-digit OTP. | Staff Login | High | Current canonical staff login method. |
| Device Binding | Rule where a staff login/session may be tied to an approved device. | Staff Login | Low | Confirm whether implemented and user-visible. |
| Session | Authenticated app usage period after login. | Staff Login | Medium | Confirm expiry and logout behavior. |
| Tech Support Ticket | Internal ticket raised by staff for app, application, document, communication, or disbursement issues. | Tech Support Tickets | High | Support tech team owns triage/resolution; RO/AM can reopen. |
| Ticket ID | Unique identifier assigned to a support ticket. | Tech Support Tickets | High | Confirm exact format. |
| Issue Type | Category selected while raising a support ticket. | Tech Support Tickets | High | Confirm final dropdown values. |
| Issue Detail | Sub-category or more specific issue selected after issue type. | Tech Support Tickets | Medium | Confirm dependency rules. |
| Brief Note | Free-text explanation entered by staff while raising a ticket. | Tech Support Tickets | High | Confirm length and validation rules. |
| Attachment | File or screenshot uploaded with a support ticket. | Tech Support Tickets | High | Personal information should not be shared in attachments. |
| Reopen | Action used when a resolved ticket needs additional work. | Tech Support Tickets | High | RO/AM can reopen tickets. |
| All Loan Files | Staff app module used to view, search, filter, and act on loan files across lifecycle buckets. | All Loan Files | High | Includes in-progress, rework, rejected, expired, disbursed, and other role-permitted queues. |
| In-Progress Files | Active loan files that are still being completed, reviewed, or corrected. | All Loan Files | High | Rough source confirms sorting, search, and status filtering. |
| Rework Files | Files sent back from backend, FCU, credit, or operations for correction. | All Loan Files | High | Exact stage, screen, document/data point, and backend remarks should be shown. |
| Application Rework | Feature that lets credit/review teams send a loan application back to the responsible RO/AM/PD owner for correction before review can continue. | Rework | High | Rework is not allowed for Top-Up and Repeat. |
| NOVA | Internal platform used by credit users to review loan applications, assign cases, inspect details, and send rework. | Rework / Credit Review | Medium | Product docs should mention NOVA where required, without documenting technical implementation. |
| Credit Queue | NOVA queue showing files waiting for credit review assignment. | Rework / Credit Review | High | Screenshot shows Credit Queue tab under All Loan Files. |
| My Tasks | NOVA tab showing cases assigned to the current credit user. | Rework / Credit Review | High | Screenshot shows Credit Assessment and Level 0 on task card. |
| Level 0 | First credit review level where credit analyst accepts/assigns, checks every detail, edits where allowed, and can send rework. | Rework / Credit Review | High | User validated Level 0 responsibility. |
| Level 1 | Final credit review level after Level 0 where the reviewer checks the file and approves the loan for offer generation where eligible. | Rework / Credit Review | High | User validated Level 1 responsibility. |
| Rework Summary | Staff-app tab showing requested rework items and their status, such as Pending or Success. | Rework | High | Visible in screenshots. |
| Backend Comment | Reviewer comment shown on the staff-app target screen so the user knows what to correct. | Rework | High | Must not be vague; supports correct rework completion. |
| FOS Rework | Rework item shown to field/staff app users for correction. | Rework | Medium | FOS and Credit rework can coexist. |
| Credit Rework | Credit-side rework item shown in NOVA/review flow. | Rework | Medium | FOS and Credit rework can coexist. |
| Backend Credit Review | Queue/review state for files routed to backend/manual credit review after final BRE. | All Loan Files | Medium | Role visibility and exact bucket label need confirmation. |
| Rejected Files | Terminal queue/tab for rejected applications. | All Loan Files | High | Should show rejection reason where role permits; read-only. |
| Expired Files | Terminal queue/tab for applications expired by cut-off/TTL rule. | All Loan Files | Medium | Cut-off rule needs confirmation. |
| Disbursed Files | Terminal queue/tab for successfully disbursed applications. | All Loan Files | High | Read-only archive. |

## Status And State Terms

| Term | Meaning | Source area | Confidence | Notes |
| --- | --- | --- | --- | --- |
| ApplicationIDGenerated | Application record/id is created. | Loan Application | Medium | Confirm exact casing and trigger. |
| AppInitiated | Application flow has started. | Loan Application | Medium | Rough doc also references mobile verification statuses. |
| App1MobileVerified | Applicant 1 mobile verification is complete. | Loan Application | Medium | Confirm whether this is separate from AppInitiated. |
| TargetSegmentVerified | Target segment/eligibility checklist is completed successfully. | Loan Application | Medium | Confirm exact status label. |
| AreaServiceable | Applicant area is serviceable. | Loan Application | Medium | Confirm failure status for non-serviceable area. |
| LoanReqSubmitted | Loan requirement details are submitted. | Loan Application | Medium | Confirm exact trigger. |
| App1AadhaarSubmitted | Applicant 1 Aadhaar step submitted. | Loan Application | Medium | Do not document real Aadhaar values. |
| App1AddDocSubmitted | Applicant 1 additional document step submitted. | Loan Application | Medium | Confirm if document verification is separate. |
| App1PhotoSubmitted | Applicant 1 profile photo submitted. | Loan Application | Medium | Confirm if liveness or verification has a separate status. |
| App1CBChecked | Applicant 1 credit bureau check completed. | Loan Application | Medium | Confirm output labels shown to user. |
| AIP1Completed | Applicant 1 AIP stage completed. | Loan Application | Low | Confirm official meaning. |
| HHCreditMeterGenerated | Household Credit-O-Meter generated. | Loan Application | Medium | Confirm decision implications. |
| ResidenceDetailsSubmitted | Residence details submitted. | Loan Application | Medium | Confirm exact status label. |
| FamilyDetailsSubmitted | Family details submitted. | Loan Application | Medium | Confirm exact status label. |
| OccupationBRERunCompleted | Occupation/income BRE run completed. | Loan Application | Medium | Confirm trigger and failure handling. |
| DisbBankAccAdded | Disbursement bank account added. | Loan Application | Medium | Confirm exact status label. |
| MainBRERunCompleted | Main/final BRE run completed. | Loan Application | Medium | Confirm result statuses. |
| MainBREResultNotApproved | Main BRE result is not approved. | Loan Application | Medium | Confirm whether this routes to backend review or rejection. |
| ApplicationBackendReviewSubmitted | Application submitted for backend review. | Loan Application | Medium | Confirm review owner and SLA. |
| ApplicationReworkRequired | Application sent back for correction/rework. | Loan Application | Medium | Confirm who can edit and resubmit. |
| ApplicationRejected | Application rejected. | Loan Application | Medium | Confirm rejection reasons and visibility. |
| ApplicationExpired | Application expired due to time or policy rules. | Loan Application | Medium | Confirm expiry duration and notifications. |
| ApplicationFinalOfferGenerated | Final offer generated. | Loan Application | Medium | Confirm offer acceptance path. |
| ApplicationFinalOfferSubmitted | Final offer accepted/submitted. | Loan Application | Medium | Confirm exact user action. |
| RepayModeSubmitted | Repayment mode selected/submitted. | Loan Application | Medium | Confirm options. |
| RepaymentRegistrationCompleted | Repayment registration completed. | Loan Application | Medium | Confirm mandate success/failure states. |
| LoanAgreementSigned | Loan agreement signed. | Loan Application | Medium | Confirm signing states and retries. |
| FinalApplicationApprovedRFD | Final application approved and ready for disbursement. | Loan Application | Medium | Confirm official display label. |
| DisbursementAttempted | Disbursement was attempted. | Loan Application | Medium | Confirm retry rules. |
| DisbursementFailed | Disbursement attempt failed. | Loan Application | Medium | Confirm operational handling. |
| DisbursementSuccess | Disbursement completed successfully. | Loan Application | Medium | Confirm final loan status after success. |
| OPEN | Ticket is created and waiting for action. | Tech Support Tickets | Medium | Confirm exact capitalization. |
| WIP | Ticket is work in progress. | Tech Support Tickets | Medium | Confirm whether visible to staff users. |
| RESOLVED | Ticket is marked resolved. | Tech Support Tickets | Medium | Confirm closure and reopen rules. |

## Ticket Issue Terms

| Term | Meaning | Source area | Confidence | Notes |
| --- | --- | --- | --- | --- |
| File Stuck | Ticket issue where a loan/application file is unable to move to the next expected step. | Tech Support Tickets | Medium | Confirm examples and required fields. |
| Application Error | Ticket issue for app errors, failed actions, or unexpected screen behavior. | Tech Support Tickets | Medium | Confirm whether error code is required. |
| Agreement/Document Issue | Ticket issue related to document generation, viewing, signing, or agreement problems. | Tech Support Tickets | Medium | Confirm final label. |
| SMS/WhatsApp Issue | Ticket issue related to customer/staff communication delivery. | Tech Support Tickets | Medium | Confirm if both channels are supported in current scope. |
| Disbursement Issue | Ticket issue related to disbursement failure, delay, or incorrect state. | Tech Support Tickets | Medium | Confirm escalation owner. |
| Data Correction/Wrong Data | Ticket issue for incorrect data that needs correction. | Tech Support Tickets | Medium | Confirm allowed fields and approval rules. |

## Compliance And Data Terms

| Term | Meaning | Source area | Confidence | Notes |
| --- | --- | --- | --- | --- |
| PII | Personally identifiable information. | Manager brief | High | Must not be copied into docs. |
| Masked Aadhaar | Aadhaar displayed or stored in masked form. | Loan Application | High | Never document full Aadhaar numbers. |
| Protected Aadhaar Reference | Internal reference/token to Aadhaar data instead of raw Aadhaar values. | Loan Application | Medium | Confirm exact internal handling with tech. |
| Audit Trail | Record of who did what, when, and from where. | Product/flows | High | Useful for login, loan edits, and ticket actions. |
| Geolocation | Location captured during certain staff/customer actions. | Loan Application | Medium | Confirm where mandatory and how it is displayed. |
| Override Flag | Marker showing that a normal rule was overridden by an authorized user/system. | Loan Application | Low | Confirm if used in current app. |
| Name Match | Comparison between names from user input and verified source data. | Loan Application | Medium | Confirm matching thresholds and displayed result. |
| Liveness | Check that verifies whether a captured face/photo is live/current. | Loan Application | Low | Confirm whether part of the active flow. |
| Confidence Score | Numeric or categorical score returned by a check. | Loan Application | Low | Confirm whether users see it. |
| Cutoff Limit | Threshold used to approve, reject, or route for review. | Loan Application | Low | Business/tech to confirm exact values; do not guess. |

## Engineering Reference Terms

| Term | Meaning | Source area | Confidence | Notes |
| --- | --- | --- | --- | --- |
| Controller | Backend entry point that receives and routes API requests. | Manager brief | Medium | Dileepan to validate exact code conventions. |
| Service | Backend business logic layer. | Manager brief | Medium | Dileepan to validate exact code paths. |
| Repository | Data access layer for database queries and mutations. | Manager brief | Medium | Dileepan to validate. |
| Entity | Persistent domain model or database-backed object. | Manager brief | Medium | Dileepan to validate. |
| DTO | Data Transfer Object used at request, response, or service boundaries. | Manager brief | Medium | Dileepan to validate exact naming. |
| Provider | Third-party integration used by the product or backend. | Manager brief | High | Provider-specific truth belongs in `docs/sot/providers/`, not product docs. |
| Runbook | Operational procedure for diagnosing, resolving, or escalating recurring issues. | Manager brief | High | Put operational steps in `runbooks/`. |
| FAQ | Repeated team question with concise answer and links to canonical docs. | Manager brief | High | Seed from real team questions. |

## Open Terminology Questions

| Question | Owner | Needed from | Status |
| --- | --- | --- | --- |
| Is the official app/module name "Xpress Flow", "Staff App", or something else? | Arnav | Product stakeholder | Open |
| What is the official difference between Super Loan and Welcome Loan? | Arnav | Product stakeholder | Open |
| Does Super Loan and Welcome Loan use the exact same application flow? | Arnav | Product stakeholder | Open |
| Is Applicant 2 mandatory for every Super/Welcome Loan? | Arnav | Product stakeholder | Resolved: yes, Applicant 2 is mandatory for Super/Welcome. |
| What is the official internal expansion/name for Opex? | Arnav | Operations stakeholder | Open |
| What is the official expansion and decision meaning of AIP? | Arnav | Product/credit stakeholder | Open |
| Is "Prime Test" the same as "Target Segment Checklist"? | Arnav | Product stakeholder | Open |
| What are the exact user-visible labels for Green, Yellow, and Red BRE outcomes? | Arnav | Product/credit stakeholder | Open |
| What is the exact staff login method today: OTP, password, SSO, device binding, or mixed? | Arnav | Product/engineering | Resolved: phone number plus 6-digit OTP verification. |
| What are the final Tech Support Ticket statuses and who can move tickets between them? | Arnav | Support/product stakeholder | Open |
| What are the final issue types and issue details for Tech Support Tickets? | Arnav | Support/product stakeholder | Open |
| Which ticket fields are mandatory by issue type? | Arnav | Support/product stakeholder | Open |
| What are the exact canonical lifecycle statuses for New Loan Application? | Arnav + Dileepan | Product and engineering | Open |
| Which terms are used differently by product, operations, and engineering? | Arnav | Stakeholder interviews | Open |
