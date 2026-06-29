# All Loan Files / Case Queue

Canonical for product intent, queue structure, screen behavior, role visibility, search/filter behavior, file-card states, rework behavior, terminal states, and acceptance criteria for the **All Loan Files** experience.

Owner: Arnav  
Status: draft  
Last updated: 2026-06-29

## Source Links

| Source | Link/path | Notes |
| --- | --- | --- |
| Rough app documentation | Google Doc: https://docs.google.com/document/d/1RjWx3gUFbFS1ZXHuyM2ElMg1ltK7SCu__IaIKMfZocM/edit?usp=sharing | Priority source for All Loan Files, in-progress files, rejected/disbursed tabs, events, and status names. |
| Rough attachment | User-provided attachment | Contains status list, front-end requirements, rework logic, and backend review behavior. |
| Home Dashboard product doc | `xpress-flow-home-dashboard.md` | All Loan Files entry point from dashboard. |
| New Loan Application product doc | `new-loan-application-super-welcome.md` | Upstream source of loan application statuses and step completion. |
| Application Rework product doc | `application-rework.md` | Focused product behavior for rework across loan products. |
| Application Rework flow doc | `../flows/application-rework.md` | Focused end-to-end rework sequencing. |
| Application Rework runbook | `../runbooks/application-rework-handling.md` | Operational handling for files sent back for correction. |
| Flow doc | `../flows/all-loan-files-case-queue.md` | End-to-end sequencing, handoffs, API touchpoints, and state transitions. |
| Figma | TBD | Add exact All Loan Files, tab, filter, card, rework, rejected, and disbursed frames. |
| Tech doc | TBD | Dileepan to map queue APIs, status codes, permissions, and implementation paths. |

## Scope

This document covers the staff-facing **All Loan Files** module in the Xpress Flow / staff app.

Out of scope:

- Full New Loan Application step details.
- Full backend credit/FCU web workbench.
- Provider-specific details.
- Exact API implementation.
- Raw customer data or screenshots with PII.

## Summary

All Loan Files is the staff-facing case queue used to track loan applications after they are created. It helps staff find in-progress, rework, backend-review, sanctioned, ready-for-disbursement, disbursed, rejected, and expired loan files.

The module acts as a lifecycle tracker and action launcher:

- Staff can open role-permitted loan-file buckets.
- Staff can search by application/customer identifiers.
- Staff can sort by creation or modification date.
- Staff can filter by status.
- Staff can open file cards and continue the next allowed action.
- Rejected, expired, and disbursed files are terminal/read-only unless a future admin exception is explicitly approved.

## Business Objective

- Give staff one reliable place to find and resume loan files.
- Reduce confusion about where a case is stuck.
- Make rework visible with exact stage, document, data point, and backend remark.
- Separate actionable files from terminal history.
- Support product, credit, operations, and engineering teams with a shared status-to-queue understanding.
- Prevent unauthorized edits after files move to locked or terminal stages.

## Users And Roles

| Role | Product usage | Current understanding / open point |
| --- | --- | --- |
| RO / FOS staff | Opens own in-progress files, rework files, sanctioned next steps, and customer-facing pending actions. | Confirm exact visibility for backend review and terminal tabs. |
| AM | Views reporting RO/team files and may monitor rework, assessment, rejected, expired, and disbursed files. | Confirm area/team scope. |
| PD | May access assigned files where PD/review is required. | Confirm whether PD uses All Loan Files directly. |
| Credit / Backend team | Reviews yellow/manual-review files, can approve, reject, or send back for rework. | Rough doc references backend team; exact mobile visibility needs confirmation. |
| FCU | Reviews FCU-applicable files and can send files back, approve, or reject based on verification. | Confirm whether FCU has a staff-app queue or web-only queue. |
| Operations / Opex | Handles ready-for-disbursement, disbursement attempts, failures, NACH exceptions, and disbursed archive. | Confirm actions and queue ownership. |
| System | Fetches queue counters, filters records by role, maps statuses to buckets, and locks/unlocks actions. | Detailed implementation belongs in tech doc. |

## Entry Point

1. Staff logs in.
2. Staff lands on the Home Dashboard.
3. Staff taps **All Loan Files**.
4. App opens the All Loan Files parent/list screen based on the staff user's role and permissions.

## Parent Screen

