# Tech Support Tickets

Canonical for product intent, user-facing behavior, screens, ticket states, issue categories, validations, and acceptance criteria for in-app support tickets.

Owner: Arnav
Status: draft
Last updated: 2026-06-29

## Source Links

| Source | Link/path | Notes |
| --- | --- | --- |
| Rough app documentation | Google Doc: https://docs.google.com/document/d/1RjWx3gUFbFS1ZXHuyM2ElMg1ltK7SCu__IaIKMfZocM/edit?usp=sharing | Contains Tech Support Tickets details. |
| Wireframes - Figma | https://www.figma.com/file/F4TByjJMRTVNC8wFp8gNUq/InPrime-LOS?node-id=0-1&t=TAhXEvcdljhFjUVC-0 | Add exact ticket frames later. |
| Flow doc | `../flows/tech-support-tickets.md` | Ticket creation and state transitions. |

## Summary

Tech Support Tickets gives internal staff a structured way to report app or process issues from within the staff app. Users can view existing tickets, create new tickets, attach supporting files, and update ticket status where allowed.

## Business Objective

- Give staff a single in-app place to report technical issues.
- Standardize issue categories so support can triage faster.
- Capture evidence such as screenshots, videos, or logs.
- Track ticket status from creation through resolution or reopening.
- Reduce informal issue reporting across calls/chats by creating a traceable ticket record.

## Users

| Role | Product usage | Needs confirmation |
| --- | --- | --- |
| RO | Raise tickets for field app issues or stuck files; can reopen if issue persists. | Resolve permission still needs confirmation. |
| AM | Raise or monitor issues for team workflows. | Does AM see team tickets or only own tickets? |
| Credit Analyst / Underwriting staff | Raise issues related to review/backend workflows. | Confirm if this role has ticket access. |
| Support tech team | Triage, work, and resolve tickets. | Confirm whether support acts in this app or separate admin/backend tool. |

## Screen Inventory

| Screen | Purpose | Main elements | User-visible states |
| --- | --- | --- | --- |
| Ticket List | Show active and historical tickets. | Title `Tech Support Tickets`, active counter, ticket cards, status badges, View action, floating plus button. | Empty, loading, tickets loaded, error loading. |
| Ticket Detail / Status Sheet | Show ticket details and status action. | Ticket summary, current status, status action options. | Open, WIP, resolved. |
| Raise Issue Form | Create a new support ticket. | Application ID/mobile input, issue type, issue detail, attachments, brief note, Submit Issue. | Incomplete, valid, upload error, submitted. |
| Attachment Picker | Add supporting evidence. | Upload slots, file preview/remove. | Up to 3 attachments, file too large, upload failed. |

## Detailed Product Flow

### View Ticket List

1. Staff opens the app and lands on the workspace.
2. Staff taps **Tech Support Tickets**.
3. App opens the ticket list screen.
4. App shows the page title, active ticket counter, ticket cards, and floating plus button.
5. Each ticket card shows ticket ID, issue category, date, status badge, and View action.
6. Staff can scroll and select a ticket card.

### Create New Ticket

1. Staff taps the floating plus button.
2. App opens the Raise Issue form.
3. Staff enters either Application ID or mobile number.
4. App validates the identifier format.
5. Staff selects an Issue Type pill.
6. App updates Issue Detail options based on the selected Issue Type.
7. Staff selects Issue Detail.
8. Staff adds up to 3 attachments if needed, but must not attach personal information.
9. Staff enters a brief note.
10. App keeps Submit Issue disabled until all required fields are complete.
11. Staff taps Submit Issue.
12. App creates the ticket and returns to the ticket list or shows the created-ticket confirmation state.
13. New ticket appears with its generated ticket ID and starting status.

### View And Update Existing Ticket

1. Staff taps View on a ticket card.
2. App opens the ticket detail/status sheet.
3. App shows current ticket state and available status options.
4. For `OPEN` or `WIP` tickets, app shows `No change` and `RESOLVED`.
5. For `RESOLVED` tickets, app shows `No change` and `OPEN`.
6. Staff selects an action.
7. App updates the ticket status if user has permission.
8. App returns to ticket list with updated status badge.

### Attachment Failure Flow

1. Staff adds attachment.
2. If attachment count exceeds 3, app blocks additional upload.
3. If image/static file is above 10 MB, app rejects it.
4. If video/log/rich media is above 50 MB, app rejects it.
5. App shows validation toast and keeps user on the form.
6. Staff can remove/replace attachment and continue.

## Ticket Card Fields

| Field | Product purpose | Notes |
| --- | --- | --- |
| Ticket ID | Unique ticket reference. | Example format in rough doc: `SUP-...`; do not use real ticket IDs in docs. |
| Issue category | Helps triage. | Should map to selected Issue Type. |
| Date stamp | Shows ticket recency. | Confirm date format. |
| Status badge | Shows current state. | OPEN grey, RESOLVED green in rough doc; WIP display TBD. |
| View action | Opens ticket status/details. | Copy shown as `View >` in rough doc. |

