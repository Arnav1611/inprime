# Xpress Flow Staff Authentication

Canonical for product intent, screens, validation rules, and acceptance criteria for staff login and device verification.

Owner: Arnav
Status: draft
Last updated: 2026-06-09

## Source Links

| Source | Link/path | Notes |
| --- | --- | --- |
| Rough documentation | Google Doc: https://docs.google.com/document/d/1RjWx3gUFbFS1ZXHuyM2ElMg1ltK7SCu__IaIKMfZocM/edit?usp=sharing | Module 1: Staff Authentication & Device Binding Flow. |
| Figma | TBD | Add exact splash/login/OTP/device-warning/dashboard frames. |
| PRD | TBD | Add canonical requirements source. |
| Tech doc | TBD | Add once authentication APIs/device binding implementation are mapped. |

## Summary

Staff Authentication verifies an internal employee account through registered mobile number and OTP, enforces device-binding checks, and initializes the role-based workspace dashboard after successful login.

## Business Objective

- Allow only active internal staff to access the app.
- Reduce credential sharing by binding active credentials to an approved primary device.
- Route authenticated staff into the correct role-based dashboard/workspace.

## Users and Roles

| Role | Usage | Permissions/limits |
| --- | --- | --- |
| Relationship Officer | Login to perform loan sourcing and onboarding tasks. | Must use registered employee mobile and permitted device. |
| Area Manager | Login to monitor files, assignments, and team flows. | Role-specific dashboard access after authentication. |
| Credit Manager / PD | Login to perform verification and assessment tasks. | Role-specific dashboard access after authentication. |
| Other internal staff | TBD | Confirm whether Credit Analyst and Ops use this same login flow. |

## Screens

| Screen | Purpose | Main actions | User-visible states | Figma link |
| --- | --- | --- | --- | --- |
| Splash screen | App launch and brand/build entry state. | None or auto-transition. | Loading. | TBD |
| Mobile number login | Capture registered employee mobile number. | Enter mobile number, tap Get OTP. | Empty, valid input, invalid employee number. | TBD |
| Device warning modal | Warn or block login when hardware/device does not match expected binding. | Proceed, Go Back, Okay depending on state. | New phone warning, Not your phone lockout. | TBD |
| OTP authentication | Capture OTP delivered to staff mobile. | Enter OTP, log in, resend OTP. | OTP pending, invalid/expired OTP, resend timer. | TBD |
| Workspace handoff | Transition to home dashboard after successful auth. | None or dashboard navigation. | Authenticated session loaded. | TBD |

## Business Rules

| Rule | Source | Confidence | Notes |
| --- | --- | --- | --- |
| Mobile number accepts numeric input only. | Rough documentation | Medium | Confirm keyboard/input handling in current app. |
| Mobile number must be exactly 10 digits before Get OTP becomes active. | Rough documentation | Medium | Confirm if country code is stored separately. |
| Unregistered employee mobile number blocks progression. | Rough documentation | Medium | Error copy needs design review. |
| OTP is entered as numeric blocks. | Rough documentation | Medium | Rough doc mentions 4-digit staff OTP; applicant OTP mentions 6-digit. Confirm staff OTP length. |
| Incorrect or expired OTP blocks progression and shows an error state. | Rough documentation | Medium | Exact error copy needs review. |
| Device mismatch triggers a warning or lockout flow. | Rough documentation | Low | Requires tech/security validation. |
| Successful login loads dashboard according to role-based credentials. | Rough documentation | Medium | Confirm dashboard differences by role. |

## Acceptance Criteria

- Staff can enter a registered 10-digit mobile number and request OTP.
- Get OTP remains disabled until the mobile number format is valid.
- Unregistered mobile numbers show an inline error and do not advance to OTP.
- OTP screen shows the masked/target delivery number and supports resend behavior.
- Incorrect or expired OTP does not create an authenticated session.
- Device mismatch does not silently allow access; it must show the configured warning/lockout behavior.
- Successful authentication opens the home dashboard with correct staff identity and role context.

## Mismatches or Contradictions

| Issue | Sources that disagree | Impact | Status |
| --- | --- | --- | --- |
| Staff OTP digit count is unclear. | Rough doc says staff OTP grid has four blocks, while applicant mobile OTP is described as six digits. | QA and implementation docs may conflict. | Open |
| Device identifiers are described as MAC/IMEI. | Modern device access may not expose these directly. | Security and tech behavior needs validation. | Open |

## Open Questions

| Question | Owner | Needed from | Status |
| --- | --- | --- | --- |
| What exact OTP length is used for staff login today? | Arnav/Dileepan | Engineering/product | Open |
| What is the approved error copy for unregistered employee number? | Arnav | Product/design | Open |
| What happens when staff changes phone: self-service warning, manager approval, or hard block? | Arnav | Product/security | Open |
| Which staff roles use this login flow? | Arnav | Product/engineering | Open |
| Is device binding mandatory for all roles or only field roles? | Arnav/Dileepan | Product/security | Open |

