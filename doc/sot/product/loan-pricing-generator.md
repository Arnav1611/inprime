# Loan Pricing Generator

Canonical for product intent, user-facing behavior, screens, business rules, acceptance criteria, and open questions for the Loan Pricing Generator / Loan Pricing Calculator module.

Owner: Arnav  
Status: draft  
Last updated: 2026-06-17

## Source Links

| Source | Link/path | Notes |
| --- | --- | --- |
| Home Dashboard product doc | `xpress-flow-home-dashboard.md` | Mentions `Loan Pricing Calculator` card and purpose. |
| Xpress Flow app product doc | `xpress-flow-app.md` | Mentions pricing as a dashboard module. |
| Product variants doc | `xpress-flow-product-variants.md` | Mentions product-wise amount/offer constraints. |
| Top-Up Loan product doc | `top-up-loan.md` | Latest Top-Up ticket-size rules and amount-limit mismatch. |
| New Loan Application product doc | `new-loan-application-super-welcome.md` | Contains current Super/Welcome product limits. |
| Rough app documentation | Google Doc: https://docs.google.com/document/d/1RjWx3gUFbFS1ZXHuyM2ElMg1ltK7SCu__IaIKMfZocM/edit?usp=sharing | Mentions dynamic loan offer/pricing behavior. |
| Flow doc | `../flows/loan-pricing-generator.md` | End-to-end flow and state transitions. |

## Naming

| Name | Usage |
| --- | --- |
| Loan Pricing Generator | Working documentation name requested by product. |
| Loan Pricing Calculator | Visible dashboard/module name in existing rough docs. |

## Scope

This document covers the internal staff app module used to estimate or generate loan pricing before or during a loan journey.

Out of scope:

- Provider-specific pricing APIs.
- Backend formula implementation.
- Public/customer-facing pricing pages.
- Final legal sanction letter format.
- Detailed accounting or finance posting logic.

## Summary

Loan Pricing Generator helps staff estimate loan cost and affordability by entering or selecting product, loan amount, tenure, and other required pricing inputs. The expected output may include EMI, fees, insurance, disbursement amount, and offer-related values.

The module is currently documented as a draft for exact formulas and ownership, but pricing output is official enough to show to the customer.

## Business Objective

- Help staff quickly estimate customer-facing loan pricing.
- Reduce manual calculation errors during customer discussion.
- Show product-specific limits before staff commits to a loan amount or tenure.
- Support informed loan requirement and offer conversations.
- Make pricing changes visible in real time when amount or tenure changes.

## Users And Roles

| Role | Product role in pricing | Open questions |
| --- | --- | --- |
| RO / Staff user | Opens pricing module, selects product, enters amount/tenure, and views estimated pricing. | Confirm exact roles allowed to access module. |
| AM / Manager | May use pricing for review, coaching, or approval discussion. | Confirm whether manager can generate pricing or only view. |
| Credit / Product team | Owns pricing policy, product limits, and formula approval. | Confirm final formula owner. |
| Customer | Does not directly use the internal module, but pricing may be discussed with customer by staff. | Confirm whether generated quote can be shared. |

## Screen Inventory

| Screen / module | Purpose | Expected behavior | Open questions |
| --- | --- | --- | --- |
| Home Dashboard card | Entry point. | User taps **Loan Pricing Calculator** / pricing card. | Confirm exact label: Calculator vs Generator. |
| Product selection | Select loan product. | User selects Super Loan, Welcome Loan, Top-Up Loan, Repeat Loan, MLAP / Micro LAP, SMART Loan, or another allowed product if later added. | Confirm exact UI labels and order. |
| Pricing input screen | Capture amount, tenure, and required values. | User enters pricing inputs; invalid values show validation errors. | Confirm field list and default values. |
| Pricing result screen | Show generated estimate. | EMI, fees, insurance, disbursement amount, and/or offer values update based on input. | Confirm exact output fields. |
| Save/share action | Preserve or share generated estimate. | Optional; only if product wants quote persistence. | Confirm whether pricing result is saved or temporary. |

## Detailed Product Flow

