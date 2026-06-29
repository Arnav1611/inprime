# Digital Leads

Canonical for product intent, upload source, screen behavior, card fields, star prioritization, edit/save behavior, actions, dedupe, acceptance criteria, and open questions for **Digital Leads**.

Owner: Arnav  
Status: draft  
Last updated: 2026-06-29

## Source Links

| Source | Link/path | Notes |
| --- | --- | --- |
| Lead Management attachment | User-provided attachment | Priority source for Digital Leads behavior. |
| Leads parent doc | `leads.md` | Parent Lead Management module. |
| Digital Leads flow doc | `../flows/digital-leads.md` | End-to-end sequence and handoffs. |
| Web Figma | https://www.figma.com/design/IyJk7N4pu3glJSKAyzUZH7/Web---InPrime-LOS?node-id=12156-16950&t=4erwxgXpaiWYPNDC-4 | CRM/web lead design reference. |
| App Figma | https://www.figma.com/design/F4TByjJMRTVNC8wFp8gNUq/InPrime-LOS?node-id=9438-20020&t=FTAjCUnQn0QQHMLo-4 | App lead design reference. |

## Scope

This document covers **Digital Leads**, the imported/campaign lead bucket inside Leads.

Out of scope:

- My Leads/manual lead creation.
- Top-Up/Repeat lead eligibility.
- Retarget leads.
- Full CRM implementation.
- Detailed API implementation.

## Summary

Digital Leads are leads imported from marketing, WhatsApp Credit-O-Meter, contact-centre, and other digital sources. These leads are uploaded into CRM Lead Master and shown to staff in the app with key fields, Prime/Bureau pass indicators, and follow-up actions.

Digital Leads are prioritized using star indicators:

- Blue star: Prime Test Pass.
- Yellow star: Bureau Pass.

## Business Objective

- Convert centrally sourced digital/campaign leads into field follow-ups.
- Give ROs a prioritized queue based on Prime/Bureau pass status.
- Allow AMs to monitor Digital Leads by RO and reallocate within AO.
- Preserve campaign/import source while allowing RO to enrich lead information.
- Prevent duplicates using mobile-number dedupe.

## CRM Upload Source

CRM path: **CRM > Master > Lead Master**.

Digital Leads upload file:

| Field | Required? | Notes |
| --- | --- | --- |
| Name | Yes | Customer name. |
| Mobile Number | Yes | Primary dedupe key. |
| Lead Generated Date | Yes | Auto-populates Lead Capture Date. |
| Area Office | Yes | Assignment context. |
| Pincode | Yes | Used to fetch/map area and staff. |
| Area Name | No | Optional. |
| Staff ID | Yes | Map automatically if pincode exists; assign to RO with more cases; if no RO available, assign to AM. |
| Nature of Occupation | No | Optional. |
| Bureau Pass Status | No | Based on WhatsApp Credit-O-Meter. |
| Prime Test Pass Status | No | Based on contact-centre calling. |

## Card Fields

| Field | Notes |
| --- | --- |
| Lead ID | Auto-generated. |
| Customer Name | PII. |
| Mobile Number | PII and dedupe key. |
| Lead Capture Date | Auto-populated from COM/generated date. |
| Location | Pincode + Area, fetched from pincode. |
| RO Name | Shown additionally in AM view. |
| Blue star | Prime Test Pass. |
| Yellow star | Bureau Pass. |

## Sorting / Prioritization

| Priority | Lead type |
| --- | --- |
| 1 | Two-star leads. |
| 2 | Single-star leads with Bureau priority. |
| 3 | Single-star leads with Prime priority. |
| 4 | No-star leads. |

Planned visit date is combined into sorting.

## Digital Lead Edit / Save

When user taps a Digital Lead, the app opens the Add Lead screen with pre-filled information:

- Customer Name.
- Mobile Number.
- Lead Capture Date.
- Lead Source default WhatsApp COM.
- Positive Points.
- Negative Points.
- Occupation.
- Nature of occupation.
- Planned Visit Date.
- Geotag Location.
- Address.
- Upload Business Photo.
- Remarks.

For Digital Leads in this edit mode, source says all fields are non-mandatory. Whatever the user fills and saves should be saved.

## Actions

| Action | Behavior |
| --- | --- |
| Reject Lead | Opens rejection screen with multi-select reasons and mandatory remarks. |
| Start Application | Navigates to Home Screen / Super-SMART product selection flow. |
| Call Customer | Opens phone/dialer. |
| Get Directions | Opens Google Maps only if geotag is available; disabled otherwise. |
| Reallocate | AM-only; reallocates lead to another RO within AO. |
| Open lead | Opens pre-filled Add Lead screen. |

## Rejection Reasons

- Loan Not Required.
- No Major Occupation.
- Document Not available.
- Long Distance.
- Already High Obligation.
- Not in working area.
- Low Income.
- Need higher loan amount.
- Co-applicant not interested.
- Rented House.
- Profile not suitable.
- Negative profile.

## Dedupe

Mobile number is the primary key for dedupe.

| Scenario | Expected behavior |
| --- | --- |
| CRM upload includes a mobile number already in lead collection | Error: `Lead - {Mobile Number} already available with {RO Name}`. |
| Failure-file approach | Error shown against each failed row in downloadable file. |
| Toast approach | Show all duplicate numbers in long-duration toast with copy feature; entire file should not be processed. |
| My Lead later comes through Digital/COM | Owner mapping may differ because Digital assignment logic uses RO application count/pincode. Needs final rule. |

## Business Rules

| Rule | Behavior | Status |
| --- | --- | --- |
| Digital Leads are imported. | Created through CRM Lead Master upload/master file. | Source-backed. |
| AM view includes RO name. | AM can see assigned RO and filter/reallocate within AO. | Source-backed. |
| Star indicators drive priority. | Two stars first, then single-star, then no-star. | Source-backed. |
| Get Directions depends on geotag. | Disabled if geotag unavailable. | Source-backed. |
| Edit fields are non-mandatory. | User can save whatever is filled. | Source-backed. |
| Mobile-number dedupe is mandatory. | Duplicate import should fail or block file processing based on final UX. | Source-backed; final UX open. |

## Acceptance Criteria

- CRM upload can create Digital Leads from required file fields.
- Digital Leads show Lead ID, name, mobile, lead capture date, and location.
- AM view shows RO name.
- Prime/Bureau pass stars are visible and correctly mapped.
- Digital Leads are sorted by star priority and planned visit date.
- Tapping a lead opens pre-filled Add Lead screen.
- Saving optional enrichment fields updates the lead.
- Get Directions is disabled when geotag is unavailable.
- Reject Lead requires reason and remarks.
- Duplicate mobile numbers are handled through the approved failure-file/toast behavior.

## Open Questions

| Question | Owner | Needed from | Status |
| --- | --- | --- | --- |
| What final duplicate upload behavior should be used: failure file or toast/copy? | Arnav + Dileepan | Product/engineering | Open |
| Should saving a Digital Lead trigger WhatsApp COM campaign message? | Arnav | Product/marketing/engineering | Open |
| If a My Lead later appears as Digital/COM, which RO owns it? | Arnav | Product/business | Open |
| What exact assignment rule decides RO with more cases from pincode? | Dileepan | Engineering/data | Open |
| Which Digital Lead fields can be edited after save? | Arnav + Dileepan | Product/engineering | Open |
