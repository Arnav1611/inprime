# InPrime Smart Loan Product Construct

Canonical for product intent, target customer, high-level product features, repayment behavior, loan offer rules, documentation, and open questions for InPrime Smart Loan.

Owner: Arnav  
Status: draft  
Last updated: 2026-06-15

## Source Links

| Source | Link/path | Notes |
| --- | --- | --- |
| Smart Loan product overview attachment | User-provided attachment | Product overview, customer segment, features, technical construct. |
| SMART Loan phase 1 attachment | User-provided attachment | Mobile flow, CRM changes, validations, test cases, observations. |
| SMART Loan application product doc | `new-loan-application-smart-loan.md` | Product-level app flow and 17-step checklist. |
| SMART Loan application flow doc | `../flows/new-loan-application-smart-loan.md` | Sequencing, handoffs, state transitions. |
| Product variants doc | `xpress-flow-product-variants.md` | Cross-product comparison. |
| Smart Loan process flow | https://whimsical.com/inprime-smart-loan-WsYHLJArVnUJqaQUisyrVC | High-level process flow from source. |

## Summary

InPrime Smart Loan is designed for small businesses in trade, service, and manufacturing in urban geographies. It is intended to provide flexible ticket size, repayment options, repayment frequency, digital servicing, and attractive pricing for small businesses.

## Target Customers

| Parameter | Criteria |
| --- | --- |
| Geography | Urban. |
| Age | 18 to 55. |
| Occupation | Trade, service, manufacturing. |
| Gender | Male or female. |
| Household income range | Rs. 5 lakh to Rs. 12 lakh. |
| Credit experience | 12 months and above. |
| Business location | Marketplace / commercial location. |
| Business premise | Dedicated business premise, not operated from residence. |

## Product Features

| Feature | Current value |
| --- | --- |
| Applicants | Minimum 1, maximum 2. |
| Loan amount | Rs. 50,000 to Rs. 3 lakh. |
| Tenure | 3 months to 36 months. |
| Interest rate | 25% per annum fixed. |
| Interest type | Declining / reducing balance. |
| Processing fee | 2.5% of approved loan amount + GST. |
| Purpose | Business Loan. |
| Repayment | Daily, weekly, fortnightly, or monthly. |
| Repayment modes | UPI Autopay, NACH, online payment via debit card/UPI. |
| Product code | 201. |
| Client type | Individual. |
| Disbursement to | Self / applicant. |

## Value Proposition

| Value proposition | Product meaning |
| --- | --- |
| Right loan amount | Uses business/income assessment to provide suitable loan amount based on need and capacity. |
| Better pricing | Designed to be attractive compared with digital loans and traditional business-place acquisition. |
| Flexible repayment | Supports repayment frequency based on business cashflow cycle. |
| Paperless process | Staff-assisted digital journey should make onboarding smoother and faster. |

## Charges And Repayment Rules

| Area | Rule |
| --- | --- |
| Processing fee | 2.5% of approved loan amount + GST, collected at disbursement. |
| Insurance charges | Credit Life Insurance charges as per insurance construct; first charge mandatory, second charge optional for co-applicant. |
| Late repayment penalty | Rs. 211.9 + GST, effectively Rs. 250, after 7-day grace period. |
| Foreclosure charges | 5% of outstanding principal. |
| Repayment structure | Equal instalments. |
| Repayment frequency | Daily, weekly, fortnightly, monthly as given by API. |
| EMI rounding | Only monthly EMI rounded to nearest 100. |
| Moratorium | 30 days for monthly, or as per weekly/daily frequency. |
| Day count | 365 days. |
| Interest calculation period | Daily. |
| NPA tagging | 90 days overdue. |

## Credit Assessment And Offer

| Area | Product behavior |
| --- | --- |
| Credit assessment | As per InPrime Credit Policy updated from time to time. |
| Assessment inputs | Personal and business KYC, demographics, credit history/current outstanding, household profile, household income, bank account, digital transactions. |
| BRE | Automated Business Rule Engine enables quick decisioning/rejection and quicker manual review. |
| Loan offer | Approved applications get maximum loan amount and maximum EMI. |
| Customer choice | Customer can choose loan amount up to maximum offer and tenure that meets maximum EMI criteria. |
| FOIR | Offer generated based on current and resultant FOIR sanctioned by Credit. |

## KYC And Loan Documentation

| Document / requirement | Product behavior |
| --- | --- |
| KYC | Collected and verified for all applicants as per InPrime KYC policy. |
| Business KYC | Personal and business KYC are part of assessment. |
| Loan Application Form | Collected with credit bureau consent. |
| Form 60 | Collected where applicant does not have PAN. |
| Loan Agreement | Signed as part of fulfilment. |
| Key Fact Statement | Signed/shared as required. |
| Insurance onboarding form | Required if insurance is opted. |
| E-sign | Aadhaar OTP and assisted biometric options enabled. |
| Physical signing | Available if customer is not willing to sign through Aadhaar e-sign. |

## Open Questions

| Question | Owner | Needed from | Status |
| --- | --- | --- | --- |
| Is SMART Loan live in the current staff app, or still planned/in rollout? | Arnav | Product/manager | Open |
| What exact UI step list applies to SMART Loan today? | Arnav | Product/design | Open |
| Is Reapply Review visible in the current 17-step SMART Loan app checklist? | Arnav | Product/design | Open |
| Which API provides repayment frequency options? | Dileepan | Engineering | Open |
| What is the exact DigiCal income assessment behavior and source? | Arnav + Dileepan | Product/credit/engineering | Open |
| Is first insurance charge mandatory for all Smart Loan cases? | Arnav | Product/insurance | Open |
