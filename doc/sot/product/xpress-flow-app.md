# Xpress Flow App

Canonical for product-level overview, roles, modules, navigation, and open product questions for the internal Xpress Flow staff app.

Owner: Arnav
Status: draft
Last updated: 2026-06-18

## Source Links

| Source | Link/path | Notes |
| --- | --- | --- |
| Rough documentation | Google Doc: https://docs.google.com/document/d/1RjWx3gUFbFS1ZXHuyM2ElMg1ltK7SCu__IaIKMfZocM/edit?usp=sharing | Source used for this draft. Needs product review before becoming canonical. |
| Figma | TBD | Add exact frame links for every screen/module. |
| PRD | TBD | Add canonical product requirement source if available. |
| Leads product doc | `leads.md` | Leads module, tabs, cards, actions, and open questions. |
| Leads flow doc | `../flows/leads.md` | Leads sequencing, handoffs, touchpoints, and states. |
| Flow docs | TBD | Create after Week 1 inventory. |
| Tech docs | TBD | Dileepan to map APIs, controllers, services, entities, providers. |

## Summary

Xpress Flow is an internal staff app used by InPrime field, credit, area, and operations teams to manage loan origination and related staff workflows. The app supports staff login, role-based dashboard navigation, new loan application creation, product-specific onboarding flows, applicant verification, residence and family data capture, bank statement ingestion, credit and policy checks, offer acceptance, repayment mandate setup, and agreement e-sign.

This document is product-level only. Detailed API behavior, provider behavior, code paths, and implementation ownership should live in `docs/sot/tech/` and `docs/sot/providers/`.

## User Roles

| Role | Persona code | Product responsibility | Access/products mentioned | Open questions |
| --- | --- | --- | --- | --- |
| Relationship Officer | `ROLE-RO` | Lead sourcing, customer profiling, initial applicant data capture, customer-facing onboarding, document capture, OTP/consent, loan flow completion where permitted. | Staff login, home dashboard, new loan application, leads, loan pricing calculator, leaderboard, offer, NACH, e-sign. | Confirm exact module permissions by product and stage. |
| Credit Manager / Personal Discussion user | `ROLE-PD` | Ground-level physical verification, risk profiling, collateral assessment, income and household cash-flow sanity checks. | Residence/income assessment, disbursement account capture, additional docs, BRE-related steps. | Confirm whether `ROLE-PD` and Credit Manager are the same internal role. |
| Area Manager | `ROLE-AM` | Area-level monitoring, team metrics, pipeline visibility, escalations, growth monitoring, case assignment/ownership. | Dashboard, all loan files, leaderboard, SMART Loan PD assignment and field audit stages. | Confirm exact AM authority for assignment, overrides, and approvals. |
| Credit Analyst | `ROLE-CR` | Formal underwriting, policy review, compliance check, bureau review, sanction/reject decisions. | Credit review queues and final file decisioning. | Confirm whether this role uses Xpress Flow directly or another backend workbench. |
| Operations | `ROLE-OPS` | Closing checks, pre-disbursement verification, bank routing validation, transaction/disbursement workflows. | All loan files, disbursement-related queues. | Confirm operations screens in Xpress Flow. |

## Main Navigation

| Dashboard card | Purpose | Expected users | Product notes | Open questions |
| --- | --- | --- | --- | --- |
| New Loan Application | Start a new loan application and select product type. | Primarily `ROLE-RO` | Routes into product selection and applicant onboarding. | Confirm if AM/PD can initiate any product. |
| All Loan Files | View active/historical loan files by queue/status. | All internal staff | Queue results should filter by role and permissions. | Confirm exact bucket names and visibility logic. |
| Tech Support Tickets | Create and view support tickets. | TBD | Mentioned on home dashboard. | Need separate product doc if in scope. |
| Leads | Create and view leads. | `ROLE-RO`; possibly AM | Dedicated Leads docs created. Top-Up Loan is accessed via Leads > Top-up tab. | Confirm lead statuses, tabs, assignment rules, and role permissions. |
| Loan Pricing Calculator | Estimate loan cost before/alongside application. | Field and manager roles | Product-specific constraints and fees apply. | Confirm whether calculations are advisory or official. |
| InPrime Leaderboard | View FOS/marketing performance rankings. | `ROLE-RO`, `ROLE-AM` | Supports RO vs Area Office and MTD vs FTD views. | Confirm metric definitions and source events. |

## Product Areas Covered In Rough Documentation

| Area | Product doc | Status |
| --- | --- | --- |
| Staff authentication and device binding | `xpress-flow-staff-authentication.md` | Drafted |
| Home dashboard | `xpress-flow-home-dashboard.md` | Drafted |
| New loan application and product routing | `xpress-flow-loan-origination.md` | Drafted |
| SMART Loan product variant | `xpress-flow-product-variants.md` | Drafted |
| Leads | `leads.md` | Drafted |
| Top-Up Loan via Leads | `top-up-loan.md` | Drafted |
| Leaderboard | TBD | Needs separate product doc if prioritized. |
| Loan pricing calculator | TBD | Needs separate product doc if prioritized. |
| All Loan Files | TBD | Needs separate product doc if prioritized. |

## App-Level Business Rules

| Rule | Source | Confidence | Notes |
| --- | --- | --- | --- |
| Staff must authenticate through registered mobile number and OTP. | Rough documentation | Medium | Validate OTP length and exact error copy. |
| Staff login is tied to a primary device/hardware binding. | Rough documentation | Medium | Requires tech/security validation. |
| Dashboard identity uses active session staff name and staff ID. | Rough documentation | Medium | Validate session payload field names in tech docs. |
| Dashboard cards may be visible broadly, but opening a module validates role permissions. | Rough documentation | Low | Needs product and engineering review. |
| Product selection changes downstream onboarding steps and mandatory applicant rules. | Rough documentation | Medium | Needs validation against current app behavior. |
| Product docs should not duplicate API implementation details. | Manager brief | High | Link to tech/provider docs instead. |

## Open Questions

| Question | Owner | Needed from | Status |
| --- | --- | --- | --- |
| What is the official app name: Xpress Flow, Staff App, or another internal name? | Arnav | Product/manager | Open |
| Which roles are active in the current app and which are planned/future? | Arnav | Product/engineering | Open |
| Which dashboard cards are visible to each role? | Arnav | Product/engineering | Open |
| Which product journeys are live today: Super/Welcome Loan, Smart Loan, Micro LAP, Top-Up? | Arnav | Product/manager | Open |
| Which rough-doc examples are placeholder values versus real current UI copy? | Arnav | Product/design | Open |
| Which Figma frames are canonical for each module? | Arnav | Product/design | Open |
| Which PRD or requirement note is canonical for Xpress Flow? | Arnav | Product/manager | Open |
