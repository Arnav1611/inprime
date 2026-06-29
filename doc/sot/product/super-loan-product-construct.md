# InPrime Super Loan Product Construct

Canonical for product intent, target customer, high-level product features, repayment behavior, loan offer rules, documentation, and open questions for InPrime Super Loan.

Owner: Arnav  
Status: draft  
Last updated: 2026-06-15

## Source Links

| Source | Link/path | Notes |
| --- | --- | --- |
| Super Loan product overview attachment | User-provided attachment | Product overview, customer segment, features, technical construct. |
| New Loan Application product doc | `new-loan-application-super-welcome.md` | Staff app journey for Super/Welcome application. |
| Product variants doc | `xpress-flow-product-variants.md` | Cross-product comparison. |
| Pre-closure runbook | `../runbooks/super-loan-pre-closure.md` | Operational pre-closure process. |

## Summary

InPrime Super Loan is designed for Informal Prime customers: informal economy households with a proven credit track record, growing digital adoption, and need for higher ticket-size credit across multiple purposes.

## Target Customers

| Characteristic | Product definition |
| --- | --- |
| Segment | Informal Prime customers. |
| Household income | Rs. 4 lakh to Rs. 10 lakh annual income. |
| Economy type | Informal economy; income may not be well documented like salaried or GST-registered businesses. |
| Credit track record | 5+ years credit history, often upgraded from micro loans, two-wheeler loans, or gold loans. |
| Cash behavior | Moving from cash to less-cash ecosystem. |
| Digital behavior | At least one smartphone with active WhatsApp in the household. |
| Occupations | Micro businesses, small/marginal farmers, livestock owners, informal service providers such as carpenter, plumber, electrician. |

## Product Features

| Feature | Current value |
| --- | --- |
| Applicants | Minimum 2, maximum 3. |
| Loan amount | Rs. 80,000 to Rs. 3 lakh. |
| Tenure | 6 months to 36 months. |
| Interest rate | 25% per annum fixed. |
| Interest type | Declining / reducing balance. |
| Processing fee | 2.5% of approved loan amount + GST. |
| Purpose | Business, house improvement, agriculture, livestock, personal/consumption. |
| Repayment | Monthly EMI. |
| Repayment modes | NACH, UPI Autopay, online payment, debit card/UPI, BBPS, cash points. |
| Disbursement to | Self / applicant. |
| Client type | Individual. |
| Product code | 101. |

## Value Proposition

| Value proposition | Product meaning |
| --- | --- |
| Higher loan amount | Gives informal prime customers access to larger ticket-size credit than typical micro-loan limits. |
| Multiple purposes | Supports business, house improvement, agriculture, livestock, and consumption needs. |
| Easier repayment | Supports digital and assisted repayment channels instead of only cash/center meetings. |
| Paperless process | Staff-assisted digital journey should reduce friction and errors. |
| Quick turnaround | Digital onboarding, verification, and BRE should enable faster decisions. |

## Credit Assessment And Offer

| Area | Product behavior |
| --- | --- |
| Credit assessment | As per InPrime Credit Policy updated from time to time. |
| Assessment inputs | KYC, demographics, credit history/current outstanding, household profile, household income, bank account, digital transactions. |
| BRE | Automated Business Rule Engine enables quick loan decisioning, rejection, and manual review. |
| Loan offer | Approved applications get maximum loan amount and maximum EMI. |
| Customer choice | Customer can choose loan amount up to maximum offer and tenure that meets maximum EMI criteria. |
| FOIR | Offer generated based on current and resultant FOIR sanctioned by Credit. |

## Repayment And Accounting Rules

| Area | Rule |
| --- | --- |
| Repayment structure | Equated Monthly Instalments. |
| Number of instalments | 6 to 36, same as tenure. |
| Repayment date | Fixed date of month. |
| EMI rounding | Nearest hundred. |
| Moratorium | Minimum 30 days between disbursement and first instalment. |
| Day count | 365 days. |
| Interest calculation period | Daily. |
| Broken period interest | Adjusted to first EMI. |
| Late repayment penalty | Rs. 211.9 + GST, effectively Rs. 250, after 7-day grace period. |
| NPA tagging | 90 days overdue. |
| Stop interest accrual on NPA | Yes. |

## KYC And Loan Documentation

| Document / requirement | Product behavior |
| --- | --- |
| KYC | Collected and verified for all applicants as per InPrime KYC policy. |
| Loan Application Form | Collected with credit bureau consent. |
| Form 60 | Collected where applicant does not have PAN. |
| Loan Agreement | Signed as part of fulfilment. |
| Key Fact Statement | Signed/shared as required. |
| Insurance onboarding form | Required if insurance is opted. |
| E-sign | Aadhaar OTP and assisted biometric options enabled. |
| Physical signing | Available if customer is not willing to sign through Aadhaar e-sign. |

## Product Mismatch To Resolve

| Issue | Source A | Source B | Current accepted doc value | Status |
| --- | --- | --- | --- | --- |
| Super Loan amount range differed across earlier drafts. | Older interim notes included Rs. 80,000 to Rs. 1 lakh. | Latest product-limit screenshot and Arnav validation show Rs. 80,000 to Rs. 3 lakh. | Rs. 80,000 to Rs. 3 lakh. | Resolved for current product docs. |

## Open Questions

| Question | Owner | Needed from | Status |
| --- | --- | --- | --- |
| Are repayment modes all live today or phased? | Arnav | Product/operations | Open |
| Is Credit Life Insurance optional for all Super Loan applicants? | Arnav | Product/insurance | Open |
| Which exact repayment channels are available in staff app vs customer channels? | Arnav | Product/operations | Open |
| Where should GL/accounting details live: product doc, finance runbook, or tech/LMS doc? | Arnav + Dileepan | Finance/ops/engineering | Open |
