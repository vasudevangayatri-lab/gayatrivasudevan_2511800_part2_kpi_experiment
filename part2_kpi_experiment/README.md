# A/B Experiment Analysis — Onboarding & Activation Campaign
**Part 2 | Business Analytics Assignment**\
**Company:** Subscription-based digital product company\
**Experiment period:** January 1 – May 31, 2025\
**Dataset:** `data/campaign_experiment_data.xlsx` — 1,408 users (693 Control, 715 Treatment)  

---

## 1. Business Context

### Business Problem Statement (Task 1)

### 1. What Decision Needs to Be Made

A subscription-based digital product company launched a new onboarding and activation campaign to improve user conversion and early engagement. Users were divided into two groups.

Leadership needs a data-supported decision on whether to launch the campaign to all users.

Leadership must decide whether to **fully launch the new onboarding and activation campaign experience (Treatment) to all new users**, replacing the existing onboarding flow (Control).

- **Control group (n=690):** Existing onboarding experience
- **Treatment group (n=710):** New campaign experience

**Business question:** Does the new campaign meaningfully improve paid conversion rate without creating unacceptable side effects?

This is a binary, irreversible-in-the-short-term decision with direct revenue implications. The decision requires evaluating whether the Treatment's improvements on success metrics are statistically reliable, practically meaningful, and free of unacceptable harm to user experience or business operations.

Specifically, the decision must answer:

- Does the new campaign significantly improve paid conversion rate — the primary metric of interest?
- Does it improve upstream funnel health (landing page visits, trial starts, onboarding completion)?
- Do guardrail metrics (support ticket volume, refund requests) remain within acceptable bounds?
- Are the gains consistent across user segments (region, device, plan type, traffic source)?
- Is there evidence of novelty effects that might erode gains over time?

### 2. Who the Decision Impacts

| Stakeholder | Impact |
|---|---|
| **New users (all future signups)** | They will experience either the existing or the new onboarding — affecting their likelihood of activating and converting to a paid plan |
| **Revenue & Finance team** | Paid conversion rate directly determines monthly recurring revenue; a 120% relative lift in conversion, if sustained, materially changes growth projections |
| **Customer Support team** | Treatment users in the experiment generated 69.6% more support tickets per user; a full rollout could significantly increase support load |
| **Product & Engineering** | Responsible for maintaining the Treatment experience and addressing the friction points that are generating excess support contacts |
| **Marketing** | Campaign attribution and CAC models depend on the onboarding path users take |
| **Leadership / Board** | The rollout decision is a strategic go/no-go that affects growth targets and resource allocation |

### 3. What Metric Should Improve

The **primary success metric** is:

> **Paid conversion rate** — the proportion of new users who convert to a paid subscription within 30 days of signup.

This metric was chosen because it is the most direct expression of the campaign's business objective (improving user conversion) and is the metric that drives recurring revenue. The experiment is specifically designed to answer whether the new campaign experience moves this needle.

**Supporting (secondary) metrics** that must also show improvement or, at minimum, not deteriorate:

| Metric | Why It Matters |
|---|---|
| Onboarding completion rate | Upstream leading indicator of conversion; users who complete onboarding are far more likely to convert |
| Trial start rate | Mid-funnel health; signals whether the landing page is persuading users to engage |
| Landing page visit rate | Top-of-funnel; indicates whether the campaign drives users into the funnel at all |
| Engagement score (30d) | Early signal of long-term retention; higher engagement predicts lower churn post-conversion |
| Days to convert | Speed of conversion is a proxy for experience clarity; faster conversion reduces revenue delay and drop-off risk |
| Revenue per converted user (30d) | Quality of conversions matters, not just quantity |

### 4. What Risks Must Be Monitored

The following **guardrail metrics** represent risks that could make a conversion lift a net-negative outcome:

#### Primary Guardrails

| Guardrail | Threshold (suggested) | Status in Experiment | Concern Level |
|---|---|---|---|
| **Support ticket volume per user** | Should not increase by more than 15% vs. Control | **+69.6% in Treatment** (p < 0.0001) | 🔴 HIGH — statistically significant increase |
| **Refund request rate** | Should not increase vs. Control | 0.0% Control vs. 0.42% Treatment (p = 0.088) | 🟡 MEDIUM — directionally negative; not yet significant at α=0.05 |
| **Revenue per paying user** | Should not significantly decrease | $1,630 Control vs. $770 Treatment (small samples) | 🟡 MEDIUM — Treatment converters generating lower individual revenue; may reflect plan mix |

#### Secondary Risks

