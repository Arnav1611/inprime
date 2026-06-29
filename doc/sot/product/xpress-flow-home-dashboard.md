# Xpress Flow Home Dashboard / Home Screen

Canonical for product intent, home-screen layout, dashboard options, role visibility, navigation routes, business rules, analytics events, acceptance criteria, and open questions for the Xpress Flow staff app home screen.

Owner: Arnav  
Status: draft  
Last updated: 2026-06-29

## Source Links

| Source | Link/path | Notes |
| --- | --- | --- |
| Rough documentation | Google Doc: https://docs.google.com/document/d/1RjWx3gUFbFS1ZXHuyM2ElMg1ltK7SCu__IaIKMfZocM/edit?usp=sharing | Module 2: Core Workspace Home Dashboard Hub. |
| Staff authentication product doc | `xpress-flow-staff-authentication.md` | Login/session handoff into dashboard. |
| Staff login to dashboard flow | `../flows/staff-login-home-dashboard.md` | Authentication-to-dashboard sequence and exception paths. |
| New Loan Application docs | `xpress-flow-loan-origination.md`, `new-loan-application-super-welcome.md`, `new-loan-application-smart-loan.md`, `new-loan-application-mlap.md` | Product routes after New Loan Application click. |
| All Loan Files product doc | `all-loan-files-case-queue.md` | All Loan Files route and queues. |
| Leads product doc | `leads.md` | Leads route, tabs, cards, and actions. |
| Tech Support Tickets product doc | `tech-support-tickets.md` | Ticket route and ticket actions. |
| Loan Pricing product doc | `loan-pricing-generator.md` | Loan Pricing Calculator route and pricing behavior. |
| Product variants doc | `xpress-flow-product-variants.md` | Product options and product-specific rules. |
| Figma | TBD | Add exact dashboard frame and role-specific variants. |
| Tech doc | TBD | Dileepan to map dashboard APIs, role permissions, card visibility, and analytics events. |

## Scope

This document covers the first authenticated screen after staff login: the **Home Dashboard / Home Screen**.

Out of scope:

- Full login/OTP/device-binding behavior.
- Detailed behavior inside each module after the user opens it.
- API implementation details.
- Role-permission code paths.
- Provider-specific behavior.

## Summary

The Home Dashboard is the staff app's main workspace after successful login. It displays the logged-in staff identity and provides navigation cards for the major internal workflows:

- New Loan Application.
- All Loan Files.
- Tech Support Tickets.
- Leads.
- Loan Pricing Calculator.
- InPrime Leaderboard.

The dashboard should make daily work fast for field and internal staff. Current validation says all listed dashboard cards are accessible.

## Business Objective

- Give every authenticated staff user a single starting point.
- Route staff into the highest-frequency workflows quickly.
- Keep product navigation consistent across roles.
- Avoid staff entering modules or actions they are not permitted to use.
- Support tracking of dashboard usage through approved analytics events.
- Make major product areas discoverable without mixing detailed module behavior into the home screen.

## Users And Roles

| Role | Home-screen usage | Current understanding / open point |
| --- | --- | --- |
| RO / Relationship Officer | Starts new applications, opens Leads, views files, raises support tickets, uses pricing calculator, views leaderboard. | New Loan Application and Leads are primarily RO workflows. |
| AM / Area Manager | Monitors team/area files, Leads, performance/leaderboard, support issues, and possibly pricing. | Confirm whether AM can start any application or only view/assign. |
| PD | May access assigned files or field-verification work through All Loan Files. | Confirm whether PD sees all dashboard cards. |
| Credit / Backend user | May access review queues through All Loan Files. | Confirm if Credit uses mobile dashboard or separate web workbench. |
| Operations / Opex | May access disbursement/closing-related queues through All Loan Files and support tickets. | Confirm operations card visibility. |
| Tech Support user | May view/triage tickets if same app supports support-team login. | Confirm if support team uses this dashboard. |

## Home Screen Layout

