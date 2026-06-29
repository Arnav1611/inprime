# Staff Login

Canonical for product intent, user-facing behavior, login requirements, audit expectations, events, and open questions for staff login.

Owner: Arnav
Status: draft
Last updated: 2026-06-29

## Source Links

| Source | Link/path | Notes |
| --- | --- | --- |
| Staff Login flow | https://whimsical.com/staff-login-N12jhpKQxrZXK4edT4XJoX | Login source flow. |
| Wireframes - Figma | https://www.figma.com/file/F4TByjJMRTVNC8wFp8gNUq/InPrime-LOS?node-id=0-1&t=TAhXEvcdljhFjUVC-0 | Add exact login frames later. |
| Requirements attachment | User-provided attachment | LOS and front-end requirements. |
| Rough app documentation | Google Doc: https://docs.google.com/document/d/1RjWx3gUFbFS1ZXHuyM2ElMg1ltK7SCu__IaIKMfZocM/edit?usp=sharing | Earlier mobile OTP/device binding notes. |
| Flow doc | `../flows/staff-login.md` | Sequence and exceptions. |

## Summary

Staff Login controls access to the internal staff app. It should validate that the user is an active staff member, create an authenticated session, apply role-based access, and record audit details for login attempts.

The current staff login method is phone number plus 6-digit OTP verification. Staff ID/password and forgot-password items from older requirement notes should not be treated as live unless reconfirmed.

## Business Objective

- Allow only active internal staff to access the app.
- Ensure each staff user is mapped to the correct role and access level.
- Maintain an audit trail of login attempts.
- Reduce unauthorized use through validation, session timeout, and possible device binding.
- Route staff into the correct workspace after login.

## Users

| Role | Login usage | Notes |
| --- | --- | --- |
| RO | Field sourcing and application workflows. | Must confirm if device binding applies. |
| AM | Team monitoring, assignments, review workflows. | Role permissions after login need mapping. |
| PD / Credit Manager | Verification and assessment workflows. | Confirm exact role code. |
| Credit Analyst | Backend review or underwriting access. | Confirm whether this role logs into the same app. |
| Operations | Disbursement/closing workflows. | Confirm whether Ops uses this app login. |

## Product Requirements

| Requirement | Product meaning | Status |
| --- | --- | --- |
| Admin portal to configure roles and access. | Product/admin team can control role permissions. | Needs validation. |
| Staff ID management. | Admin can create, activate, deactivate, assign role, and change role. | Needs validation. |
| Login validation. | User must pass phone number + 6-digit OTP validation before app access. | Validated. |
| Audit trail of login. | Store staff ID, timestamp, geolocation, IP address, and success/failure where approved. | Required, privacy review needed. |
| Auto-logout after inactivity. | Session expires after 10 minutes of inactivity. | Confirm if 10 minutes is final. |
| Role-based routing after login. | User sees permitted workspace/actions based on role. | Required. |

## Screen Inventory

| Screen | Purpose | Main actions | User-visible states | Figma link |
| --- | --- | --- | --- | --- |
| Splash / app launch | Entry before login. | Auto-transition. | Loading. | TBD |
| Login screen | Capture staff phone number. | Enter registered mobile number and request OTP. | Empty, invalid format, unregistered/inactive staff. | TBD |
| OTP screen | Validate OTP if OTP login is current. | Enter OTP, submit, resend. | Pending, invalid, expired, resend timer. | TBD |
| Device warning / lockout | Warn/block unrecognized device if device binding is current. | Proceed, go back, okay/exit. | New phone warning, device mismatch lockout. | TBD |
| Authenticated handoff | Route to staff workspace. | None. | Login success, role context loaded. | TBD |

## Detailed Product Flow

### Standard Login Flow

1. Staff opens the app.
2. App shows splash/loading screen.
3. App routes to login screen.
4. Staff enters registered phone number.
5. App validates that the identifier format is acceptable.
6. Staff taps the login / request OTP CTA.
7. App validates whether the staff account exists and is active.
8. If valid, app moves to the next authentication step.
9. Staff completes 6-digit OTP verification.
10. If authentication succeeds, app creates a staff session.
11. App loads staff role and access context.
12. Staff is routed to the workspace/home dashboard.

### Failed Login Flow

1. Staff enters invalid, inactive, or unregistered credentials.
2. App blocks login.
3. App shows approved error copy.
4. Failed login event is recorded.
5. Staff remains on login screen and can retry if policy allows.

### OTP Flow If Mobile OTP Is Current

1. Staff enters registered mobile number.
2. App checks mobile number format.
3. Staff requests OTP.
4. App shows OTP entry screen.
5. Staff enters OTP.
6. If OTP is correct and valid, login continues.
7. If OTP is incorrect or expired, app shows OTP error state.
8. Staff can retry or resend based on the approved resend policy.

