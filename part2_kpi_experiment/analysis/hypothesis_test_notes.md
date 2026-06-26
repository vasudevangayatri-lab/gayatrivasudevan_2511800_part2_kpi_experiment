# Hypothesis Test Notes
**Project:** A/B Experiment — Onboarding & Activation Campaign\
**Date:** June 2026

---

## Task 6: Hypothesis Framing

### 1. Null Hypothesis (H₀)
> The new onboarding campaign (Treatment) produces **no improvement** in paid conversion rate compared to the existing experience (Control).
>
> **H₀: p_treatment ≤ p_control**
>
> Where `p` is the proportion of users in each group who converted to a paid subscription within 30 days of sign-up.

### 2. Alternate Hypothesis (H₁)
> The new onboarding campaign produces a **statistically significant improvement** in paid conversion rate compared to the existing experience.
>
> **H₁: p_treatment > p_control**

### 3. Test Direction: One-Tailed
The test is **one-tailed (right-tailed)** because the business question is directional:
> "Is Treatment *better* than Control?"

Leadership is not interested in detecting whether the campaign is *worse* — if it is worse, the launch decision is simply "No." Testing only in the direction of improvement preserves statistical power for detecting the effect of interest.

### 4. Significance Level
**α = 0.05** (5%)

This is the industry-standard threshold for product experiments. It means we accept a 5% chance of incorrectly rejecting H₀ when it is actually true (Type I error). Given the moderate business cost of a false positive (launching a campaign that doesn't help) vs. the cost of a false negative (missing a genuinely effective campaign), α = 0.05 is appropriate.

### 5. Metric Being Tested
**Paid Conversion Rate** — the proportion of users who converted from a free or trial account to a paid subscription within 30 days of sign-up.

Formula:
```
Paid Conversion Rate = Users Converted to Paid / Total Users in Group
```

### 6. Reason for Choosing This Metric
Paid Conversion Rate is selected as the **North Star Metric** for this experiment for the following reasons:

- **Direct revenue linkage**: It is the most immediate predictor of 30-day revenue. Every incremental conversion translates directly into subscription revenue.
- **Clear business decision**: The hypothesis is specifically about whether the campaign converts more users. Conversion rate is the most direct, unambiguous measurement of that.
- **Actionable and measurable**: Unlike engagement score or onboarding completion (which are process metrics), conversion rate is an outcome metric. It answers "did the campaign work?" rather than "did users try things?"
- **Manageable sensitivity**: With ~700 users per group, conversion rate (a binary outcome) is statistically tractable. A two-sample proportion test is the right tool.

**Why not other metrics?**
- *Engagement score*: A supporting metric — high engagement doesn't guarantee conversion.
- *ARPU*: Revenue per user includes ₹0 for non-converters, creating extreme right skew that makes testing difficult without outlier removal.
- *Onboarding completion*: A funnel step, not an outcome.

### 7. Interpretation Logic
The business interpretation of the test outcome operates as follows:

| Test Result | Statistical Decision | Business Decision |
|---|---|---|
| p < α (0.05) | Reject H₀ | Treatment improves conversion — proceed to launch evaluation (subject to guardrails) |
| p ≥ α (0.05) | Fail to reject H₀ | No evidence of improvement — do not launch; consider redesign |
| Significant but guardrails breach | Reject H₀ | Improvement is real but has side effects — conditional launch or continue testing |

The test result is **necessary but not sufficient** for a launch recommendation. Even if H₀ is rejected, guardrail metrics (support tickets, refund rate, revenue per converted user) must be evaluated before a final recommendation is made.

---

## Task 7: Hypothesis Test Results

### Test Method: Two-Sample Z-Test for Proportions (One-Tailed)

**Test statistic formula:**
```
Z = (p̂_treatment - p̂_control) / √[ p̂_pooled × (1 - p̂_pooled) × (1/n_treatment + 1/n_control) ]
```

### Test Inputs

| Input | Value |
|---|---|
| Test type | One-tailed Z-test for proportions |
| Metric | Paid Conversion Rate |
| α (significance level) | 0.05 |
| Control group size (n) | 690 |
| Control conversions | 22 |
| Control conversion rate | 3.19% |
| Treatment group size (n) | 710 |
| Treatment conversions | 50 |
| Treatment conversion rate | 7.04% |

### Test Outputs

| Output | Value |
|---|---|
| Pooled proportion (p̂) | 0.0514 |
| **Z-statistic** | **3.2640** |
| **P-value (one-tailed)** | **0.000549** |
| Z-critical (α=0.05, one-tail) | 1.645 |
| 95% CI — Control | [2.11%, 4.78%] |
| 95% CI — Treatment | [5.38%, 9.16%] |
| Absolute lift | +3.85 percentage points |
| Relative lift | **+120.9%** |

### Decision Rule
```
If p-value < α (0.05)  →  REJECT H₀
If p-value ≥ α (0.05)  →  FAIL TO REJECT H₀
```

### Outcome
**p = 0.000549 < α = 0.05  →  REJECT H₀**

The Z-statistic of 3.26 exceeds the critical value of 1.645. The probability of observing a conversion lift this large by chance alone (if H₀ were true) is 0.055% — far below the 5% threshold.

The 95% confidence intervals for the two groups do not overlap:
- Control: [2.11%, 4.78%]
- Treatment: [5.38%, 9.16%]

This non-overlap provides additional confirmation that the effect is real.

### Business Interpretation

The new onboarding and activation campaign produced a **statistically significant 120.9% improvement in paid conversion rate** (3.19% → 7.04%, p < 0.001). This result is highly significant and robust.

**In practical terms:**
- The Treatment group converted at more than double the rate of Control
- This would translate to approximately **28 additional conversions per 1,000 users**
- At an average treatment revenue of ₹770 per converted user, this implies approximately **₹21,560 in incremental revenue per 1,000 users deployed**

**Caveats:**
1. Statistical significance does not automatically mean the campaign should be launched. Two guardrail metrics (support ticket rate and revenue per converted user) showed adverse signals that require evaluation before a final recommendation.
2. The experiment ran January–May 2025. Seasonal effects may influence generalisability to other periods.
3. Sample size was relatively small (n=1,400 total; 72 total conversions). While the result is significant, a larger sample would provide more stable effect size estimates.

---

*Evidence of test output saved as: `screenshots/hypothesis_test_output.png`*
*Test calculations in: `outputs/experiment_summary.xlsx` → Sheet: "Overall Summary"*
