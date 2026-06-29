# Product Operating System

Canonical for product function principles, ownership boundaries, prioritization, and operating model used to evaluate product work and documentation quality.

Owner: Arnav  
Status: draft  
Last updated: 2026-06-15

## Source Links

| Source | Link/path | Notes |
| --- | --- | --- |
| Product operating-system attachment | User-provided attachment | Purpose, principles, scope, ownership, prioritization, buy vs build. |

## Purpose

The Product function should create a reliable, business-impact-led operating system that compounds InPrime's growth by:

- Designing scalable business backbones rooted in efficiency, quality, and reliability.
- Building contextual products and technologies for Informal Prime customers and internal stakeholders.
- Orchestrating builders, customers, internal stakeholders, and partners to maximize short-term and strategic business outcomes.

## Guiding Principles

| Principle | Meaning for product docs |
| --- | --- |
| Business-impact-first | Every feature/doc should state business impact, adoption plan, and release risk where applicable. |
| Reliability built-in | Workflows, migrations, and partner integrations should include risk controls, monitoring, and fallback paths. |
| Ownership boundaries | Product defines intent/rules/outcomes; Tech owns implementation quality; Business/Ops/Credit operate BAU. |

## Product Scope

| Scope area | Product responsibility |
| --- | --- |
| Technology-enabled change | Define problem, options, tradeoffs, workflow, rules, exceptions, risk, and rollout approach. |
| Customer value proposition | Own customer promise and lifecycle for loans, insurance, and digital financial products. |
| Requirements architecture | Translate business intent into workflows, states, rules, exception paths, and acceptance criteria. |
| Temporary operation of 0-to-1 initiatives | Own governance, issue identification, adoption, iteration, and handoff until BAU where needed. |

## Product-Tech Operating Model

| Stage | Product role | Tech role |
| --- | --- | --- |
| Problem framing | Lead with stakeholders: problem, user, constraints, success metrics, impact claim. | Provide feasibility input. |
| Solution design | Define workflow, systems, data, rules, exception handling, compliance needs. | Shape architecture and implementation approach. |
| Delivery | Provide clarity, user stories, acceptance criteria, test scenarios, rollout plan. | Execute engineering delivery. |
| Release and rollout | Joint ownership of checklist, monitoring, rollback readiness. | Own release engineering and incident response. |
| Adoption and outcomes | Drive adoption, training, communication, and outcome verification. | Support instrumentation and fixes. |
| Lifecycle management | Share performance/reliability review and enhancement decisions. | Own platform reliability and tech debt. |

## Ownership Boundaries

| Function | Owns |
| --- | --- |
| Product | Strategy, value proposition, problem framing, prioritization, workflows, rules, exceptions, adoption, outcome realization. |
| Tech | Architecture quality, scalability, security, code quality, platform reliability, observability, deployment, performance. |
| Business/Ops/Credit | Day-to-day BAU execution, SOP adherence, frontline adoption, operational controls, feedback and escalation. |

## Prioritization

| Lane | Meaning |
| --- | --- |
| Business Impact | Features/changes tied to measurable revenue, volume, risk reduction, time saved, or productivity. |
| Reliability/Hygiene | Stability, security, performance, compliance, and operational resilience. |
| Strategic | Work that may not have immediate measurable outcome but supports the InPrime business model. |

## Documentation Implications

- Product docs should include business objective, users, business rules, acceptance criteria, adoption/ops impact, and open questions.
- Flow docs should include handoffs, state transitions, exception paths, and operational ownership.
- Runbooks should define responsibilities, timelines, controls, and exception handling.
- Provider docs should include failure modes, fallbacks, retries, owner boundaries, and operational caveats.
- Docs should not claim impact or behavior that cannot be sourced.

## Open Questions

| Question | Owner | Needed from | Status |
| --- | --- | --- | --- |
| Should every product feature doc include a business-impact claim section? | Arnav | Product reviewer | Open |
| What template should be used for adoption plan and release risk plan? | Arnav | Product/manager | Open |
| Which 0-to-1 initiatives are currently temporarily operated by Product? | Arnav | Product/manager | Open |