### Device Warning / Lockout Flow If Device Binding Is Current

1. Staff attempts login from a device that does not match the expected device record.
2. App shows warning or lockout screen.
3. If warning flow is allowed, staff can proceed or go back according to policy.
4. If hard lockout applies, app blocks login and shows a single exit/okay action.
5. Device mismatch outcome is recorded for audit.

### Inactivity Logout Flow

1. Staff is logged in.
2. Staff remains inactive for the configured inactivity window.
3. App automatically expires the session.
4. App routes staff back to login or session-expired screen.
5. Staff must authenticate again to continue.

## Validation Rules

| Rule | Source | Product note |
| --- | --- | --- |
| Login must validate active staff identity. | Requirements attachment. | Exact login method must be confirmed. |
| Staff ID format validation was mentioned but struck through. | Requirements attachment. | Treat as deprecated until confirmed. |
| Password validation was mentioned but struck through. | Requirements attachment. | Treat as deprecated until confirmed. |
| Forgot-password flow was mentioned but struck through. | Requirements attachment. | Treat as deprecated until confirmed. |
| Mobile number OTP login is described in rough app notes. | Rough documentation + Arnav validation. | Current login method. |
| Device binding is described in rough app notes. | Rough documentation. | Not present in pasted requirements; confirm with product/security. |
| Auto-logout after 10 minutes inactivity. | Requirements attachment. | Confirm final duration and behavior. |

## Business Rules

| Rule | Product behavior | Status |
| --- | --- | --- |
| Only active staff can log in. | Deactivated or inactive staff must be blocked. | Needs validation |
| Role access comes from staff configuration. | After login, user should see only allowed workspace/actions. | Needs validation |
| Login attempts require audit trail. | Success and failure attempts should be recorded with approved audit fields. | Required |
| Inactive sessions expire automatically. | App should auto-logout after approved inactivity duration. | Needs validation |
| Deprecated flows should not appear in UI. | Struck-through forgot-password/password flows should not be documented as live unless reconfirmed. | Needs validation |

## Events

| Event | Trigger | Status |
| --- | --- | --- |
| `StaffLoginClicked` | User taps login CTA. | Active requirement. |
| `StaffLoginSuccess` | Login succeeds. | Active requirement. |
| `StaffLoginFailed` | Login fails. | Active requirement. |
| `StaffForgotPasswordClicked` | User taps forgot password. | Struck through; confirm if removed. |
| `StaffForgotPasswordOTPTriggered` | Forgot password OTP triggered. | Struck through; confirm if removed. |
| `StaffForgotPasswordOTPValidated` | Forgot password OTP validated. | Struck through; confirm if removed. |
| `StaffResetPasswordSuccess` | Password reset succeeds. | Struck through; confirm if removed. |
| `StaffResetPasswordFailed` | Password reset fails. | Struck through; confirm if removed. |

## Audit And Data Logging

| Data | Trigger | Product note |
| --- | --- | --- |
| Staff ID | Login attempt. | Required for audit. |
| Staff mobile number | Login attempt if mobile login is used. | PII/internal sensitive. |
| Login timestamp | Login attempt. | Required. |
| Success/failure | Login attempt. | Required. |
| Geolocation | Login attempt. | Requires product/security/privacy confirmation. |
| IP address | Login attempt. | Requires engineering validation. |

## Acceptance Criteria

- Inactive/deactivated staff cannot log in.
- Successful login creates a valid staff session.
- Failed login shows a clear, approved error state.
- Login success/failure events are captured.
- Login audit trail stores required approved fields.
- Staff is routed to the correct role-based workspace after login.
- Session expires after the approved inactivity duration.

## Mismatches / Clarifications Needed

| Issue | Why it matters | Owner |
| --- | --- | --- |
| Latest login method is unclear: mobile OTP vs staff ID/password. | Product docs cannot be final until the canonical method is confirmed. | Arnav |
| Device binding appears only in rough documentation. | Need decide if it is live, future, or removed. | Arnav |
| Forgot password items are struck through in the source. | Avoid documenting deprecated flows as live. | Arnav |

## Open Questions

| Question | Owner | Needed from | Status |
| --- | --- | --- | --- |
| What is the current canonical staff login method? | Arnav | Product/engineering | Resolved: phone number + 6-digit OTP verification. |
| Is device binding in scope for Staff Login? | Arnav | Product/security | Partially resolved: IT administrator at head office can reset device binding/access. |
| Is forgot password removed from scope? | Arnav | Product | Open |
| Is auto-logout after 10 minutes final? | Arnav | Product/security | Open |
| Which roles use this login today? | Arnav | Product/manager | Open |
| What audit fields are mandatory and where are they reviewed? | Arnav | Product/security | Open |