### 1. Entry From Home Dashboard

1. Staff logs in and reaches Home Dashboard.
2. Staff taps **Loan Pricing Calculator**.
3. App opens the Loan Pricing Generator module.
4. App should validate whether the staff role is allowed to use pricing.

### 2. Product Selection

1. Staff selects product.
2. App loads product-specific pricing limits and rules.
3. Each product follows product-specific amount limits.

Confirmed limits currently known:

| Product | Amount limit |
| --- | --- |
| Super Loan | Rs. 80,000 to Rs. 3 lakh. |
| Welcome Loan | Rs. 80,000 to Rs. 1.5 lakh |
| Top-Up Loan | Rs. 40,000 to Rs. 2 lakh |
| Repeat Loan | Rs. 40,000 to Rs. 3 lakh |
| MLAP / Micro LAP | Rs. 4 lakh to Rs. 10 lakh |
| SMART Loan | Rs. 50,000 to Rs. 3 lakh |
| Festival Loan | Rs. 25,000 to Rs. 40,000 |

### 3. Pricing Inputs

1. Staff enters loan amount.
2. Staff selects or enters tenure.
3. Staff enters any other required pricing inputs.
4. App validates product limits before generating result.
5. If amount or tenure changes, pricing should update dynamically.

Inputs to confirm:

| Input | Current understanding | Status |
| --- | --- | --- |
| Product | Required. | Product-wise limits follow the latest product-limit screenshot and product docs. |
| Loan amount | Required. | Validate against selected product limit. |
| Tenure | Required. | Tenure limits need confirmation. |
| Purpose | May be required if pricing is tied to loan requirement. | Needs confirmation. |
| Interest rate / ROI | Likely required or derived. | Needs confirmation. |
| Processing fee | May be calculated or shown. | Needs confirmation. |
| Insurance | Existing docs mention insurance in pricing estimate. | Needs confirmation. |
| Taxes/charges | May affect disbursement amount. | Needs confirmation. |

### 4. Pricing Generation

1. App calculates or fetches pricing output.
2. Result should update in real time when amount or tenure changes.
3. Staff should see a clear breakdown of customer-facing values.
4. Invalid inputs should prevent final generation or show clear correction message.

Expected outputs to confirm:

| Output | Current understanding | Status |
| --- | --- | --- |
| EMI | Mentioned in existing docs as loan cost estimate. | Needs formula/source confirmation. |
| Fees | Mentioned in existing docs. | Needs fee list confirmation. |
| Insurance | Mentioned in existing docs. | Needs product applicability confirmation. |
| Disbursement amount | Mentioned in existing docs. | Needs net-disbursement formula confirmation. |
| Total payable | Likely useful but not confirmed. | Open |
| Interest rate / ROI | Likely shown or derived. | Open |
| Tenure-wise comparison | Not confirmed. | Open |

### 5. Result Usage

1. Staff uses generated pricing for customer/product discussion.
2. If linked to an active application, pricing may support Loan Requirement or Loan Offer Generation.
3. If standalone, pricing may remain temporary unless product confirms save/share behavior.

Open items to confirm:

- Pricing is official enough to show to customer.
- Whether generated pricing is saved against lead/application/customer.
- Whether staff can share pricing with customer.
- Whether customer acknowledgement is required.

## Business Rules And Validations

