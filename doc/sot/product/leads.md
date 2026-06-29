# Leads / Lead Management

Canonical for product intent, lead categories, screens, visible fields, add-lead behavior, lead actions, rejection rules, dedupe, reallocation, CRM upload behavior, acceptance criteria, and open questions for the Lead Management module.

Owner: Arnav  
Status: draft  
Last updated: 2026-06-29

## Source Links

| Source | Link/path | Notes |
| --- | --- | --- |
| Lead Management attachment | User-provided attachment | Priority source for this draft. |
| Rough app documentation | Google Doc: https://docs.google.com/document/d/1RjWx3gUFbFS1ZXHuyM2ElMg1ltK7SCu__IaIKMfZocM/edit?usp=sharing | Base staff app source. |
| Home Dashboard product doc | `xpress-flow-home-dashboard.md` | Leads card from dashboard. |
| My Leads product doc | `my-leads.md` | Focused doc for RO-created/self-sourced leads. |
| Digital Leads product doc | `digital-leads.md` | Focused doc for imported/campaign leads. |
| Retarget Leads product doc | `retarget-leads.md` | Focused doc for old rejected applications that may now be eligible. |
| Top-Up Loan product doc | `top-up-loan.md` | Top-Up starts from Leads > Top-up tab. |
| Repeat Loan product doc | `repeat-loan.md` | Repeat currently appears under Top-up section but marked Repeat. |
| Flow doc | `../flows/leads.md` | End-to-end sequencing, handoffs, API touchpoints, state transitions. |
| My Leads flow doc | `../flows/my-leads.md` | Focused My Leads sequence. |
| Digital Leads flow doc | `../flows/digital-leads.md` | Focused Digital Leads sequence. |
| Retarget Leads flow doc | `../flows/retarget-leads.md` | Focused Retarget sequence. |
| Web Figma | https://www.figma.com/design/IyJk7N4pu3glJSKAyzUZH7/Web---InPrime-LOS?node-id=12156-16950&t=4erwxgXpaiWYPNDC-4 | CRM/web lead design reference. |
| App Figma | https://www.figma.com/design/F4TByjJMRTVNC8wFp8gNUq/InPrime-LOS?node-id=9438-20020&t=FTAjCUnQn0QQHMLo-4 | App lead design reference. |
| Tech doc | TBD | Dileepan to map collections, APIs, dedupe logic, CRM upload, and role permissions. |

## Scope

This document covers the **Lead Management** module in the staff app and its CRM upload/source behavior.

Out of scope:

- Full underwriting and application checklist after Start Application.
- Final Top-Up/Repeat eligibility rules.
- Provider-specific integrations.
- Raw customer PII.
- Detailed API implementation.

## Summary

Lead Management helps staff track, prioritize, contact, reject, reallocate, and convert leads. It creates a digital record for leads that were earlier handled informally through brochures, field visits, call-centre lists, WhatsApp campaign flows, and existing-customer retention lists.

Leads are grouped into:

- **My Leads**: self-sourced/manual leads added by RO.
- **Digital Leads**: marketing/campaign/call-centre leads such as WhatsApp Credit-O-Meter leads.
- **Top-up Leads**: existing customers with disbursed loans and retention/top-up opportunity.
- **Rejected Leads**: leads rejected from active buckets.
- **Retarget Leads**: old rejected applications that may now be eligible after filters and PR are run. Current validation says Retarget is no longer in use.

## Business Objective

- Give ROs a structured way to track self-sourced leads.
- Improve follow-up discipline through planned visit date and lead details.
- Centralize digital, Top-Up, Repeat, and retargeting opportunities.
- Help AMs monitor and reallocate leads across ROs within an AO.
- Reduce duplicate leads using mobile-number dedupe.
- Improve conversion by showing positive/negative lead indicators and pass-status signals.

## Lead Collections