| Area | Product behavior |
| --- | --- |
| Header / identity | Shows staff name and staff ID, with profile picture on the top right. |
| Role/session context | Dashboard should load cards and permissions based on authenticated staff role. |
| Navigation cards | Shows module cards/options listed in this doc. |
| Card subtitle | Each card should communicate the action briefly, such as Create new loan application or View all loan files. |
| Error state | If dashboard data cannot load, app should show a retry/error state. Exact copy TBD. |
| Restricted access state | Current validation says all listed cards are accessible; no restricted-card copy is required for these cards. |

## Dashboard Options / Cards

| Card / option | Visible subtitle / intent | What it is for | Routes to | Related docs | Current notes |
| --- | --- | --- | --- | --- | --- |
| New Loan Application | Create new loan application | Start a new loan journey and choose product type. | Product selection screen for Super/Welcome, SMART, MLAP, and other enabled products. | `xpress-flow-loan-origination.md`, product-specific loan docs | Primarily RO-owned; confirm if AM/PD can initiate any product. |
| All Loan Files | View all loan files | View active, rework, review, sanctioned, ready-for-disbursement, rejected, expired, and disbursed files. | All Loan Files / Case Queue. | `all-loan-files-case-queue.md` | Available by role/assignment; file list must be permission-filtered. |
| Tech Support Tickets | Create and View Tickets | Raise and track internal support tickets for app/file/document/disbursement issues. | Tech Support Tickets list and create-ticket flow. | `tech-support-tickets.md` | Confirm support-team and staff permissions. |
| Leads | Create and View Leads | View lead tabs, create leads, contact customers, reject leads, start applications, and access Top-Up/Repeat leads. | Leads module. | `leads.md`, `top-up-loan.md`, `repeat-loan.md` | Top-Up and Repeat are accessed through Leads. Repeat currently appears under Top-up section with Repeat tag. |
| Loan Pricing Calculator | Estimate loan costs | Estimate pricing values such as amount, tenure, EMI, fees, insurance, and net disbursement. | Loan Pricing Generator / Calculator. | `loan-pricing-generator.md` | Output is official enough to show customer. |
| InPrime Leaderboard | View performance leaderboard | View staff/team performance ranking and productivity metrics. | Leaderboard module. | TBD | Live today; metric definitions need a separate doc if prioritized. |

## New Loan Application Route

When staff taps **New Loan Application**, the app should route to product selection.

Current documented product options include:

| Product option | Product doc | Notes |
| --- | --- | --- |
| Super / Welcome Loan | `new-loan-application-super-welcome.md` | Shared flow with amount differences. |
| SMART Loan | `new-loan-application-smart-loan.md` | 17-step flow; Applicant 1 mandatory. |
| MLAP / Micro LAP | `new-loan-application-mlap.md` | 18-step flow; collateral/property rules. |

Top-Up and Repeat do **not** start from New Loan Application in current docs; they start from Leads.

## Leads Route

When staff taps **Leads**, the app opens the Leads module.

Expected Lead tabs/current examples:

| Leads area | Notes |
| --- | --- |
| My Leads | Assigned leads for logged-in staff; exact ownership rule open. |
| Top-up | Existing-borrower Top-Up leads. |
| Repeat | Currently appears under Top-up section but marked/tagged Repeat; separate tab decision open. |
| Digital Leads | Digital-source leads. |
| Retarget | No longer in use per latest validation. |

## All Loan Files Route

When staff taps **All Loan Files**, the app opens the case queue.

Expected file areas include:

- In-Progress Files.
- Rework Files.
- Backend Credit Review.
- Sanctioned Files.
- Ready for Disbursement.
- Disbursed / Completed Files.
- Rejected Files.
- Expired Files.

Exact tabs and visibility differ by role and need final confirmation in the All Loan Files doc.

## Role Visibility And Permissions