| UI element | Product behavior |
| --- | --- |
| Page title | Shows All Loan Files or equivalent final label. |
| Search | Supports searching loan files by Mobile, Application ID, Customer Name, and PAN. |
| Sort | In-progress files can be sorted by Date Created and Date Modified. |
| Filter | Files can be filtered by Status. |
| Queue/tab list | Shows role-permitted buckets/tabs such as In-Progress, Rework, Rejected, Completed/Disbursed, and other lifecycle buckets. |
| File cards | Show key application context and current state. |
| Empty state | Should tell user no files are available for the selected filter/tab. Exact copy TBD. |

## Queue Buckets / Tabs

The exact final UI grouping needs confirmation. Product docs should currently treat the following as the working bucket model.

| Bucket / tab | Purpose | Expected behavior | Status |
| --- | --- | --- | --- |
| In-Progress Files | Active loan files that are still being completed or reviewed. | Sort by Date Created/Date Modified; search by Mobile/Application ID; filter by Status. | Supported by rough doc. |
| Rework Files | Files sent back from backend/FCU/credit for correction. | Dedicated tab under In-Progress Files; highlights stage requiring rework. | Supported by rough doc. |
| Application Assessment | Files requiring field/application assessment activity. | Shows current application stage and lets permitted staff resume allowed step. | Needs final queue naming. |
| Backend Credit Review | Files in backend/manual/FCU review after final BRE yellow/manual path. | Backend can approve, reject, or send back for rework. RO visibility/action needs confirmation. | Supported by rework logic, final UI TBD. |
| Sanctioned Files | Approved files where final offer, repayment, agreement, or post-sanction steps are pending. | Shows post-sanction roadmap and active next step. | Needs UI validation. |
| Ready for Disbursement | Files with completed documentation and ready for operations disbursement. | Status source: `FinalApplicationApprovedRFD`. Ops action rules need validation. | Mentioned in status list. |
| Disbursed / Completed Files | Successful disbursement archive. | Additional tab for completed/disbursed files. Read-only. | Supported by rough doc. |
| Disbursed & NACH Failed | Exception queue for disbursed loans with repayment/NACH failure. | Actions need operations validation. | Mentioned in earlier draft; needs source confirmation. |
| Rejected Files | Terminal rejected files. | Additional tab with rejection reason. Read-only. | Supported by rough doc. |
| Expired Files | Files expired due to application cut-off limit. | Read-only historical state showing expiry point. | Supported by status list. |

## Search, Sort, And Filter

| Control | Confirmed behavior | Open point |
| --- | --- | --- |
| Search by Mobile | Rough source confirms. | Masking/display rules need confirmation. |
| Search by Application ID | Rough source confirms. | Confirm exact application ID format. |
| Search by Customer Name | Supported. | Validated by Arnav. |
| Search by PAN | Supported. | Sensitive; product/security masking rules still apply. |
| Sort by Date Created | Confirmed for In-Progress Files. | Confirm default sort direction. |
| Sort by Date Modified | Confirmed for In-Progress Files. | Confirm if last rework/review update drives Date Modified. |
| Filter by Status | Confirmed for In-Progress Files. | Confirm status options and whether multi-select exists. |

## File Card Fields

Final card design needs Figma/app validation. Based on current docs and rough source, the card should include only role-permitted and necessary fields.

| Field | Purpose | PII / sensitivity note |
| --- | --- | --- |
| Application ID | Primary file identifier. | Low sensitivity. |
| Customer name | Helps staff identify file. | PII; avoid copying real values into docs. |
| Mobile number | Helps search/contact. | PII; should be masked in documentation and screenshots. |
| Product tag | Shows product variant: Super, Welcome, SMART, Top-Up, MLAP, etc. | Low sensitivity. |
| Current status/sub-status | Explains where file is in lifecycle. | Must map to canonical statuses. |
| Date created | Helps queue aging. | Low sensitivity. |
| Date modified / last updated | Helps staff prioritize recently changed files. | Low sensitivity. |
| Assigned RO/AM/PD/Credit owner | Explains ownership and handoff. | Internal staff info; confirm visibility. |
| Rework badge | Highlights file returned for correction. | Should be visible only when applicable. |
| Rejection reason | Explains terminal rejection. | RO/AM can see rejected reasons. |

## Statuses Relevant To All Loan Files

These statuses come from rough source and upstream loan application docs. Exact implementation names must be validated by Dileepan.