- **Sample ratio mismatch (SRM):** No SRM detected (p = 0.558); randomisation appears sound
- **Novelty effect:** The 5-month experiment window partially mitigates this, but engagement score gains should be monitored post-launch for decay
- **Segment heterogeneity:** If the Treatment works primarily for one segment (e.g., Free plan users, Mobile users), a full rollout may dilute the observed average effect
- **Support cost economics:** A 70% increase in support contacts per user could erode the revenue gain from higher conversion if support costs are material

#### Risk Framework

```
IF (conversion lift is real AND statistically significant)
  AND (support ticket increase is explainable and manageable)
  AND (refund rate remains below 1%)
  AND (revenue per user does not significantly drop)
THEN → Launch recommendation
ELSE → Conditional launch with guardrails / further investigation
```

### 5. What Evidence Is Required Before Making a Recommendation

A credible recommendation requires the following evidence to be evaluated in sequence:

#### Step 1 — Sample integrity
- Confirm no sample ratio mismatch (SRM) between Control and Treatment
- Verify temporal distribution of signups is balanced across months
- Confirm balance on key covariates: region, device, plan type, traffic source

#### Step 2 — Primary metric statistical significance
- Paid conversion rate difference must be statistically significant at α = 0.05
- The observed effect size must be large enough to be practically meaningful (not just statistically significant with a large sample)
- Confidence intervals for the conversion lift must be calculated and reported

#### Step 3 — Funnel analysis
- Each stage of the conversion funnel (landing page → trial → onboarding → paid) must be analysed
- Leakage points where Treatment underperforms must be identified even if the final conversion rate improves

#### Step 4 — Guardrail metric evaluation
- Support ticket rates must be tested for statistical significance and, if significant, investigated for root cause
- Refund rates must be compared with appropriate statistical tests
- Revenue per paying user must be compared, acknowledging small sample sizes in the converter sub-group

#### Step 5 — Segment analysis (heterogeneity of treatment effects)
- Conversion rate gains must be checked across region, device type, plan type, and traffic source
- If gains are concentrated in a sub-segment, that must inform the rollout recommendation

#### Step 6 — Effect size and practical significance
- Cohen's h or similar effect size metrics must confirm the conversion lift is not merely a statistical artefact of sample size
- Power analysis must confirm the experiment was adequately powered to detect the observed effect

#### Step 7 — Synthesis and decision
- All evidence is synthesised into a Go / No-Go / Conditional recommendation
- The recommendation must quantify the expected revenue impact, the expected support cost increase, and the net expected value

---

## 2. Dataset Description

| Property | Detail |
|---|---|
| **Source file** | `campaign_experiment_data.xlsx` |
| **Raw records** | 1,408 rows × 16 columns |
| **After cleaning** | 1,400 rows (8 duplicate user_ids removed) |
| **Experiment period** | January–May 2025 |
| **Groups** | Control (690), Treatment (710) |

---

### Quick Data Reference (columns)

| Field | Description |
|---|---|
| `user_id` | Unique user identifier |
| `signup_date` | Date user signed up (Jan–May 2025) |
| `experiment_group` | `Control` or `Treatment` |
| `region` | East, North, South, West |
| `device_type` | Desktop, Mobile, Tablet |
| `traffic_source` | Email, Organic, Paid Search, Referral, Social |
| `plan_type` | Free, Basic, Premium |
| `visited_landing_page` | 1 if user visited the campaign landing page |
| `started_trial` | 1 if user started a free trial |
| `completed_onboarding` | 1 if user completed the onboarding flow |
| `converted_to_paid` | 1 if user converted to a paid plan (PRIMARY METRIC) |
| `revenue_30d` | Revenue generated in first 30 days (0 if not converted) |
| `support_tickets_30d` | Number of support tickets raised in first 30 days (GUARDRAIL) |
| `refund_requested` | 1 if user requested a refund (GUARDRAIL) |
| `days_to_convert` | Days from signup to paid conversion (null if not converted) |
| `engagement_score` | Proprietary engagement score (0–100) in first 30 days |


### Data Quality Issues Found and Actions Taken

| Issue | Count | Action |
|---|---|---|
| Duplicate user_ids | 8 | Removed; kept first occurrence |
| Missing `device_type` | 18 | Filled with 'Unknown' |
| Missing `traffic_source` | 24 | Filled with 'Unknown' |
| Missing `engagement_score` | 14 | Excluded from mean (not imputed) |
| Missing `days_to_convert` | 1,336 | Expected — only converters (72) have values |
| Revenue outliers (>₹1,000) | 24 | Retained — all are valid converted users |
| Binary columns | 0 invalid | All confirmed as {0,1} |
| Segment balance | Minor email skew | Monitored in segment analysis |

Full DQ documentation in: `analysis/experiment_analysis.xlsx` → Sheet: "Data Quality Checks"

---

## 3. North Star Metric Selected

