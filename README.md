# Source of Truth Knowledge Base

This directory is the internal knowledge base for product and engineering teams.
It is intended to become a structured, reviewable source of truth for how the
product works, how core flows behave, how the system is implemented, and how
third-party providers and operational workflows behave.

## Directory Ownership

| Area | Canonical for | Primary owner |
| --- | --- | --- |
| `product/` | Product intent, roles, screens, business rules, acceptance criteria, Figma and PRD links | Arnav |
| `flows/` | End-to-end journeys, sequencing, handoffs, touchpoints, state transitions, exception paths | Arnav and Dileepan |
| `tech/` | Implementation details, APIs, code paths, DTOs, entities, repos, services, controllers | Dileepan |
| `providers/` | Third-party provider behavior, code wiring, error handling, fallbacks, operational caveats | Dileepan |
| `runbooks/` | Operational procedures, diagnosis steps, escalation paths | Shared |
| `faq/` | Repeated product and engineering questions | Shared |
| `glossary.md` | Shared vocabulary and status definitions | Arnav |

## Documentation Rules

- Do not guess. If the answer is unclear, add it to `open-questions.md`.
- Every meaningful doc must state what it is canonical for.
- Link related PRDs, Figma screens, APIs, code paths, providers, runbooks, and FAQs.
- Product and flow docs should link to detailed API truth in `tech/` instead of duplicating it.
- If product intent, Figma, docs, and code disagree, call out the mismatch explicitly.
- Do not include secrets, tokens, raw production provider payloads, PII, or sensitive screenshots.
- Use sanitized examples only.

## Status Values

Use these status values in document frontmatter or metadata tables:

- `draft`: Created but not reviewed.
- `source-inventory`: Source links collected, but canonical content not complete.
- `ready-for-review`: Complete enough for product/engineering review.
- `reviewed`: Reviewed by the named stakeholder.
- `needs-update`: Known to be stale or contradicted by newer source material.