| Area | Rule / validation | Status |
| --- | --- | --- |
| Access | Pricing module opens from Home Dashboard card. | Confirm role permissions. |
| Product | User must select a valid product before pricing. | Confirm supported products. |
| Super Loan amount | Allowed range is Rs. 80,000 to Rs. 3 lakh. | Latest product-limit screenshot. |
| Welcome Loan amount | Allowed range is Rs. 80,000 to Rs. 1.5 lakh. | Confirmed by Arnav. |
| Top-Up Loan amount | Allowed range is Rs. 40,000 to Rs. 2 lakh. | Latest product-limit screenshot. |
| Repeat Loan amount | Allowed range is Rs. 40,000 to Rs. 3 lakh. | Latest product-limit screenshot. |
| MLAP / Micro LAP amount | Allowed range is Rs. 4 lakh to Rs. 10 lakh. | Confirmed by Arnav. |
| SMART Loan amount | Allowed range is Rs. 50,000 to Rs. 3 lakh. | Confirmed by Arnav. |
| Amount validation | Amount outside product range must show error and block generation. | Draft. |
| Tenure validation | Tenure must be within product rules. | Needs limits. |
| Dynamic update | Pricing should change in real time when amount or tenure changes. | Source: rough docs for loan offer screen. |
| Formula authority | Pricing formula must come from approved product/credit source. | Needs owner. |
| Official vs advisory | Generated result is official enough to show customer, but must not override final BRE/offer rules. | Validated by Arnav. |
| Final offer linkage | Pricing generator must not override final BRE/offer rules. | Draft. |

## Analytics Events

Event names are draft until engineering validates naming.

| Event | Trigger |
| --- | --- |
| `LoanPricingCalculatorClicked` | User taps pricing card from Home Dashboard. |
| `LoanPricingProductSelected` | User selects product. |
| `LoanPricingInputChanged` | User changes amount, tenure, or pricing input. |
| `LoanPricingGenerated` | Pricing result is generated/refreshed. |
| `LoanPricingGenerationFailed` | Pricing cannot be generated due to validation or system issue. |
| `LoanPricingSaved` | User saves pricing result, if save exists. |
| `LoanPricingShared` | User shares pricing result, if share exists. |

## Acceptance Criteria

- Staff can open Loan Pricing Generator from the Home Dashboard pricing card.
- Staff can select a loan product before entering pricing values.
- Amount validation uses product-specific limits.
- Super Loan amount validation should follow the latest product-limit screenshot: Rs. 80,000 to Rs. 3 lakh.
- Welcome Loan amount outside Rs. 80,000 to Rs. 1.5 lakh is blocked.
- Top-Up Loan amount outside Rs. 40,000 to Rs. 2 lakh is blocked.
- Repeat Loan amount outside Rs. 40,000 to Rs. 3 lakh is blocked.
- MLAP / Micro LAP amount outside Rs. 4 lakh to Rs. 10 lakh is blocked.
- SMART Loan amount outside Rs. 50,000 to Rs. 3 lakh is blocked.
- Staff can enter or select tenure.
- Pricing output updates when amount or tenure changes.
- Result screen clearly shows calculated pricing values that product confirms as required.
- Validation errors clearly tell staff what to correct.
- The module can show pricing to customers, while still distinguishing calculator output from final BRE-approved loan offer where applicable.
- If pricing is saved or shared, the app records the action and shows confirmation.

## Mismatches Or Contradictions

| Issue | Impact | Status |
| --- | --- | --- |
| Existing dashboard docs call the module Loan Pricing Calculator, while current request calls it Loan Pricing Generator. | Naming may be inconsistent across docs and app UI. | Open |
| Rough docs mention dynamic loan offer changes, but separate pricing-generator formula is not documented. | Formula and output fields cannot be treated as canonical yet. | Open |
| Top-Up product amount limits conflicted across older sources. | Pricing validation can be wrong if old limits are used. | Updated to latest product-limit screenshot: Rs. 40,000 to Rs. 2 lakh. |

## Open Questions

| Question | Owner | Needed from | Status |
| --- | --- | --- | --- |
| What is the final feature name: Loan Pricing Generator or Loan Pricing Calculator? | Arnav | Product/design | Open |
| Which roles can access this module? | Arnav | Product/operations | Open |
| What are the tenure limits for each product? | Arnav | Product/credit | Open |
| What formula/source is used for EMI, fees, insurance, and net disbursement? | Arnav + Dileepan | Product/credit/engineering | Open |
| Is generated pricing advisory, official, or tied to final loan offer? | Arnav | Product/credit | Resolved: official enough to show customer; final BRE/offer rules still override. |
| Can staff save or share generated pricing? | Arnav | Product/operations | Open |
| Does pricing attach to a lead/application/customer record? | Arnav + Dileepan | Product/engineering | Open |
