# My Leads

Canonical for product intent, screen behavior, add-lead fields, sorting, actions, dedupe, rejection behavior, acceptance criteria, and open questions for the **My Leads** bucket inside Lead Management.

Owner: Arnav  
Status: draft  
Last updated: 2026-06-29

## Source Links

| Source | Link/path | Notes |
| --- | --- | --- |
| Lead Management attachment | User-provided attachment | Priority source for My Leads behavior. |
| Leads parent doc | `leads.md` | Parent Lead Management module. |
| My Leads flow doc | `../flows/my-leads.md` | End-to-end sequence and handoffs. |
| App Figma | https://www.figma.com/design/F4TByjJMRTVNC8wFp8gNUq/InPrime-LOS?node-id=9438-20020&t=FTAjCUnQn0QQHMLo-4 | App lead design reference. |

## Scope

This document covers **My Leads**, the RO/self-sourced lead bucket inside Leads.

Out of scope:

- Digital Leads.
- Top-Up/Repeat leads.
- Retarget leads.
- Full loan application after Start Application.
- API implementation.

## Summary

My Leads lets ROs digitally record and track self-sourced leads that earlier may have existed only in diaries, brochures, customer callbacks, or field memory. ROs can add a lead, capture planned visit date, occupation, geotag, positive/negative points, business photo, and remarks, then follow up through call, directions, rejection, or application start.

For AMs, My Leads should show the same lead information plus RO name and support filtering/reallocation by RO within the AO.

## Business Objective

- Give ROs a structured way to manage self-sourced field leads.
- Improve follow-up discipline using planned visit dates.
- Create a digital trail for non-digital marketing activity.
- Help AMs monitor RO lead pipelines and reallocate leads when needed.
- Reduce duplicates using mobile-number dedupe.

## Users And Roles

| Role | My Leads behavior |
| --- | --- |
| RO | Adds, views, edits, follows up, rejects, calls, gets directions, and starts applications for own leads. |
| AM | Views My Leads for ROs in AO, sees RO name, filters by RO, and reallocates leads. |
| Customer | Represented by lead record; contacted by RO. |
| System | Stores lead, validates required fields, runs dedupe, geotag/address mapping, and routes actions. |

## Card Fields

| Field | Notes |
| --- | --- |
| Lead ID | Lead identifier. |
| Customer Name | PII; do not reproduce raw values in docs. |
| Mobile Number | PII and dedupe key. |
| Lead Capture Date | Date lead was added. |
| Planned Visit Date | Used for sorting and follow-up. |
| Occupation | Major occupation selected by RO. |
| Location | Pincode + Area, from geotag-to-address API. |
| RO Name | Shown additionally in AM view. |

## Sorting

- Sort by **Planned Visit Date**.
- Newer planned visit dates appear at the top.
- Leads without planned visit date appear at the bottom.

## Add Lead Form

| Field | Required? | Notes |
| --- | --- | --- |
| Customer Name | Yes | Manual entry. |
| Mobile Number | Yes | Primary dedupe key. |
| Lead Source | Yes | Manual dropdown; default upload sources are not shown. |
| Positive Points | No | Chip select/deselect. |
| Negative Points | No | Chip select/deselect. |
| Occupation | Yes | Major occupation dropdown. |
| Planned Visit Date | No | Used for sorting/follow-up. |
| Geotag Location | Yes | Required for My Leads creation. |
| Address | No | User input after geotag; can override API response. |
| Upload Business Photo | No | Confirm mandatory/optional. |
| Remarks | No | Free text. |

## Lead Source Dropdown

Manual dropdown values:

- Customer Referral.
- Doorstep Brochure.
- Ex-company Customer.
- Personal Network.
- Canopy Marketing.
- Poster.
- Van Marketing.

Default sources used only for auto-population and not shown in dropdown:

- Contact Centre.
- WhatsApp COM.

Customer Referral note:

- If **Customer Referral** is selected, a **Referred By** section opens.
- Staff must enter referral name and referral mobile number.

## Positive Points

Active chips from source:

- Good Income in Major Occupation.
- Own House.
- Own Business.
- Good Credit-O-Meter.
- Low Obligation.

## Negative Points

Active chips from source:

- No Loan Required.
- No Major Occupation.
- Not interested in InPrime.
- Less Income.
- Rented House.
- High Obligation.

## Occupation Dropdown

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

## Actions

| Action | Behavior |
| --- | --- |
| Reject Lead | Opens rejection reason screen with multi-select reasons and mandatory remarks. |
| Start Application | Navigates to Home Screen / Super-SMART product selection flow. |
| Call Customer | Opens phone/dialer. |
| Get Directions | Opens Google Maps using geotag/location. |
| Reallocate | AM-only; reallocates lead to another RO within AO. |
| Open lead | Shows Add Lead screen with pre-filled information. |

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

Mobile number is the primary dedupe key.

| Scenario | Expected behavior |
| --- | --- |
| RO adds a lead already added by another RO | Show `Lead - {Mobile Number} already added by {RO Name}`. |
| My Lead later appears in Digital Leads / COM | It appears in My Leads only as a COM lead. |

## Business Rules

| Rule | Behavior | Status |
| --- | --- | --- |
| My Leads are RO-created. | Leads appear in the user's My Leads bucket after save. | Source-backed. |
| AM view includes RO name. | AM can see which RO owns the lead. | Source-backed. |
| AM can reallocate. | AM reallocates to active RO within same AO. | Source-backed. |
| Planned visit date controls sorting. | Newer visit dates at top; missing dates at bottom. | Source-backed. |
| Mobile number dedupe is mandatory. | Duplicate mobile blocks lead creation. | Source-backed. |
| Geotag required. | Customer name, mobile number, lead source, and geotag are mandatory for creation. | Validated by Arnav. |

## Acceptance Criteria

- RO can open My Leads from Leads.
- RO can create a lead using plus button.
- Required fields are enforced.
- Duplicate mobile number is blocked with RO-name error.
- My Leads are sorted by planned visit date.
- Leads without planned visit date appear at bottom.
- AM can view RO name and reallocate leads within AO.
- Reject Lead requires reason and remarks.
- Start Application routes to product selection.
- Get Directions works only when usable location exists.

## Open Questions

| Question | Owner | Needed from | Status |
| --- | --- | --- | --- |
| Is geotag mandatory for old diary leads, or can staff mark location not captured at customer place? | Arnav | Product/business/design | Resolved: yes, geotag is mandatory. |
| Should My Leads be transferred to contact centre as hot leads? | Arnav | Product/contact centre | Open |
| Should customer referral capture referral mobile number? | Arnav | Product/design | Resolved: yes, referral name and mobile number are captured. |
| Are planned visit date notifications/nudges in scope? | Arnav | Product/engineering | Resolved: yes. |
| Should loan requirement be captured at lead stage? | Arnav | Product/credit | Resolved: no. |
| Should negative point chips be reduced further? | Arnav | Product/business | Open |
