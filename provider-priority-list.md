# Provider Priority List

Canonical for provider documentation prioritization, not for provider behavior.

Owner: Dileepan
Status: draft
Last updated: 2026-06-08

## Priority Providers

| Priority | Provider | Expected doc | Initial focus | Status |
| --- | --- | --- | --- | --- |
| 1 | Digitap | `providers/digitap.md` | Use cases, API wiring, error behavior, retries/fallbacks, operational caveats | Selected |
| 2 | Digio | `providers/digio.md` | Use cases, callbacks/webhooks if any, signing/KYC flow, error behavior | Selected |
| 3 | Karza | `providers/karza.md` | Verification use cases, response handling, failure modes | Selected |
| 4 | Equifax | `providers/equifax.md` | Bureau pull, consent, error handling, data retention/PII caveats | Selected |
| 5 | CRIF | `providers/crif.md` | Bureau pull, request/response handling, operational caveats | Selected |
| 6 | MSG91 | `providers/msg91.md` | SMS/OTP/communication flows, retry behavior, template ownership | Later |
| 7 | Finflux | `providers/finflux.md` | LMS/core integration, state sync, operational failure handling | Later |

## Provider Documentation Rules

- Do not include secrets, tokens, credentials, raw production payloads, or PII.
- Use sanitized field examples only when needed.
- Link code paths where requests are created, sent, parsed, logged, retried, and failed.
- Capture known provider error patterns and operational actions.
- If real behavior is unclear, mark it as an open question.

