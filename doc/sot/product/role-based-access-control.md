# Role Based Access Control

Canonical for product-level role definitions, expected access intent, and open questions for staff role permissions.

Owner: Arnav  
Status: draft  
Last updated: 2026-06-15

## Source Links

| Source | Link/path | Notes |
| --- | --- | --- |
| Arnav clarification | User message, 2026-06-15 | Current role definitions and role lifecycle activities. |
| Staff Login product doc | `staff-login.md` | Related authentication entry point. |
| Home Dashboard product doc | `xpress-flow-home-dashboard.md` | Related dashboard card visibility. |
| Role lifecycle runbook | `../runbooks/role-lifecycle-access-changes.md` | Operational activities for onboarding, exits, movement, and temporary PD access. |

## Scope

This document captures product-level access intent for current staff roles.

Out of scope:

- Backend permission implementation.
- Exact database role names.
- HR system integration.
- Maker-checker approval implementation.
- Audit log schema.

## Current Roles

| Role | Product meaning | Expected access intent | Open questions |
| --- | --- | --- | --- |
| RO | Relationship Officer; ability to generate sales. | Can create/sell loans, initiate customer-facing workflows, and access own assigned files. | Confirm exact modules visible to RO. |
| AM | Area Manager; ability to view files of all reporting ROs. | Can monitor/view reporting RO files and may perform/coordinate area-level actions. | Confirm whether AM can edit, approve, assign, or only view by module. |
| PD | Personal Discussion role; ability to do PD in assigned PD offices. | Can access assigned PD office cases and complete PD-related activities. | Confirm whether PD is a separate role or certification on AM/CM. |
| CM | Credit Manager / Credit role. | Mentioned in lifecycle activities; exact product access not yet defined. | Confirm role expansion and system permissions. |

## Access Principles

| Principle | Product expectation |
| --- | --- |
| Role-based visibility | Dashboard cards, queues, and actions should depend on staff role and assignment. |
| Assignment-aware access | AM should view files for reporting ROs; PD should access assigned PD office cases. |
| Lifecycle-aware access | Onboarding, exit, absconding, and movement should update access promptly. |
| Temporary access | Temporary PD access at another AO should be time-bound and auditable. |
| No stale access | Exited or absconded staff should not retain active access. |
| Auditability | Role changes should preserve who changed access, when, why, and approval source. |

## Role Lifecycle Activities

Detailed operational steps belong in the runbook, but the product system should support these activity types:

| Activity | Product expectation | Status |
| --- | --- | --- |
| RO onboarding | Create RO access and assign correct AO/reporting structure. | Needs workflow details. |
| AM onboarding | Create AM access and assign reporting ROs/AO. | Needs workflow details. |
| AM PD certified | Add PD capability/certification to AM where applicable. | Needs rule details. |
| CM onboarding | Create CM access. | Need role definition. |
| RO exited | Remove/deactivate RO access and handle assigned files. | Needs responsibility mapping. |
| AM exited | Remove/deactivate AM access and reassign reporting structure. | Needs responsibility mapping. |
| CM exited | Remove/deactivate CM access. | Needs responsibility mapping. |
| RO absconded | Urgently suspend RO access and handle assigned files. | Needs SLA/escalation. |
| RO movement from one AO to another | Update AO, reporting manager, and file visibility. | Needs effective-date rule. |
| AM movement from one AO to another | Update AO and reporting hierarchy. | Needs effective-date rule. |
| CM movement from one AO to another | Update CM assignment/access. | Needs effective-date rule. |
| AM temporary going to PD at another AO | Grant temporary PD access for target AO. | Needs expiry and approval rule. |
| CM temporary going to do PD at another AO | Grant temporary PD access for target AO. | Needs expiry and approval rule. |

## Acceptance Criteria

- System has clear definitions for RO, AM, PD, and CM.
- RO access supports sales/file-generation workflows only within allowed assignment.
- AM can view files of reporting ROs.
- PD can access PD work only for assigned PD office(s).
- Exited and absconded staff access can be disabled.
- AO movement updates access and reporting visibility.
- Temporary PD access can be granted with start date, end date, target AO, and approval source.
- All role changes are auditable.

## Open Questions

| Question | Owner | Needed from | Status |
| --- | --- | --- | --- |
| What is the official expansion and responsibility boundary for CM? | Arnav | Product/credit/operations | Open |
| Which modules/actions can RO, AM, PD, and CM access? | Arnav + Dileepan | Product/engineering | Open |
| Who approves onboarding, exit, movement, and temporary PD access? | Arnav | Operations/HR/business | Open |
| What is the SLA for disabling exited or absconded staff access? | Arnav | Operations/security | Open |
| Does temporary PD access auto-expire? | Arnav + Dileepan | Product/engineering | Open |
| How are active files reassigned when RO/AM/CM exits or moves AO? | Arnav | Operations/business | Open |