| Status | Product meaning | Queue impact |
| --- | --- | --- |
| `ApplicationIDGenerated` | Application ID created. | File can appear in in-progress queue. |
| `ApplicationBackendReviewSubmitted` | Application submitted for backend review. | Moves to backend credit/manual review queue. |
| `ApplicationReworkRequired` | Backend/FCU/credit sent application back for correction. | Moves to rework tab/queue. |
| `ApplicationRejected` | Application terminally rejected at any point. | Moves to Rejected Files; read-only. |
| `ApplicationExpired` | Application expired because cut-off limit reached from file creation date. | Moves to Expired Files; read-only. |
| `ApplicationFinalOfferGenerated` | Final loan offer generated. | Moves/updates sanctioned or offer stage. |
| `ApplicationFinalOfferSubmitted` | Final offer submitted based on customer requirement. | Moves to repayment/agreement next stage. |
| `RepayModeSubmitted` | Preferred repayment mode selected and submitted. | Moves toward repayment registration. |
| `LoanAgreementSigned` | Loan agreement signed by all required applicants. | Moves toward RFD/disbursement. |
| `RepaymentRegistrationCompleted` | ENACH/UPI Autopay registration completed. | Moves toward RFD/disbursement. |
| `FinalApplicationApprovedRFD` | Application completed and ready for disbursement. | Moves to Ready for Disbursement. |
| `DisbursementAttempted` | Disbursement attempted. | Shows pending/success/failure state. |
| `DisbursementFailed` | Disbursement failed to credit customer account. | Moves to failure/exception handling. |
| `DisbursementSuccess` | Disbursement successful. | Moves to Disbursed/Completed Files; read-only. |
| `LoanAccIDGenerated` | Loan account ID generated. | Appears in post-disbursement/disbursed context. |

## Rework Behavior

Rework is a core All Loan Files behavior.

Detailed rework behavior is documented in `application-rework.md`. This section keeps the parent queue-level summary only.

| Rule | Product behavior |
| --- | --- |
| Rework source | Backend team, FCU, credit, or operations can send eligible files back for correction. |
| Eligibility | Rework is allowed only for files that are still in-progress. |
| Not allowed | Rework is not allowed for Rejected, Disbursed, or Expired files. |
| Queue placement | Cases sent back for change should appear in a dedicated tab under In-Progress Files. |
| Step highlighting | The application stage requiring rework should be highlighted in the loan application steps screen. |
| Detail required | Rework details should include exact stage, screen, document/data point, and backend remarks. |
| Staff action | FOS/RO edits only the allowed item and submits a remark while resubmitting. |
| Resubmission | After rework, file returns to backend review/FCU after final validations. |
| Audit | LOS should receive response back from FOS app along with remarks. |

## Self Edit And Self Reject

| Area | Product behavior |
| --- | --- |
| Self edit | FOS staff may change limited submitted application data. Some submitted data points cannot be edited. |
| Edit source | Final editable data-point list is referenced in a sheet in rough source and must be linked when available. |
| Resubmission | Resubmitted data should replace old data in LOS where allowed. |
| Self reject | Manual rejection should capture rejection reason and checklist items where applicable. |
| Event | Rough source mentions `ManualRejectLoanApplicationTriggered`. |

## Backend Review And Final BRE Relationship

| BRE result | Product behavior | Queue impact |
| --- | --- | --- |
| Green | Straight-through offer. | File proceeds to final offer generation. |
| Yellow | FCU or backend/manual review. | File moves to backend review/FCU queue. |
| Red | Straight-through rejected. | File moves to Rejected Files. |

For Yellow/manual-review files, backend team can approve, reject, or send the case back for rework. If sent back, the rework logic above applies.

## Product Tags

All Loan Files should show product tags consistently so staff can identify product-specific flows.

| Product | Expected tag behavior |
| --- | --- |
| Super | Show Super tag. |
| Welcome | Show Welcome tag. |
| SMART | Show SMART tag similar to Super/Welcome tags. |
| Top-Up | Show Top-Up tag where application comes from Leads > Top-up. |
| MLAP / Micro LAP | Show MLAP/Micro LAP tag; final label needs confirmation. |

## Business Rules