| Card | RO | AM | PD | Credit | Operations | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| New Loan Application | Expected yes | Open | Open | Likely no/open | Likely no/open | Confirm whether non-RO roles can start applications. |
| All Loan Files | Expected yes | Expected yes | Expected yes for assigned files | Expected yes for review queues | Expected yes for ops queues | Must be filtered by role/assignment. |
| Tech Support Tickets | Expected yes | Expected yes | Open | Open | Open | Confirm if all staff can create tickets. |
| Leads | Expected yes | Expected yes/open | Likely no/open | Likely no/open | Likely no/open | Confirm view/create/start permissions. |
| Loan Pricing Calculator | Expected yes | Expected yes/open | Open | Open | Open | Confirm who can use pricing and whether result is official. |
| InPrime Leaderboard | Expected yes | Expected yes | Open | Likely no/open | Likely no/open | Confirm metric scope and role visibility. |

## Business Rules

| Rule | Product behavior | Status |
| --- | --- | --- |
| Auth required | Dashboard loads only after successful staff authentication. | Confirmed from login flow. |
| Identity shown | Dashboard shows staff name and staff ID with profile picture on top right. | Validated. |
| Role-based permissions | Cards/routes should respect staff role and assignment. | Needs final role matrix. |
| Unauthorized access | Current validated home cards are all accessible. | Validated for listed cards. |
| All Loan Files filtering | Even if visible broadly, All Loan Files must show only permitted records. | Confirmed product expectation. |
| New Loan Application route | Opens product selection, not directly a fixed loan flow. | Confirmed by product docs. |
| Top-Up/Repeat route | Starts from Leads, not Home > New Loan Application. | Confirmed by current product docs. |
| Tech Support route | Opens ticket list/create flow. | Confirm final issue types and permissions. |
| Loan Pricing route | Opens calculator/generator. | Validated as official enough to show customer. |

## Analytics Events

Events mentioned in rough documentation and existing docs. Engineering must validate actual names/payloads.

| Event | Trigger |
| --- | --- |
| `HomeScreenHubLoaded` | Dashboard loads after successful login. |
| `NewLoanApplicationClicked` | Staff taps New Loan Application. |
| `AllLoanFilesClicked` | Staff taps All Loan Files. |
| `TechSupportTicketsClicked` | Staff taps Tech Support Tickets. |
| `LeadsClicked` | Staff taps Leads. |
| `LoanPricingCalculatorClicked` | Staff taps Loan Pricing Calculator. |
| `InPrimeLeaderboardClicked` | Staff taps InPrime Leaderboard. |

## Acceptance Criteria

- Dashboard loads only after successful staff authentication.
- Dashboard displays correct staff identity from active session.
- Dashboard shows the approved set of cards/options for the logged-in role.
- Tapping New Loan Application opens product selection.
- Tapping All Loan Files opens a role-filtered case queue.
- Tapping Tech Support Tickets opens the ticket list/create-ticket workflow.
- Tapping Leads opens the Leads module with role-permitted tabs/actions.
- Tapping Loan Pricing Calculator opens the pricing calculator/generator.
- Tapping InPrime Leaderboard opens the leaderboard module.
- Current listed routes are accessible.
- Dashboard click events are tracked if analytics is approved and implemented.

## Open Questions

| Question | Owner | Needed from | Status |
| --- | --- | --- | --- |
| Are all dashboard cards visible to every role, or should unauthorized cards be hidden/disabled? | Arnav | Product/design/engineering | Resolved: all listed cards are accessible. |
| What is the exact staff identity format: staff name, staff ID, role, AO, or other fields? | Arnav | Product/design | Resolved: name and staff ID with profile picture on top right. |
| What is the final ordered list of dashboard cards? | Arnav | Product/design | Resolved: New Loan Application, All Loan Files, Tech Support Tickets, Leads, Loan Pricing Calculator, InPrime Leaderboard. |
| Is InPrime Leaderboard live today, and what metrics does it show? | Arnav | Product/business | Partially resolved: live today; metrics require separate doc/source. |
| Are dashboard analytics events implemented with the names listed here? | Dileepan | Engineering/analytics | Open |
| What message appears when a user taps a module they are not allowed to access? | Arnav | Product/design | Resolved for current cards: all are accessible. |