**Paid Conversion Rate** — proportion of users who converted to a paid subscription within 30 days.

**Why this metric and how this connects to business growth:**\
- Direct revenue linkage — every conversion = immediate subscription revenue
- Binary, unambiguous, and fully within the experiment's causal chain
- Directly answers the business question: "Does the campaign convert more users?"
- Statistically tractable for a two-sample proportion test at n=1,400

**Why other metrics are supporting one (not a North Star):**\
North Star metrics is the most direct expression of the campaign's business objective (improving user conversion) and is the metric that drives recurring revenue.\
**Other Supporting (secondary) metrics** are designed to act as boundary condition rather than measures of fundamental business growth; They protect the user experience, prevent localized optimisation, binary or threshold based. However must show improvement or, at minimum, not deteriorate. For Example:

- *Engagement score*: A supporting metric — high engagement doesn't guarantee conversion.
- *ARPU*: Revenue per user includes ₹0 for non-converters, creating extreme right skew that makes testing difficult without outlier removal.
- *Onboarding completion*: A funnel step, not an outcome.

**What could go wrong if optimised blindly:**\
If only conversion rate is tracked without revenue quality, the campaign could attract low-intent users who convert to low-tier plans and churn quickly, reducing LTV even as conversion rate rises. This risk materialised in this experiment (Revenue per Converted User declined 52.8%).

---

## 4. KPI Tree Summary

The KPI tree (see `outputs/kpi_tree.png`) organises metrics into three primary driver pillars under the North Star:

**Pillar 1 — Activation Funnel Depth:** Landing Page Visit Rate, Trial Start Rate, Onboarding Completion Rate. All three improved significantly (Treatment: +13.8%, +15.7%, +35.0%).

**Pillar 2 — Revenue Quality:** ARPU (+4.4%), Revenue per Converted User (−52.8% ⚠), Engagement Score (+10.4%). Mixed signals — conversion is happening, but revenue per converter is lower.

**Pillar 3 — User Experience:** Days to Convert (−27.8% ✓ faster), Support Ticket Rate (+69.4% ⚠ risk), Refund Rate (+0.42%, not significant).

**Guardrail metrics:** Support ticket rate (⚠ AT RISK), Revenue per converted user (⚠ MONITOR), Refund rate (✓), Days to convert (✓), Segment-level decline (✓ none).

---

## 5. Experiment Analysis Approach

### Data Preparation (Task 4)
- Removed 8 duplicate user_ids (kept first occurrence)
- Filled missing device_type and traffic_source with 'Unknown'
- Excluded missing engagement scores from mean calculations
- Retained revenue outliers as valid high-value converted users
- Verified all binary columns contain only {0,1}
- Confirmed acceptable segment balance across Control and Treatment

### Metric Calculation (Task 5)
All 11 required metrics computed from the cleaned dataset with Control vs Treatment comparison, absolute difference, relative lift, and statistical test results. Three segment breakdowns produced: by Region, by Device Type, and by Plan Type. All documented in `outputs/experiment_summary.xlsx`.

---

## 6. Hypothesis Test Summary

**Test:** One-Tailed Z-Test for Proportions
**Metric tested:** Paid Conversion Rate
**H₀:** p_treatment ≤ p_control
**H₁:** p_treatment > p_control
**α:** 0.05

| Statistic | Value |
|---|---|
| Control rate | 3.19% (22/690) |
| Treatment rate | 7.04% (50/710) |
| Z-statistic | 3.2640 |
| P-value | 0.000549 |
| Z-critical | 1.645 |
| **Decision** | **REJECT H₀** |
| Relative lift | +120.9% |
| CI — Control | [2.11%, 4.78%] |
| CI — Treatment | [5.38%, 9.16%] |

**Interpretation:** The campaign produced a statistically significant 120.9% improvement in paid conversion rate (p < 0.001). The confidence intervals do not overlap, confirming the effect is real and robust. Full notes in `analysis/hypothesis_test_notes.md`.

---

## 7. Guardrail Metrics Considered

| Guardrail | Control | Treatment | Sig | Status |
|---|---|---|---|---|
| Support Ticket Rate | 0.220 | 0.373 | p<0.001 | ⚠ AT RISK |
| Rev / Converted User | ₹1,630 | ₹770 | — | ⚠ MONITOR |
| Refund Rate | 0.00% | 0.42% | p=0.25 (ns) | ✓ Safe |
| Days to Convert | 8.86d | 6.40d | p=0.004 | ✓ Improved |
| Segment-level decline | — | — | — | ✓ None |

Guardrails measure system health. Optimising them does not necessarily drive growth; it just ensures product remain usable while we pursue NSM.  It provides defensive checks to keep the product usable. 