| Rule | Source | Confidence | Notes |
| --- | --- | --- | --- |
| Staff can open All Loan Files from dashboard. | Existing dashboard docs | High | Confirm final card label. |
| In-progress files can be sorted by Date Created and Date Modified. | Rough source | High | Confirm default sort. |
| In-progress files can be searched by Mobile, Application ID, Customer Name, and PAN. | Arnav validation | High | Confirm masking and access control for PAN. |
| Files can be filtered by Status. | Rough source | High | Confirm filter values. |
| Rejected Files need an additional tab/screen with rejection reason. | Rough source | High | Role visibility needs confirmation. |
| Completed/disbursed files need an additional tab/screen. | Rough source | High | Terminal read-only unless exception exists. |
| Rework files appear under In-Progress Files in a dedicated tab. | Rough source | High | Exact tab label needs confirmation. |
| Rework must show exact stage/screen/document/data point and backend remarks. | Rough source | High | Product-critical. |
| Rework is not allowed for rejected, disbursed, or expired files. | Rough source | High | Terminal state rule. |
| Manual reject should capture checklist items in rejection reason. | Rough source | Medium | Confirm final rejection form. |

## Events

Events mentioned in rough source:

| Event | Trigger |
| --- | --- |
| `InProgressFilesClicked` | Staff opens In-Progress Files. |
| `ManualRejectLoanApplicationTriggered` | Staff manually rejects an application. |
| `ApplicationSubmittedForFinalBRERun` | Final BRE submitted. |
| `FinalBRERunCompleted` | Final BRE completed. |
| `FinalBRERunApplicationGreen` | Final BRE result Green. |
| `FinalBRERunApplicationYellow` | Final BRE result Yellow. |
| `FinalBRERunApplicationRed` | Final BRE result Red. |
| `FinalBRERunApplicationFCU` | Final BRE routes to FCU. |
| `FinalLoanOfferGeneratedSTP` | Straight-through final offer generated. |
| `FinalLoanOfferSubmitted` | Final offer submitted. |
| `ApplicationBackendReject` | Backend rejects application. |
| `FinalLoanOfferGeneratedBE` | Backend-generated final offer. |
| `ApplicationSentBackFromBE` | Backend sends application back. |
| `ApplicationReworkSubmittedFOS` | FOS submits rework. |

## Acceptance Criteria

- Staff can open All Loan Files from the Home Dashboard.
- Staff sees only queues and records allowed by role and assignment.
- In-progress files support sort by Date Created and Date Modified.
- In-progress files support search by Mobile and Application ID.
- Files can be filtered by Status.
- Rework files appear in a dedicated in-progress/rework tab.
- Rework file cards or detail screens show the exact stage, screen, document/data point, and backend remarks.
- Only allowed rework fields/documents are editable.
- Rework resubmission asks for or records FOS/staff remarks.
- Rework resubmission sends the file back to backend review/FCU.
- Rejected files show rejection reason where the role is permitted to see it.
- Disbursed/completed files appear in a separate tab/screen and are read-only.
- Expired files are read-only and show the expiry/cut-off context.
- PII is masked or only shown where role and business need allow it.

## Mismatches Or Gaps

| Issue | Impact | Status |
| --- | --- | --- |
| The exact final bucket/tab list is not confirmed. Rough source clearly mentions in-progress, rejected, and completed/disbursed additions; earlier draft also had backend review, sanctioned, RFD, NACH failed, expired. | Product docs may overstate UI tabs unless validated. | Open |
| Search by Customer Name and PAN appeared in earlier draft but extracted rough lines confirm only Mobile and Application ID. | Search docs may include unsupported/sensitive fields. | Open |
| Ready for Disbursement and Disbursed & NACH Failed need more operations detail. | Ops workflows cannot be fully accepted yet. | Open |
| Role visibility for rejection reasons and backend review is unclear. | Sensitive credit remarks may be overexposed if not controlled. | Open |

## Open Questions

| Question | Owner | Needed from | Status |
| --- | --- | --- | --- |
| What is the final canonical list of All Loan Files buckets/tabs? | Arnav | Product/design | Open |
| Which roles can view, open, and act on each bucket? | Arnav + Dileepan | Product/engineering | Open |
| Which statuses map to each bucket? | Dileepan | Engineering/code | Open |
| Are Customer Name and PAN supported search fields, or only Mobile and Application ID? | Arnav | Product/design/security | Resolved: Customer Name and PAN are supported. |
| What are the exact filter values under Status? | Arnav | Product/design | Open |
| What is the default sort order for each queue? | Arnav | Product/design | Open |
| What is the TTL/cut-off rule for ApplicationExpired? | Arnav + Dileepan | Product/engineering | Open |
| Which roles can see rejection reasons and backend remarks? | Arnav | Product/security/credit | Partially resolved: RO/AM can see rejected reasons; backend remarks visibility still needs product/security validation. |
| What actions exist in Ready for Disbursement and Disbursed & NACH Failed? | Arnav | Operations | Open |