| Collection | What it contains | Examples |
| --- | --- | --- |
| Leads with no loan application generated | Leads not yet converted into loan application. | WhatsApp leads, My Leads, Other Digital Leads. |
| Leads with disbursed file | Existing borrowers eligible for retention journeys. | Top-Up leads, Repeat leads where applicable. |
| Old rejected applications that may now be eligible | Retarget Leads. | Eligibility is identified using filters and PR, then shared to RO in Leads > Retarget. |

## Lead Types

| Lead type | Meaning | Source / current behavior |
| --- | --- | --- |
| My Leads | Leads manually added by RO through the plus button. | Used for self-sourced leads from field/marketing activity. |
| Digital Leads | Leads imported from marketing/campaign/call-centre sources. | Includes WhatsApp Credit-O-Meter and contact-centre leads. |
| Top-up Leads | Existing customers who have already availed a loan and may be eligible for additional disbursement. | Previously inside All Loan Files; now moved to Leads. |
| Repeat Leads | Existing-customer retention leads. | Currently shown under Top-up section but marked/tagged Repeat. |
| Retarget Leads | Previously rejected applications that may now be eligible. | No longer in use per latest validation. Keep historical docs for reference only. |
| Rejected Leads | Leads rejected from active buckets. | Current/Phase 2 behavior differs; see Rejected Leads section. |

## Common Lead Data Model

For leads with no loan application generated, source recommends storing the below and selectively showing fields to staff.

| Field | Required? | Notes |
| --- | --- | --- |
| Mobile Number | Yes | Primary dedupe key. PII. |
| Name | Yes | Customer name. PII. |
| Lead Capture Date | Yes | Capture/import date. |
| Lead Type | Yes | COM, My Lead, Contact Centre, etc. |
| Area Office | Yes | Used for assignment/reallocation. |
| Lead Source | Conditional | Applicable for My Leads. |
| Pincode | No | Used to derive area. |
| Planned Visit Date | No | Drives My Leads sort order. |
| RO | No | Assigned RO. AM view shows RO name. |
| Occupation | No | Major occupation dropdown for My Leads. |
| Geotag | Yes for My Leads creation | Required with customer name, mobile number, and lead source. |
| Area Name | No | Derived from pincode/geotag where available. |
| House ownership | No | Lead profiling signal. |
| Business Premise Ownership | No | Lead profiling signal. |
| Bureau Pass Status | No | Based on WhatsApp Credit-O-Meter. |
| Prime Test Pass Status | No | Based on contact-centre calling. |
| Positive Points | No | Chips. |
| Negative Points | No | Chips. |
| Photo | No | Business/customer photo. |
| Lead Converted | No | Y/N with application ID. |
| Lead Rejected | No | Y/N. |
| Lead Rejection Reason | Conditional | Required when rejecting. |
| Lead Rejection DateTimestamp | Conditional | Set on rejection. |

## App Entry Point

1. Staff logs in.
2. Staff opens Home Dashboard.
3. Staff taps **Leads**.
4. Leads opens below/after Loan Files in main navigation as per source.

## Lead Buckets / Tabs

| Bucket | Product purpose | Current behavior |
| --- | --- | --- |
| My Leads | RO-created/self-sourced leads. | Shows leads added by user via plus button. |
| Top-up | Existing-borrower retention leads. | Includes Top-Up leads; Repeat may currently appear here with Repeat tag. |
| Digital | Imported digital/campaign/call-centre leads. | Uses star prioritization based on Prime Test and Bureau pass. |
| Rejected | Rejected leads. | Current source says rejected leads shown here with no actions; Phase 2 expands fields/tags. |
| Retarget | Previously rejected applications that may now be eligible for InPrime Loan. | No longer in use per latest validation. |

## My Leads

### Card Fields

| Field | Notes |
| --- | --- |
| Lead ID | Lead identifier. |
| Customer Name | PII; do not reproduce raw values in docs. |
| Mobile Number | PII. |
| Lead Capture Date | Date lead was added. |
| Planned Visit Date | Used for sorting. |
| Occupation | Major occupation. |
| Location | Pincode + Area, derived from geotag-to-address API. |
| RO Name | Shown additionally in AM view. |

### Sorting