## Form Fields And Validation

| Field | Product rule |
| --- | --- |
| Application ID or Mobile Number | Required. Must validate as either 9-digit Application ID or 10-digit mobile number. |
| Issue Type | Required. User selects one primary category. |
| Issue Detail | Required. Options depend on selected Issue Type. |
| Attachments | Up to 3 attachments. |
| Brief Note | Required. Minimum length TBD. |
| Submit Issue | Disabled until all required fields are complete. |

## Issue Type Matrix

| Issue type | Issue detail options |
| --- | --- |
| File Stuck | KYC not updating; Submit button disabled; Processing for 24h+ |
| Application Error | App crashing; White screen; Validation error |
| Agreement/Document | Document not uploading; E-sign failed; Blurry OCR |
| SMS/WhatsApp issue | OTP not received; WhatsApp link expired; SMS failed |
| Disbursement issue | Payment pending; Bank account mismatch; UTR not generated |
| Data Correction/Wrong data | Wrong Contact Details; Name Mismatch; Address Error |

## Ticket State Matrix

| Current state | Options shown | Product behavior |
| --- | --- | --- |
| `OPEN` | No change, RESOLVED | User can keep ticket open or mark resolved if permitted. |
| `WIP` | No change, RESOLVED | User can keep WIP or mark resolved if permitted. |
| `RESOLVED` | No change, OPEN | User can reopen the ticket if issue persists, if permitted. |

## Attachment Rules

| Attachment type | Limit | Product behavior |
| --- | --- | --- |
| Static image | Up to 10 MB each | Reject larger files and show validation toast. |
| Video / logs / rich media | Up to 50 MB each | Reject larger files and show validation toast. |
| Count | Up to 3 attachments | Prevent adding more than 3 files. |

## Business Rules

| Rule | Product behavior | Status |
| --- | --- | --- |
| Ticket creation requires a valid file/customer reference. | User must enter either a 9-digit Application ID or a 10-digit mobile number. | Draft |
| Issue Detail depends on Issue Type. | Selecting Issue Type filters the secondary issue detail options. | Draft |
| Submit remains disabled until required fields are complete. | Required identifier, issue type, issue detail, and brief note must be filled. | Draft |
| Attachment limits must be enforced before submission. | More than 3 attachments or oversized files are rejected. | Draft |
| Ticket status actions depend on current status. | OPEN/WIP can move to RESOLVED; RESOLVED can move back to OPEN if permitted. | Needs role validation |
| Sensitive identifiers should be masked where required. | Mobile number/application-linked details should not expose unnecessary PII; attachments should not include personal information. | Arnav validated. |
| RO/AM can reopen tickets. | If an issue persists after resolution, RO/AM can reopen. | Arnav validated. |
| Support tech team owns triage/resolution. | Support tech team reviews and resolves tickets. | Arnav validated. |

## Events To Confirm

The rough documentation does not list explicit ticket events. Product should confirm whether these events are needed for analytics and support reporting.

| Candidate event | Trigger |
| --- | --- |
| `TechSupportTicketsClicked` | User opens Tech Support Tickets from dashboard. |
| `TechSupportTicketViewed` | User opens an existing ticket. |
| `TechSupportTicketCreateClicked` | User taps plus/create. |
| `TechSupportTicketSubmitted` | Ticket is created successfully. |
| `TechSupportTicketSubmitFailed` | Ticket creation fails. |
| `TechSupportTicketStatusChanged` | Ticket moves OPEN/WIP/RESOLVED. |
| `TechSupportAttachmentUploadFailed` | Attachment upload fails validation or upload. |

## Acceptance Criteria

- Staff can open Tech Support Tickets from the home dashboard.
- Ticket list displays ticket ID, category, date, status badge, and View action.
- User can create a ticket only after required fields are complete.
- Issue Detail options update based on selected Issue Type.
- Attachment upload enforces the count and file-size limits.
- OPEN/WIP tickets show a resolve option only if the user has permission.
- RESOLVED tickets show a reopen option only if the user has permission.
- Status changes are reflected immediately after successful save.
- Mobile numbers and other sensitive identifiers are masked where required.

## Open Questions

| Question | Owner | Needed from | Status |
| --- | --- | --- | --- |
| Is Tech Support Tickets live today or planned? | Arnav | Product/manager | Open |
| Which roles can create tickets? | Arnav | Product/support | Open |
| Which roles can resolve or reopen tickets? | Arnav | Product/support | Partially resolved: Support tech team resolves; RO/AM can reopen. |
| Does AM see team tickets or only tickets created by self? | Arnav | Product/support | Open |
| Where does support work tickets: same app, admin panel, Jira, Slack, or another system? | Arnav | Product/support | Partially resolved: Support tech team owns it; working tool still open. |
| Are tickets linked to application ID, mobile number, staff ID, or all three? | Arnav | Product/support | Open |
| What exact file types are allowed? | Arnav | Product/support | Open |
| Should ticket creation send notifications? | Arnav | Product/support | Open |
