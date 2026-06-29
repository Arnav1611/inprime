# Retarget Leads

Historical reference for the deprecated **Retarget Leads** concept under the Leads module. Retarget Leads are no longer in use as per latest Arnav validation.

Owner: Arnav  
Status: deprecated / historical reference  
Last updated: 2026-06-29

## Source Links

| Source | Link/path | Notes |
| --- | --- | --- |
| Product note from Arnav | Current Codex thread, 2026-06-23 | Priority source for Retarget Leads behavior. |
| Leads parent doc | `leads.md` | Parent Lead Management module. |
| Retarget Leads flow doc | `../flows/retarget-leads.md` | End-to-end sequence and handoffs. |
| App Figma | https://www.figma.com/design/F4TByjJMRTVNC8wFp8gNUq/InPrime-LOS?node-id=15553-28578&t=JSVL0rmJfDSvlZ1P-11 | Retarget Leads design reference. |
| Digital Leads product doc | `digital-leads.md` | Reject Lead behavior should work similar to Digital Leads. |
| Rough app documentation | Google Doc: https://docs.google.com/document/d/1RjWx3gUFbFS1ZXHuyM2ElMg1ltK7SCu__IaIKMfZocM/edit?usp=sharing | Base staff app source. |

## Scope

This document covers the old **Retarget Leads** concept. It is retained only for historical reference because the feature is no longer in use.

Out of scope:

- Detailed eligibility filter logic.
- PR/eligibility run implementation.
- Provider-specific behavior.
- Full New Loan Application checklist after Start Application.
- CRM/upload UI, because no CRM/upload feature is needed as of current scope.
- Raw customer PII.

## Summary

Retarget Leads were intended to be created from old loan applications that were previously rejected and may now be eligible. Eligibility would have been identified by applying filters on old applications and then running PR on the shortlisted cases. Latest validation says this flow is no longer active.

This is meant to help ROs increase business from their captive relationship base by reapproaching customers who already have prior relationship/application history with InPrime.

## Business Objective

- Reuse previously rejected loan applications where the customer may now be eligible.
- Increase business from RO's captive relationship base.
- Give ROs a separate queue for retargeting opportunities instead of mixing them with My Leads or Digital Leads.
- Allow staff to call, navigate to customer location, reject, or start application from the Retarget bucket.
- Keep the first version backend-driven without requiring a CRM/upload screen.

## App Entry Point

The below entry point is historical only.

1. Staff logs in to XPress App.
2. Staff opens Home Dashboard.
3. Staff taps **Leads**.
4. Staff selects the **Retarget** tab.
5. System shows eligible Retarget lead cards.

## Screens

| Screen | Purpose | Notes |
| --- | --- | --- |
| Leads tab list | Shows available lead buckets. | Retarget should be a separate tab under Leads. |
| Retarget lead list | Shows old rejected applications that may now be eligible. | Data is added from backend upload/process, not CRM UI. |
| Lead action menu | Allows staff to act on the lead. | Reject Lead should follow Digital Leads rejection flow. |
| Reject Lead screen | Captures rejection reason and remarks. | Same/similar behavior as Digital Leads. |
| Start Application route | Starts the applicable loan application flow. | Final product routing needs confirmation. |

## Retarget Lead Source

Retarget data will be shared in upload format and added directly from backend.

Current scope:

- No CRM upload feature is needed.
- No app-side Add Lead flow is needed.
- No manual RO creation of Retarget Leads is expected.
- Eligibility is established before the lead reaches RO.

## Card Fields

| Field | Source / meaning | Required? | Notes |
| --- | --- | --- | --- |
| Applicant 1 Name | Old loan application | Yes | PII; do not copy real values into docs. |
| Applicant 1 Mobile Number | Old loan application | Yes | Primary contact number. PII. |
| Last Application Date | Old loan application | Yes | Shows when the earlier application was created/submitted. |
| Occupation | Prime Test from old application | Yes | Occupation should come from Prime Test. |
| Location in UI view | Pincode and Micro Area from old application | Yes | Used for staff to understand the area. |
| Location for Get Direction | Applicant 1 selfie location | Conditional | Used when staff taps Get Direction. |

## Actions

| Action | Behavior |
| --- | --- |
| Call Customer | Opens phone/dialer for Applicant 1 mobile number. |
| Reject Lead | Works similar to Digital Leads rejection flow. |
| Start Application | Starts the applicable InPrime loan application journey. Final target product/routing needs confirmation. |
| Get Direction | Uses Applicant 1 selfie location, not the UI display location. |

## Business Rules

| Rule | Behavior | Status |
| --- | --- | --- |
| Retarget is a Leads tab. | Historical design only; Retarget is no longer in use. | Deprecated. |
| Retarget leads come from old rejected applications. | Previously rejected applications may be retargeted if they may now be eligible. | Source-backed. |
| Eligibility is pre-identified. | System/business filters old applications and runs PR before sharing to RO. | Source-backed; exact filters open. |
| Data is backend-added. | Upload format is used, but no CRM/upload feature is needed in current scope. | Source-backed. |
| Location has two uses. | UI view uses pincode + micro area; Get Direction uses Applicant 1 selfie location. | Source-backed. |
| Reject flow follows Digital Leads. | Rejection behavior should be similar to Digital Leads. | Source-backed. |

## Acceptance Criteria

- Historical design had a **Retarget** tab; current product validation says Retarget is no longer in use.
- Retarget tab shows backend-added eligible retarget leads.
- Each Retarget lead card shows Applicant 1 name, Applicant 1 mobile number, last application date, occupation, and UI location.
- UI location is based on pincode and micro area from the old application.
- Get Direction uses Applicant 1 selfie location.
- Reject Lead follows the same/similar flow as Digital Leads.
- Rejected Retarget Leads move out of the active Retarget queue or show as rejected based on final rejected-bucket behavior.
- Start Application is available only when product/role eligibility allows it.
- No CRM/upload screen is required for Retarget Leads in current scope.

## Open Questions

| Question | Owner | Needed from | Status |
| --- | --- | --- | --- |
| Is Retarget active in the current product? | Arnav | Product | Resolved: no longer in use. |
| Should this historical doc be archived later? | Arnav | Product/docs owner | Open |
