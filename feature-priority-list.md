# Feature Priority List

Canonical for documentation prioritization, not for feature behavior.

Owner: Arnav and Dileepan
Status: draft
Last updated: 2026-06-10

## Priority Features

| Priority | Feature/domain | Why it matters | Initial docs to create | Product owner | Tech owner | Status |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | New Loan Application - Super/Welcome Loan | Highest-value loan creation flow for the first documentation pass; narrows scope to Super/Welcome only instead of covering every product variant. | `product/new-loan-application-super-welcome.md`, `flows/new-loan-application-super-welcome.md`, `tech/new-loan-application-super-welcome.md` | Arnav | Dileepan | Selected |
| 2 | Staff Login | Entry point for staff users; establishes authentication, OTP, device binding, and authenticated session rules. | `product/staff-login.md`, `flows/staff-login.md`, `tech/staff-login.md` | Arnav | Dileepan | Selected |
| 3 | Tech Support Tickets | Internal issue reporting workflow; useful for support operations, repeated app issues, ticket status handling, attachments, and routing. | `product/tech-support-tickets.md`, `flows/tech-support-tickets.md`, `tech/tech-support-tickets.md` | Arnav | Dileepan | Selected |
| 4 | Date handling and reporting contracts | Cross-cutting source of ambiguity; important for analytics and operations. | Product rules, tech contract, runbook if needed. | Arnav | Dileepan | Candidate |
| 5 | Logging and PII rules | Safety-critical and AI-grounding relevant. | Runbook/policy doc plus tech references. | Arnav | Dileepan | Candidate |

## Selection Criteria

- High onboarding value.
- Frequently asked about by product, engineering, or operations.
- Crosses product, flow, tech, provider, or runbook boundaries.
- Has enough source material to document without guessing.
- Has known ambiguity or mismatch risk.

## Week 1 Decision Needed

Confirmed first three feature packs:

1. New Loan Application - Super/Welcome Loan only.
2. Staff Login.
3. Tech Support Tickets.

## Deferred Candidates

| Feature/domain | Reason deferred |
| --- | --- |
| All Loan Files / Case Queue | Deferred from the first three after scope correction. Keep as a next candidate because it is important for tracking and rework. |
| SMART Loan, Micro LAP, Top-Up | Out of first pass. Avoid mixing product variants into the Super/Welcome doc. |
| RO productivity | Still important, but current Week 1 source material is stronger for Xpress Flow. Revisit after initial source inventory. |
| Case investigation | Can become a separate feature pack once case investigation scope is clearer. |
| Date handling and reporting contracts | Keep as cross-cutting gap/risk item. |
| Logging and PII rules | Keep as safety/runbook item. |
| New Loan Application - SMART Loan | Added after receiving SMART Loan Phase 1 details; should be treated as a product-specific loan application feature pack after Super/Welcome. |