- My Leads are sorted by **Planned Visit Date**.
- Newer dates appear at the top.
- Leads without planned visit date go to the bottom.

### Add Lead Form

The plus button opens Add Lead.

| Field | Required? | Notes |
| --- | --- | --- |
| Customer Name | Yes | Manual entry. |
| Mobile Number | Yes | Primary dedupe key. |
| Lead Source | Yes | Dropdown excludes default auto-population sources. |
| Positive Points | No | Chip select/deselect. |
| Negative Points | No | Chip select/deselect. |
| Occupation | Yes | Major occupation dropdown. |
| Planned Visit Date | No | Used for follow-up sorting. |
| Geotag Location | Yes | Required for My Leads creation. |
| Address | No | User input after geotag; can override API response address. |
| Upload Business Photo | No | Confirm mandatory/optional. |
| Remarks | No | Free text. |

Lead Source dropdown:

- Customer Referral.
- Doorstep Brochure.
- Ex-company Customer.
- Personal Network.
- Canopy Marketing.
- Poster.
- Van Marketing.

Default sources used only for auto population, not shown in dropdown:

- Contact Centre.
- WhatsApp COM.

Customer Referral note:

- If **Customer Referral** is selected, a **Referred By** section opens.
- Staff must enter referral name and referral mobile number.

Positive point chips:

- Good Income in Major Occupation.
- Own House.
- Own Business.
- Good Credit-O-Meter.
- Low Obligation.

Negative point chips:

- No Loan Required.
- No Major Occupation.
- Not interested in InPrime.
- Less Income.
- Rented House.
- High Obligation.

Source list had additional struck-through/de-scoped chips. Do not treat them as active until product confirms.

### Occupation Dropdown

Major occupation options from source:

- Livestock Animal Husbandry.
- Salaried Organised.
- Kirana or Provision Store.
- Tailoring.
- Sericulture.
- Hotel or Eatery.
- Maestri Gare Mason.
- Salon/Beauty Parlor.
- Tea Shop.
- Flour Mill.
- Service Business.
- Iron Shop.
- Cloth Business.
- Trade or Sales Business.
- Roti Manufacturing.
- Bakery.
- Fancy and Cosmetic Store.
- Woodwork and Furniture Manufacturing.
- Bar Bending Maestri.
- Vegetables and Fruits Shop.
- Photo Studio.
- Stationery & Xerox Shop.
- Manufacturing.
- Event Planning.
- Welding Work.
- Footwear Shop.
- Juice Centre.
- Electric Services.
- Flower Business.
- Mobile Services and Sales.

## Digital Leads

Digital Leads are imported from a master file and include WhatsApp Credit-O-Meter and contact-centre/campaign leads.

### Card Fields

| Field | Notes |
| --- | --- |
| Lead ID | Auto-generated. |
| Customer Name | PII. |
| Mobile Number | PII. |
| Lead Capture Date | Auto-populated from COM generated date. |
| Location | Pincode + Area from pincode. |
| RO Name | Shown additionally in AM view. |

### Stars / Prioritization

Digital Leads show two stars:

| Star | Meaning |
| --- | --- |
| Blue star | Prime Test Pass. |
| Yellow star | Bureau Pass. |

Sorting:

1. Two-star leads first.
2. Single-star leads next, with bureau then prime priority.
3. No-star leads last.
4. Planned visit date is combined into sorting.

### Digital Lead Edit / Save

When user taps a Digital Lead, the Add Lead screen opens pre-filled:

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

Once saved, filled information should be saved. For Digital Leads in this edit mode, all fields are non-mandatory per source.

## Top-Up Leads

- Top-Up leads inside All Loan Files should be moved to Leads.
- Lead cards should show existing-customer context such as mobile, last disbursement date, EMIs paid, and current InPrime OSP.
- Top-Up details live in `top-up-loan.md`.
- Repeat currently appears under Top-up section with Repeat tag; details live in `repeat-loan.md`.
- The green/check indicator on lead cards signifies where/how the lead was generated.

