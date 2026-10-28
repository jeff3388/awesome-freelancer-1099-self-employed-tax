# Awesome Freelancer & 1099 Self-Employed Tax [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated reference for independent contractors, freelancers, gig workers, and sole proprietors navigating US self-employment taxes — covering SE tax, Schedule C, QBI deduction, quarterly estimated payments, and key deductions. All formulas cite official IRS sources.

---

## Contents

- [1099 Form Types](#1099-form-types)
- [Self-Employment Tax (SE Tax)](#self-employment-tax-se-tax)
- [Schedule C — Profit or Loss from Business](#schedule-c--profit-or-loss-from-business)
- [Qualified Business Income (QBI) Deduction — Section 199A](#qualified-business-income-qbi-deduction--section-199a)
- [Quarterly Estimated Tax Payments](#quarterly-estimated-tax-payments)
- [Key Self-Employment Deductions](#key-self-employment-deductions)
- [SE Health Insurance Deduction](#se-health-insurance-deduction)
- [Home Office Deduction](#home-office-deduction)
- [Vehicle Expenses](#vehicle-expenses)
- [Retirement Contributions for Self-Employed](#retirement-contributions-for-self-employed)
- [Python Implementations](#python-implementations)
- [Safe Harbor Rules](#safe-harbor-rules)
- [Common 1099 Mistakes & Audit Flags](#common-1099-mistakes--audit-flags)
- [See Also](#see-also)
- [Official IRS Sources](#official-irs-sources)

---

## 1099 Form Types

The IRS uses multiple 1099 forms to report non-wage income. Knowing which form applies prevents misreporting.

| Form | What It Reports | Who Files It | 2026 Threshold |
|------|----------------|--------------|----------------|
| **1099-NEC** | Nonemployee compensation (freelance, contract work) | Businesses paying ≥ $600 to a contractor | $600 |
| **1099-MISC** | Rent, royalties, prizes, attorney payments, other income | Various payers | $600 (most items) |
| **1099-K** | Payment card / third-party network transactions (Venmo, PayPal, Stripe) | Payment processors | $2,500 (2026 transitional) |
| **1099-INT** | Interest income | Banks, brokerages | $10 |
| **1099-DIV** | Dividends and distributions | Brokerages, mutual funds | $10 |
| **1099-B** | Proceeds from broker transactions | Brokerages | Any amount |
| **1099-G** | Government payments (unemployment, state tax refunds) | Government agencies | $10 |
| **1099-R** | Distributions from pensions, IRAs, annuities | Plan administrators | $10 |
| **1099-S** | Proceeds from real estate transactions | Settlement agents | $600 |
| **1099-SA** | HSA / Archer MSA distributions | Financial institutions | Any amount |

> **Source:** [IRS About Form 1099-NEC](https://www.irs.gov/forms-pubs/about-form-1099-nec) · [IRS About Form 1099-K](https://www.irs.gov/forms-pubs/about-form-1099-k)

### 1099-NEC vs. 1099-MISC: Key Distinction

- **1099-NEC** (Box 1): Freelance/contractor payments for services — filed directly on Schedule C
- **1099-MISC** (Box 2): Royalties; (Box 3): Other income; (Box 1): Rent — filing location depends on box

> **Note:** Even without a 1099, all self-employment income must be reported. The IRS receives 1099s from payers and will match them to your return.

---

## Self-Employment Tax (SE Tax)

Self-employed individuals pay both the employee and employer share of FICA taxes via Schedule SE.

### 2026 SE Tax Rates

| Component | Rate | Wage Base |
|-----------|------|-----------|
| Social Security | 12.4% | $176,100 (2026 SS wage base) |
| Medicare | 2.9% | No limit |
| **Combined SE tax rate** | **15.3%** | Up to $176,100 |
| Medicare only (above wage base) | 2.9% | Above $176,100 |
| Additional Medicare Tax | 0.9% | Above $200,000 (single) / $250,000 (MFJ) |

> **Source:** [IRS Publication 334 — Tax Guide for Small Business](https://www.irs.gov/publications/p334) · [IRS Schedule SE Instructions](https://www.irs.gov/instructions/i1040sse)

### SE Tax Calculation

```
Net Earnings from Self-Employment = Gross SE Income − Business Expenses

SE Tax Base = Net SE Income × 92.35%
  (The 7.65% reduction mirrors the employer deduction an employee would receive)

SE Tax = SE Tax Base × 15.3%  (if SE Tax Base ≤ $176,100)
       = ($176,100 × 15.3%) + ((SE Tax Base − $176,100) × 2.9%)  (if above wage base)

SE Tax Deduction = SE Tax × 50%
  (Deductible on Schedule 1, Line 15 — reduces AGI, not just taxable income)
```

### Example: $80,000 Net Self-Employment Income

```
SE Tax Base:   $80,000 × 0.9235 = $73,880
SE Tax:        $73,880 × 0.153  = $11,304
SE Deduction:  $11,304 × 0.50   = $5,652
```

The $5,652 deduction reduces your adjusted gross income, which in turn reduces your income tax (but not the SE tax itself).

---

## Schedule C — Profit or Loss from Business

Schedule C is filed by sole proprietors and single-member LLCs (disregarded entities) to report business income and deductions.

### Schedule C Structure

```
Part I — Income
  Line 1:  Gross receipts / sales
  Line 2:  Returns and allowances
  Line 4:  Cost of goods sold (from Part III)
  Line 7:  Gross income (Line 1 − Line 2 − Line 4 + other income)

Part II — Expenses
  Line 8:   Advertising
  Line 9:   Car and truck expenses
  Line 10:  Commissions and fees
  Line 11:  Contract labor
  Line 12:  Depletion
  Line 13:  Depreciation (Form 4562)
  Line 14:  Employee benefit programs
  Line 15:  Insurance (other than health)
  Line 16:  Interest (mortgage or other)
  Line 17:  Legal and professional services
  Line 18:  Office expense
  Line 19:  Pension and profit-sharing plans
  Line 20:  Rent or lease
  Line 21:  Repairs and maintenance
  Line 22:  Supplies
  Line 23:  Taxes and licenses
  Line 24:  Travel and meals (50% meals limit)
  Line 25:  Utilities
  Line 26:  Wages
  Line 27:  Other expenses

  Net Profit (Line 31) = Gross Income − Total Expenses
```

> **Source:** [IRS Schedule C Instructions](https://www.irs.gov/instructions/i1040sc)

### Ordinary and Necessary Expense Standard

An expense is deductible if it is:
1. **Ordinary** — common and accepted in your trade or business
2. **Necessary** — helpful and appropriate for your business

Personal expenses are never deductible. Mixed-use items (phone, car) must be prorated by business-use percentage.

---

## Qualified Business Income (QBI) Deduction — Section 199A

The QBI deduction allows eligible self-employed individuals and pass-through business owners to deduct up to **20% of qualified business income**, reducing effective tax rates on SE income.

### 2026 Thresholds

| Filing Status | Phase-Out Begins | Phase-Out Complete |
|---------------|------------------|--------------------|
| Single / HOH / MFS | $197,300 | $247,300 |
| Married Filing Jointly | $394,600 | $494,600 |

> **Source:** [IRS Revenue Procedure 2025-28](https://www.irs.gov/irb/2025-19_IRB) · [IRS Publication 535](https://www.irs.gov/publications/p535)

### QBI Deduction Rules

**Below the threshold (full deduction available):**
```
QBI Deduction = min(QBI × 20%, Taxable Income × 20%)
```

**Above the threshold (W-2 wage / capital limitations apply):**
```
W-2 Wage Limit = max(W-2 Wages × 50%, W-2 Wages × 25% + UBIA × 2.5%)
QBI Deduction = min(QBI × 20%, W-2 Wage Limit)
```

> **Sole proprietors and single-member LLCs with no W-2 employees** have a W-2 wage amount of $0. Above the threshold, their QBI deduction phases to $0 unless they have Unadjusted Basis Immediately After Acquisition (UBIA) of qualified property.

### Specified Service Trades or Businesses (SSTBs)

SSTBs have an **income-based phase-out** and receive **no QBI deduction** above the upper threshold. SSTBs include:
- Health (doctors, dentists, nurses)
- Law
- Accounting
- Actuarial science
- Performing arts
- Consulting
- Athletics
- Financial services
- Brokerage services

**Not SSTBs:** Engineering, architecture, real estate, insurance agents, retail, restaurants.

---

## Quarterly Estimated Tax Payments

Self-employed individuals must pay taxes as income is earned — not just at filing. Quarterly estimated payments cover income tax + SE tax.

### 2026 Payment Deadlines

| Payment Period | Due Date |
|---------------|----------|
| January 1 – March 31 | **April 15, 2026** |
| April 1 – May 31 | **June 16, 2026** |
| June 1 – August 31 | **September 15, 2026** |
| September 1 – December 31 | **January 15, 2027** |

> **Source:** [IRS Form 1040-ES Instructions](https://www.irs.gov/forms-pubs/about-form-1040-es)

### Estimated Payment Calculation

```
Annual Tax Liability = Income Tax + SE Tax − Credits − Withholding

Quarterly Payment = Annual Tax Liability ÷ 4
```

### Annualized Income Installment Method

For freelancers with uneven income, the annualized installment method (Form 2210, Schedule AI) calculates each quarter's required payment based on actual YTD income rather than 25% of annual estimated liability. This prevents overpaying in slow quarters.

---

## Key Self-Employment Deductions

### Schedule C Deduction Categories

| Deduction | Notes | IRS Source |
|-----------|-------|------------|
| Advertising | Digital ads, business cards, website costs | Pub 535 |
| Business insurance | E&O, general liability, professional liability | Pub 535 |
| Business meals | 50% deductible; must be business purpose | IRC §274 |
| Computer/software | Full Section 179 expensing or depreciation | Pub 946 |
| Contract labor | 1099-NEC required if ≥ $600 to any contractor | Pub 334 |
| Education | Must maintain/improve skills in current field | Pub 970 |
| Home office | Exclusive regular-use room; see below | Pub 587 |
| Legal/professional fees | Attorney, accountant, bookkeeper | Pub 535 |
| Phone/internet | Business-use percentage only | Pub 535 |
| Professional subscriptions | Trade journals, software, memberships | Pub 535 |
| Startup costs | Up to $5,000 in year 1; remainder amortized | IRC §195 |
| Travel | Airfare, hotel, 50% meals when away overnight | Pub 463 |
| Vehicle | See Vehicle section below | Pub 463 |

---

## SE Health Insurance Deduction

Self-employed individuals may deduct **100% of health insurance premiums** for themselves, their spouse, and dependents — directly on Schedule 1 (above-the-line deduction), not on Schedule C.

### Rules

- The deduction cannot exceed **net profit** from the business
- Not available for any month the taxpayer was **eligible for employer-sponsored coverage** (including through a spouse's employer)
- Includes medical, dental, vision, and long-term care insurance premiums

```
SE Health Insurance Deduction = min(Premiums Paid, Net SE Profit)
```

> **Source:** [IRS Publication 535, Chapter 6](https://www.irs.gov/publications/p535) · [IRC §162(l)](https://www.law.cornell.edu/uscode/text/26/162)

---

## Home Office Deduction

The home office deduction requires the space be used **regularly and exclusively** for business. Two methods:

### Method 1: Simplified Method

```
Deduction = Business-Use Square Footage × $5
Maximum = 300 sq ft × $5 = $1,500/year
```

- No depreciation recapture on home sale
- No Form 8829 required
- Cannot create a loss (but can carry forward unused amount)

### Method 2: Regular / Actual Expense Method

```
Business-Use Percentage = Office Sq Ft ÷ Total Home Sq Ft

Deductible Portion of:
  - Mortgage interest or rent
  - Homeowner's/renter's insurance
  - Utilities
  - Repairs and maintenance
  - Depreciation (residential rental recovery period: 39 years)

Deduction = (Business-Use %) × Qualifying Expenses
```

- Can produce a larger deduction than simplified method
- Depreciation creates a recapture event on home sale (Section 1250 unrecaptured gain, taxed at max 25%)
- Requires Form 8829

> **Source:** [IRS Publication 587 — Business Use of Your Home](https://www.irs.gov/publications/p587)

---

## Vehicle Expenses

Two methods for deducting business vehicle use. Choose the method that produces the larger deduction.

### Method 1: Standard Mileage Rate

| Year | Rate per Mile |
|------|--------------|
| 2025 | 70 cents ($0.70) |
| 2024 | 67 cents ($0.67) |
| 2023 | 65.5 cents ($0.655) |

```
Vehicle Deduction = Business Miles × $0.70  (2025 rate)
```

- Parking fees and tolls are deductible **in addition** to the mileage rate
- Cannot use standard rate if you claimed MACRS depreciation in a prior year
- Mileage log required: date, destination, business purpose, miles

### Method 2: Actual Expense Method

```
Business-Use Percentage = Business Miles ÷ Total Miles

Deductible Amount = (Business-Use %) × (Gas + Insurance + Repairs + Registration + Depreciation)
```

- Depreciation limited by luxury auto limits (IRC §280F): 2026 first-year limit ~$12,400 without bonus depreciation
- Section 179 and bonus depreciation available for SUVs > 6,000 lbs GVWR

> **Source:** [IRS Publication 463 — Travel, Gift, and Car Expenses](https://www.irs.gov/publications/p463)

---

## Retirement Contributions for Self-Employed

Self-employed individuals have access to tax-advantaged retirement plans with **significantly higher limits** than employee 401(k) plans.

### 2026 Contribution Limits

| Plan | Employee/Elective | Employer/Total | Catch-Up (Age 50+) |
|------|------------------|----------------|---------------------|
| **Solo 401(k)** — Employee | $23,500 | — | +$7,500 (age 50–59, 64+) |
| **Solo 401(k)** — Employer (25% of net SE income) | — | $70,000 combined | +$11,250 (age 60–63, SECURE 2.0) |
| **SEP-IRA** | — | 25% of net SE income (max $70,000) | No catch-up |
| **SIMPLE IRA** | $16,500 | Employer match required | +$3,500 (age 50+) |

### Solo 401(k) Formula

```
Net SE Income = Gross SE Income − Business Expenses

Net Earnings = Net SE Income × 92.35%  (removes employer-half of SE tax)
Compensation = Net Earnings − (SE Tax Deduction)
             = Net Earnings × (1 − 0.5 × 0.153)

Employee Elective Deferral = min($23,500, Compensation)
Employer Profit-Sharing = min(Compensation × 25%, $70,000 − Employee Deferral)
Total Contribution = Employee Deferral + Employer Profit-Sharing
```

> **Source:** [IRS One-Participant 401(k) Plans](https://www.irs.gov/retirement-plans/one-participant-401k-plans) · [IRS Publication 560](https://www.irs.gov/publications/p560)

---

## Python Implementations

```python
from dataclasses import dataclass, field
from typing import Optional

# 2026 Constants — Source: IRS Rev. Proc. 2025-28, Schedule SE Instructions
SS_WAGE_BASE_2026 = 176_100
SE_TAX_RATE_COMBINED = 0.153       # Social Security (12.4%) + Medicare (2.9%)
SE_TAX_RATE_MEDICARE_ONLY = 0.029  # Above SS wage base
ADDITIONAL_MEDICARE_THRESHOLD_SINGLE = 200_000
ADDITIONAL_MEDICARE_THRESHOLD_MFJ = 250_000
ADDITIONAL_MEDICARE_RATE = 0.009
SE_BASE_MULTIPLIER = 0.9235        # Net SE income × 92.35% = SE tax base


@dataclass
class SEIncomeResult:
    gross_se_income: float
    business_expenses: float
    net_se_income: float
    se_tax_base: float
    se_tax: float
    se_tax_deduction: float        # 50% of SE tax, deductible on Schedule 1
    net_after_se_deduction: float  # Net SE income minus SE deduction (for income tax)


def calculate_se_tax(
    gross_se_income: float,
    business_expenses: float,
    filing_status: str = 'single'
) -> SEIncomeResult:
    """
    Calculate self-employment tax per IRS Schedule SE.
    Source: https://www.irs.gov/instructions/i1040sse

    Args:
        gross_se_income: Total 1099/freelance receipts
        business_expenses: Schedule C deductible expenses
        filing_status: 'single', 'mfj', 'hoh', 'mfs'
    """
    net_se_income = gross_se_income - business_expenses
    if net_se_income <= 0:
        return SEIncomeResult(gross_se_income, business_expenses, net_se_income,
                               0, 0, 0, 0)

    se_tax_base = net_se_income * SE_BASE_MULTIPLIER

    if se_tax_base <= SS_WAGE_BASE_2026:
        se_tax = se_tax_base * SE_TAX_RATE_COMBINED
    else:
        se_tax = (SS_WAGE_BASE_2026 * SE_TAX_RATE_COMBINED +
                  (se_tax_base - SS_WAGE_BASE_2026) * SE_TAX_RATE_MEDICARE_ONLY)

    # Additional Medicare Tax (0.9%) — not part of SE tax, assessed on Form 8959
    # Threshold depends on filing status
    threshold = (ADDITIONAL_MEDICARE_THRESHOLD_MFJ
                 if filing_status == 'mfj'
                 else ADDITIONAL_MEDICARE_THRESHOLD_SINGLE)
    if se_tax_base > threshold:
        se_tax += (se_tax_base - threshold) * ADDITIONAL_MEDICARE_RATE

    se_tax_deduction = se_tax * 0.50
    net_after_se_deduction = net_se_income - se_tax_deduction

    return SEIncomeResult(
        gross_se_income=gross_se_income,
        business_expenses=business_expenses,
        net_se_income=net_se_income,
        se_tax_base=se_tax_base,
        se_tax=se_tax,
        se_tax_deduction=se_tax_deduction,
        net_after_se_deduction=net_after_se_deduction,
    )


@dataclass
class QBIResult:
    net_qbi: float
    qbi_deduction: float
    is_sstb: bool
    above_threshold: bool
    w2_wage_limit: float
    final_deduction: float


def calculate_qbi_deduction(
    net_qbi: float,
    taxable_income: float,
    filing_status: str = 'single',
    is_sstb: bool = False,
    w2_wages: float = 0.0,
    ubia_qualified_property: float = 0.0,
) -> QBIResult:
    """
    Calculate Section 199A QBI deduction per IRS Form 8995 / 8995-A.
    Source: https://www.irs.gov/instructions/i8995

    Args:
        net_qbi: Net qualified business income (after SE deductions)
        taxable_income: Taxable income before QBI deduction
        filing_status: 'single', 'mfj', 'hoh', 'mfs'
        is_sstb: True if Specified Service Trade or Business
        w2_wages: W-2 wages paid by the business (0 for sole proprietors with no employees)
        ubia_qualified_property: Unadjusted basis of qualified depreciable property
    """
    # 2026 thresholds — Source: IRS Rev. Proc. 2025-28
    threshold_low = 394_600 if filing_status == 'mfj' else 197_300
    threshold_high = 494_600 if filing_status == 'mfj' else 247_300
    phase_out_range = threshold_high - threshold_low  # $100,000 MFJ / $50,000 others

    above_low = taxable_income > threshold_low
    above_high = taxable_income >= threshold_high

    # SSTB phase-out: no deduction at or above upper threshold
    if is_sstb and above_high:
        return QBIResult(net_qbi, 0, True, True, 0, 0)

    # Compute tentative QBI deduction (20% of QBI)
    tentative = net_qbi * 0.20

    # W-2 wage / UBIA limitation (only applies above lower threshold)
    w2_limit = max(w2_wages * 0.50, w2_wages * 0.25 + ubia_qualified_property * 0.025)

    if not above_low:
        # Below lower threshold: no wage limitation
        applicable_w2_limit = tentative
    elif above_high:
        # Above upper threshold: full wage limitation applies
        applicable_w2_limit = w2_limit
    else:
        # In phase-out range: interpolate
        phase_fraction = (taxable_income - threshold_low) / phase_out_range
        reduction = max(0, tentative - w2_limit) * phase_fraction
        applicable_w2_limit = tentative - reduction

    # For SSTB in phase-out range, also phase-out the QBI amount
    if is_sstb and above_low and not above_high:
        phase_fraction = (taxable_income - threshold_low) / phase_out_range
        net_qbi_applicable = net_qbi * (1 - phase_fraction)
        tentative = net_qbi_applicable * 0.20
        applicable_w2_limit = min(applicable_w2_limit, tentative)

    qbi_deduction = min(tentative, applicable_w2_limit)
    # Overall limitation: 20% of taxable income (before QBI deduction) minus net capital gains
    overall_limit = taxable_income * 0.20
    final_deduction = max(0, min(qbi_deduction, overall_limit))

    return QBIResult(
        net_qbi=net_qbi,
        qbi_deduction=tentative,
        is_sstb=is_sstb,
        above_threshold=above_low,
        w2_wage_limit=w2_limit,
        final_deduction=final_deduction,
    )


@dataclass
class EstimatedTaxResult:
    annual_tax_estimate: float
    quarterly_payment: float
    safe_harbor_prior_year: float
    safe_harbor_current_year: float
    recommended_quarterly: float


def calculate_estimated_tax(
    estimated_annual_income: float,
    estimated_deductions: float,
    estimated_credits: float = 0.0,
    prior_year_tax: float = 0.0,
    prior_year_agi: float = 0.0,
    filing_status: str = 'single',
) -> EstimatedTaxResult:
    """
    Calculate quarterly estimated tax payments per Form 1040-ES.
    Source: https://www.irs.gov/forms-pubs/about-form-1040-es

    Safe harbors (avoids underpayment penalty):
      - 90% of current year tax, OR
      - 100% of prior year tax (110% if prior year AGI > $150,000)
    """
    # Simplified income tax estimate (2026 brackets, single)
    # For production use, integrate full bracket calculations
    taxable_income = max(0, estimated_annual_income - estimated_deductions)

    # SE tax (approximate)
    se_result = calculate_se_tax(estimated_annual_income * 0.9, 0)
    se_tax = se_result.se_tax
    se_deduction = se_result.se_tax_deduction

    # Approximate income tax (2026 single brackets — simplified)
    adj_taxable = max(0, taxable_income - se_deduction)
    income_tax = _approximate_income_tax_2026(adj_taxable, filing_status)

    total_tax = income_tax + se_tax - estimated_credits
    quarterly = total_tax / 4

    # Safe harbor calculations
    high_income_multiplier = 1.10 if prior_year_agi > 150_000 else 1.00
    safe_harbor_prior = (prior_year_tax * high_income_multiplier) / 4
    safe_harbor_current = (total_tax * 0.90) / 4

    # Pay the LESSER of the two safe harbors to minimize over-payment
    recommended = min(safe_harbor_prior, safe_harbor_current) if prior_year_tax > 0 else quarterly

    return EstimatedTaxResult(
        annual_tax_estimate=total_tax,
        quarterly_payment=quarterly,
        safe_harbor_prior_year=safe_harbor_prior,
        safe_harbor_current_year=safe_harbor_current,
        recommended_quarterly=recommended,
    )


def _approximate_income_tax_2026(taxable_income: float, filing_status: str) -> float:
    """2026 tax brackets (single). Source: IRS Rev. Proc. 2025-28."""
    if filing_status == 'mfj':
        brackets = [
            (23_850, 0.10),
            (96_950, 0.12),
            (206_700, 0.22),
            (394_600, 0.24),
            (501_050, 0.32),
            (751_600, 0.35),
            (float('inf'), 0.37),
        ]
    else:  # single, hoh, mfs
        brackets = [
            (11_925, 0.10),
            (48_475, 0.12),
            (103_350, 0.22),
            (197_300, 0.24),
            (250_525, 0.32),
            (626_350, 0.35),
            (float('inf'), 0.37),
        ]
    tax = 0.0
    prev = 0.0
    for upper, rate in brackets:
        if taxable_income <= prev:
            break
        taxable_in_bracket = min(taxable_income, upper) - prev
        tax += taxable_in_bracket * rate
        prev = upper
    return tax


def calculate_home_office_deduction(
    home_sqft: float,
    office_sqft: float,
    annual_rent_or_mortgage_interest: float,
    annual_utilities: float,
    annual_insurance: float,
    annual_repairs: float,
    home_value: float = 0.0,
    method: str = 'auto',
) -> dict:
    """
    Compare simplified vs. actual home office deduction.
    Source: IRS Publication 587

    Args:
        method: 'simplified', 'actual', or 'auto' (returns both, picks larger)
    """
    # Simplified method: $5/sq ft, max 300 sq ft
    simplified = min(office_sqft, 300) * 5.0

    # Actual method
    business_pct = office_sqft / home_sqft if home_sqft > 0 else 0
    direct_expenses = annual_utilities * business_pct
    indirect_expenses = (annual_rent_or_mortgage_interest + annual_insurance + annual_repairs) * business_pct
    # Annual depreciation (residential: 39 years, land excluded)
    # Typically land = 20-25% of home value
    depreciable_basis = home_value * 0.80 if home_value > 0 else 0
    annual_depreciation = (depreciable_basis / 39.0) * business_pct
    actual = direct_expenses + indirect_expenses + annual_depreciation

    return {
        'simplified_deduction': simplified,
        'actual_deduction': actual,
        'business_use_pct': round(business_pct * 100, 1),
        'recommended': 'actual' if actual > simplified else 'simplified',
        'recommended_amount': max(simplified, actual),
        'depreciation_recapture_risk': annual_depreciation > 0,
    }


def calculate_vehicle_deduction(
    business_miles: float,
    total_miles: float,
    actual_vehicle_expenses: float = 0.0,
    year: int = 2025,
) -> dict:
    """
    Compare standard mileage vs. actual expense vehicle deduction.
    Source: IRS Publication 463

    Standard mileage rates:
      2025: $0.70/mile  |  2024: $0.67/mile  |  2023: $0.655/mile
    """
    rates = {2025: 0.70, 2024: 0.67, 2023: 0.655, 2022: 0.585}
    rate = rates.get(year, 0.70)

    standard = business_miles * rate
    business_pct = business_miles / total_miles if total_miles > 0 else 0
    actual = actual_vehicle_expenses * business_pct if actual_vehicle_expenses > 0 else 0

    return {
        'standard_mileage_deduction': standard,
        'actual_expense_deduction': actual,
        'business_use_pct': round(business_pct * 100, 1),
        'mileage_rate': rate,
        'recommended': 'actual' if actual > standard else 'standard',
        'recommended_amount': max(standard, actual),
    }


# --- Example: Full SE Tax Summary ---

if __name__ == '__main__':
    # Freelance developer: $120,000 revenue, $20,000 business expenses, single filer
    result = calculate_se_tax(120_000, 20_000, 'single')
    print(f"Net SE Income:       ${result.net_se_income:>10,.0f}")
    print(f"SE Tax Base:         ${result.se_tax_base:>10,.0f}")
    print(f"SE Tax:              ${result.se_tax:>10,.0f}")
    print(f"SE Tax Deduction:    ${result.se_tax_deduction:>10,.0f}")
    print(f"Income Tax Base:     ${result.net_after_se_deduction:>10,.0f}")
    print()

    qbi = calculate_qbi_deduction(
        net_qbi=result.net_after_se_deduction,
        taxable_income=result.net_after_se_deduction - 15_000,  # std deduction
        filing_status='single',
        is_sstb=False,
    )
    print(f"QBI Deduction:       ${qbi.final_deduction:>10,.0f}")
    print()

    est = calculate_estimated_tax(
        estimated_annual_income=120_000,
        estimated_deductions=20_000 + result.se_tax_deduction + 15_000,
        filing_status='single',
    )
    print(f"Quarterly Payment:   ${est.quarterly_payment:>10,.0f}")
    print(f"Q1 Due: Apr 15 | Q2: Jun 16 | Q3: Sep 15 | Q4: Jan 15")
```

---

## Safe Harbor Rules

To avoid the underpayment penalty (IRC §6654), at least one of the following must be satisfied:

| Rule | Requirement |
|------|------------|
| **90% Rule** | Pay 90% of current year tax liability via withholding + estimated payments |
| **100% Prior Year Rule** | Pay 100% of prior year tax (if prior year AGI ≤ $150,000) |
| **110% Prior Year Rule** | Pay 110% of prior year tax (if prior year AGI > $150,000) |
| **Small balance exception** | Underpayment < $1,000 after credits and withholding |

> **Source:** [IRS Form 2210 Instructions](https://www.irs.gov/instructions/i2210)

### Annualized Income Installment Method

If income is uneven (e.g., large Q4 contract), Form 2210 Schedule AI lets you calculate each quarter's required payment based on actual annualized YTD income rather than 25% of estimated annual tax. This can eliminate or reduce an underpayment penalty even when quarterly payments are uneven.

---

## Common 1099 Mistakes & Audit Flags

| Mistake | Risk | Correct Approach |
|---------|------|-----------------|
| Not reporting 1099-K income | High — IRS matches 1099s to returns | Report all income; 1099-K threshold is $2,500 in 2026 |
| Deducting 100% of meals | Medium | Meals are 50% deductible (business meals only) |
| Claiming home office without exclusive use | High | Space must be used *only* for business |
| No mileage log | High | Log date, destination, business purpose, miles |
| Deducting commuting miles | High | Commuting (home ↔ regular workplace) is never deductible |
| Paying subcontractors > $600 without filing 1099-NEC | Medium | File 1099-NEC by Jan 31; IRS Form W-9 before paying |
| Missing state SE tax or pass-through rules | Medium | Many states have additional SE or PTE taxes |
| Hobby loss rules (IRC §183) | High | If no profit motive, deductions limited to income |

> **Source:** [IRS Audit Techniques Guide — Small Business](https://www.irs.gov/businesses/small-businesses-self-employed/audit-techniques-guides-atgs) · [IRC §183 Hobby Loss Rules](https://www.irs.gov/pub/irs-utl/IRC-183-Activities-Not-Engaged-in-for-Profit.pdf)

### Hobby vs. Business

The IRS presumes a profit motive if the activity shows a profit in **3 of 5 consecutive years** (2 of 7 for horse activities). Factors considered:
- Manner of carrying on the activity (businesslike records, separate bank account)
- Time and effort invested
- History of income/losses
- Financial status of taxpayer
- Elements of personal pleasure or recreation

---

## See Also

- **[TaxLogic Self-Employed Tax Calculator](https://taxlogic.cc/tools/tax/self-employed)** — Estimate your SE tax, QBI deduction, and quarterly payments interactively. Enter your Schedule C revenue and expenses to see a full tax breakdown.
- **[Freelancer Invoice Aging Sample](https://github.com/SirMem/freelancer-invoice-aging-sample)** — Free MIT spreadsheet (Current / 1–30 / 31–60 / 60+) to track receivables before quarterly estimated payments; cash you haven't collected isn't Schedule C income yet.

---

## Official IRS Sources

| Resource | URL |
|----------|-----|
| Publication 334 — Tax Guide for Small Business | https://www.irs.gov/publications/p334 |
| Publication 535 — Business Expenses | https://www.irs.gov/publications/p535 |
| Publication 463 — Travel, Gift, and Car Expenses | https://www.irs.gov/publications/p463 |
| Publication 587 — Business Use of Your Home | https://www.irs.gov/publications/p587 |
| Publication 560 — Retirement Plans for Small Business | https://www.irs.gov/publications/p560 |
| Schedule C Instructions | https://www.irs.gov/instructions/i1040sc |
| Schedule SE Instructions | https://www.irs.gov/instructions/i1040sse |
| Form 1040-ES (Estimated Tax) | https://www.irs.gov/forms-pubs/about-form-1040-es |
| Form 8995 (QBI Deduction) | https://www.irs.gov/forms-pubs/about-form-8995 |
| Form 2210 (Underpayment Penalty) | https://www.irs.gov/instructions/i2210 |
| Self-Employed Individuals Tax Center | https://www.irs.gov/businesses/small-businesses-self-employed/self-employed-individuals-tax-center |

---

## Contributing

Contributions welcome — please open an issue or PR. All data must cite an official IRS source or authoritative reference. No affiliate links.

## License

CC0 1.0 Universal — public domain dedication.