**Risk that must be monitored:**

Two guardrail metrics require close attention before any launch recommendation is made:

**Support ticket volume (HIGH RISK)**  
Treatment users in the experiment raised support tickets at a rate 70% higher than Control users. This is statistically significant (p < 0.0001). If sustained at full rollout scale, this could represent a material increase in support costs and may signal that the new experience introduces friction or confusion that the old experience did not. This must be investigated and explained before launch.

**Refund request rate (MEDIUM RISK)**  
No Control users requested a refund; 0.42% of Treatment users did. This is not yet statistically significant (p = 0.088), but the direction is concerning. A larger rollout could amplify this signal. This must be monitored closely.

**Revenue per converting user (MEDIUM RISK)**  
Treatment converters generated lower average revenue per user than Control converters ($770 vs. $1,630). Sample sizes here are small (22 and 50 users respectively), so this difference is driven in part by a small number of high-value outliers in the Control group. This needs to be weighted appropriately in the final recommendation.

**Other:**
- *Engagement score*: A supporting metric — high engagement doesn't guarantee conversion.
- *ARPU*: Revenue per user includes ₹0 for non-converters, creating extreme right skew that makes testing difficult without outlier removal.
- *Onboarding completion*: A funnel step, not an outcome.

This must be investigated and resolved before full launch to prevent support cost overrun; These risks do not negate the conversion gain, but they require a structured response before full launch.

---

## 8. Final Recommendation

**CONDITIONAL LAUNCH — Phase 1 to Free Plan + Premium users**

| Segment | Recommendation | Rationale |
|---|---|---|
| Free plan users | ✓ Launch (Phase 1) | +204% conversion lift; largest gain |
| Premium plan users | ✓ Launch (Phase 1) | +127% lift; high-value cohort |
| Basic plan users | ✗ Hold | Only +7% lift; redesign needed |

**Pre-conditions:**
1. Root cause analysis of support ticket surge (2-week deadline)
2. Support team capacity increased by ≥50% before Phase 1 launch
3. 30-day LTV monitoring dashboard active at launch
4. 90-day go/no-go review for full launch

**Do NOT full-launch without:** Addressing the support ticket risk and confirming that 90-day LTV for Treatment cohort meets or exceeds Control.

---

## 9. Assumptions and Limitations

### Assumptions
1. Deduplication by user_id is correct — the first occurrence of a duplicate user_id is the valid record
2. Users were randomly assigned to groups (verified via segment balance check)
3. Revenue outliers (>₹1,000) are valid high-value conversions, not data errors
4. Days-to-convert is blank for non-converters (correct); not an error
5. The 30-day window captures all relevant conversions for this experiment
6. Support ticket count is fully attributable to experiment exposure (not external factors)

### Limitations
1. Only 72 total converters — conversion rate is well-estimated, but revenue averages carry high uncertainty
2. 30-day outcomes only — no 90-day LTV or churn data available
3. Seasonal effects not controlled — experiment ran Jan–May 2025 only
4. Support ticket driver unknown — cannot confirm which specific campaign element causes the increase
5. Basic segment is nearly unaffected — the campaign may need a fundamentally different approach for this cohort
6. Small tablet segment (n=112) — the 292% lift, while notable, should be validated before acting on it

---

## 10. Screenshots Included

| File | Contents |
|---|---|
| `screenshots/summary_metrics.png` | Full Control vs Treatment metrics table with all 10 metrics, absolute diff, relative lift, significance, and risk level |
| `screenshots/hypothesis_test_output.png` | Z-test inputs and outputs, decision, and distribution visualisation with Z-statistic and rejection region |
| `screenshots/kpi_tree_preview.png` | Full KPI tree — North Star metric, 3 primary drivers, sub-drivers, Level 3 drivers, and 5 guardrail metrics |

---

## Output File Reference

| File | Task | Description |
|---|---|---|
| `campaign_experiment_data.xlsx` | Input | Raw experiment dataset |
| `analysis/experiment_analysis.xlsx` | T4 | Cleaned dataset + DQ checks |
| `analysis/hypothesis_test_notes.md` | T6/T7 | Hypothesis framing + test results |
| `outputs/kpi_tree.png` | T3 | KPI tree diagram |
| `outputs/experiment_summary.xlsx` | T5 | Control vs Treatment summary + 3 segment analyses |
| `outputs/recommendation_memo.md` | T9 | Full decision memo |
| `screenshots/summary_metrics.png` | T9 | Metrics table screenshot |
| `screenshots/hypothesis_test_output.png` | T7/T9 | Test output screenshot |
| `screenshots/kpi_tree_preview.png` | T3/T9 | KPI tree screenshot |
| `README.md` | T9 | This file |