## Rejected Leads

Current behavior:

- Rejected leads appear in Rejected bucket.
- Fields shown:
  - Lead ID.
  - Customer Name.
  - Mobile Number.
  - Lead Capture Date.
  - RO Name for AM view.
- No actions are available.
- When user taps a lead, show Lead Rejected Reason and Lead Rejected Remarks.

Phase 2 behavior:

- Show list of all rejected leads with tag for lead type: Top-up, Digital, Retarget, My Leads.
- For non-Top-Up rejected leads, show:
  - Lead ID.
  - Customer Name.
  - Mobile Number.
  - Lead Capture Date.
  - Occupation.
  - Location: Pincode + Area.
  - RO Name for AM view.
- For Top-Up rejected leads, show usual Top-Up info: mobile, last disbursement date, EMIs paid, current InPrime OSP.

## Lead Actions

| Action | Applies to | Behavior |
| --- | --- | --- |
| Reject Lead | My Leads, Digital, Top-Up, Retarget if enabled | Opens rejection reason screen with multi-select checkboxes and mandatory remarks. |
| Start Application | My Leads, Digital, Top-Up, Retarget depending on lead type | For My/Digital, navigate to Home Screen Super/Smart Loan selection flow. For Top-Up, start Top-Up flow. |
| Call Customer | All active lead types | Opens phone/dialer. |
| Get Directions | Leads with geotag/location | Opens Google Maps. For Digital Leads, disabled if geotag unavailable. |
| Reallocate | AM view | AM reallocates lead to another RO within same AO. |
| Open lead card | My/Digital | Shows Add Lead screen with pre-filled information. |

## Lead Rejection Reasons

Reject Lead screen should allow multiple checkbox selection and mandatory remarks.

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

## CRM / Lead Master

CRM path: **CRM > Master > Lead Master** with upload option.

### Digital Leads Upload File

| Field | Required? | Notes |
| --- | --- | --- |
| Name | Yes | Customer name. |
| Mobile Number | Yes | Dedupe key. |
| Lead Generated Date | Yes | Capture date. |
| Area Office | Yes | Assignment context. |
| Pincode | Yes | Used to map staff. |
| Area Name | No | Optional. |
| Staff ID | Yes | Map automatically if pincode exists. Assign to RO with more cases; if no RO available, assign to AM for Digital Leads. |
| Nature of Occupation | No | Optional. |
| Bureau Pass Status | No | Based on WhatsApp Credit-O-Meter. |
| Prime Test Pass Status | No | Based on contact-centre calling. |

### Top-Up Leads Upload File

| Field | Required? | Notes |
| --- | --- | --- |
| Core Loan Application ID | Yes | Existing loan reference. |
| No of EMIs Paid | Yes | Retention eligibility context. |
| Current InPrime OSP | Yes | Outstanding principal/exposure context. |

## Dedupe Logic

| Scenario | Expected behavior |
| --- | --- |
| RO adds a mobile number already added by another RO | Show: `Lead - {Mobile Number} already added by {RO Name}`. |
| CRM upload contains mobile number already in lead collection | Show/download failure: `Lead - {Mobile Number} already available with {RO Name}`. |
| CRM upload has duplicate records | Final handling needs confirmation. |

For CRM upload duplicates, source proposes either:

- Add the error message in downloadable failure file against each record.
- Or show all duplicate mobile numbers as a longer-duration toast with copy feature.

If the toast approach is used, the entire file should not be processed.

## Reallocation

| Scenario | Behavior |
| --- | --- |
| AM reallocates lead | AM can reallocate My Leads, Top-Up, Digital, and other active leads to different RO within AO. |
| RO resigns / assigned RO changes | Leads should migrate as part of assigned RO flow. |
| Disbursed file reallocation | If there is an active Top-Up, reallocate that as well. |

## Retarget Leads

Focused Retarget behavior is documented in `retarget-leads.md`.

Historical/current reference behavior:

- Retarget is no longer in use per latest validation. The below points remain historical/reference only until product reactivates it.
- Retarget was a separate tab under Leads.
- Retarget leads are old rejected loan applications that may now be eligible.
- Eligibility is established by applying filters on old applications and then running PR.
- Eligible cases are added from backend using an upload/process; no CRM/upload feature is needed in current scope.
- Card data includes Applicant 1 name, Applicant 1 mobile number, last application date, occupation from Prime Test, UI location, and Get Direction location.
- UI location is decided from pincode and micro area entered in the old application.
- Get Direction uses Applicant 1 selfie location.
- Reject Lead works similar to Digital Leads.

Older discussion points that still need validation before being treated as current scope:

- Whether mobile number change/KYC updates should retain old details for historical application context rather than overwrite original captured details.
- Whether applicant delete/proceed behavior is needed for Applicant 2 or Applicant 3.
- Whether usual application rejection and lead rejection need separate visible reason sets.
- Which product route retarget customers should enter after Start Application.
- Whether income must be reassessed if the old case had reached PD stage.

## Open Points From Source

- Saving a lead does not automatically trigger WhatsApp COM campaign today. Backend team verifies and sends the WhatsApp message.
- Should My Leads be transferred to contact centre as hot leads?
- If a My Lead later enters COM/Digital Leads, it may not map to the same RO because RO assignment logic is based on number of applications.
- Customer referral opens Referred By fields for referral name and mobile number.
- Planned visit date notifications/nudges may be needed.
- Loan requirement is not captured at lead stage.
- Geotag is required for My Leads creation.
- Negative points list may need reduction.
- How to capture customers demanding higher amount than current product feature?
- More detailed dedupe scenarios need final product/engineering decision.

## Acceptance Criteria

- Staff can open Leads from Home Dashboard.
- Leads module shows approved buckets as per rough doc/current design; Retarget is no longer in use unless reactivated.
- RO can add My Leads using the plus button.
- My Leads add form enforces required fields: customer name, mobile number, lead source, occupation, and geotag.
- Mobile-number dedupe blocks duplicate lead creation.
- My Leads are sorted by Planned Visit Date, with missing dates at bottom.
- Digital Leads show Prime/Bureau star indicators and sort by stars plus planned visit date.
- Staff can reject leads with reason multi-select and mandatory remarks.
- Staff can call customer and get directions where location exists.
- Start Application routes to correct downstream product flow.
- AM can view RO name and reallocate leads within AO where permitted.
- Rejected Leads are read-only and show rejection reason/remarks.

## Open Questions

| Question | Owner | Needed from | Status |
| --- | --- | --- | --- |
| What is the final bucket/tab list: My Leads, Top-up, Digital, Rejected, Retarget, Repeat? | Arnav | Product/design | Partially resolved: follow rough doc; Retarget no longer in use; Repeat remains under Top-up tab. |
| Is Repeat a separate tab or only a tag inside Top-up? | Arnav | Product/design | Resolved: same Top-up tab. |
| Which fields are searchable and filterable in each lead bucket? | Arnav + Dileepan | Product/engineering | Resolved for product: new to old and date range; exact API behavior in tech doc. |
| Is geotag mandatory for old diary leads, or can staff mark not captured at customer place? | Arnav | Product/design/business | Resolved: yes, geotag is required. |
| Should Save send WhatsApp COM campaign message? | Arnav | Product/marketing/engineering | Resolved: not automatic today; backend verifies and sends WhatsApp. |
| What is the final dedupe behavior for CRM upload duplicates: failure file or toast/copy? | Arnav + Dileepan | Product/engineering | Open |
| What exact statuses exist for Lead Converted and Lead Rejected? | Dileepan | Engineering/code | Open |
| Which roles can add, reject, reallocate, and start application for each lead type? | Arnav + Dileepan | Product/engineering | Partially resolved: RO/AM can act; exact permission matrix in tech doc. |
| What is the final Retarget lead product flow? | Arnav | Product/credit | Resolved: no longer in use. |
| Are planned visit date notifications in scope for current phase? | Arnav | Product/engineering | Resolved: yes. |
