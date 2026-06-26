# Recommendation Memo
**To:** Product Leadership & Growth Team\
**Subject:** A/B Experiment — Onboarding & Activation Campaign Launch Decision\
**Date:** June 2026

---

## 1. Executive Summary

The new onboarding and activation campaign was tested against the existing experience across 1,400 users (690 Control, 710 Treatment) from January to May 2025. The campaign delivered a **statistically significant 120.9% improvement in paid conversion rate** (3.19% → 7.04%, p < 0.001, Z = 3.26).

However, two guardrail metrics showed adverse signals: support ticket rate increased by 69.4% (p < 0.001) and average revenue per converted user fell 52.8% (₹1,630 → ₹770). These risks do not negate the conversion gain, but they require a structured response before full launch.

#### Key Findings
* **Primary Success:** Paid conversion rate increased by **+120%** (from 3.2% to 7.0%, p=0.002), showing strong conversion lift.
* **Funnel Growth:** Significant positive lifts in landing page visits (+14.1%, p=0.0004) and onboarding completion (+36.4%, p=0.008).
* **Critical Guardrail Risk:** Support ticket volume per user rose by **+70%** (p<0.001), signaling potential friction/confusion.
* **Revenue Ambiguity:** Total ARPU lift was flat (+4.1%, p=0.916); Treatment converters had lower average spend due to Control outliers.

#### Recommendation 
**Conditional Launch** — Phase 1 to Free Plan + Premium users, with immediate support capacity investment and revenue quality monitoring.

---

## 2. North Star Metric

**Selected North Star Metric:** Paid Conversion Rate

**Definition:** Proportion of users in each group who converted to a paid subscription within 30 days of sign-up.

**Why this metric?**
Paid Conversion Rate is the most direct measure of whether the onboarding campaign achieves its stated objective — turning free/trial users into paying customers. It:
- Directly drives 30-day revenue
- Is binary and unambiguous (either the user pays or does not)
- Has clear organisational alignment (it is what leadership wants to improve)
- Is statistically tractable with the experiment sample size

**Why not other metrics?**
- *ARPU* is important but driven by both conversion and post-conversion revenue, making it a lagging composite metric that is hard to act on
- *Engagement score* and *onboarding completion rate* are leading indicators but not outcomes — they matter only insofar as they predict conversion
- *Days to convert* is a valuable supporting metric but secondary to whether conversion happens at all

**Risk of blind optimisation:** If conversion rate is optimised without monitoring revenue quality, the campaign could attract low-intent users who convert to low-tier plans and churn quickly, eroding LTV. This is precisely the risk flagged in guardrail analysis (Section 6).

---

## 3. KPI Tree Explanation

The KPI tree (see `outputs/kpi_tree.png`) structures the North Star Metric into three primary driver pillars:

**Pillar 1 — Activation Funnel Depth**
Conversion begins with users entering and completing the activation funnel. Sub-drivers include Landing Page Visit Rate (+13.8%), Trial Start Rate (+15.7%), and Onboarding Completion Rate (+35.0%). Treatment improved all three, confirming the campaign successfully deepened user engagement at each funnel step.

**Pillar 2 — Revenue Quality**
Converting users is only valuable if those users generate sustainable revenue. Sub-drivers include ARPU (+4.4%), Revenue per Converted User (−52.8% ⚠), and Engagement Score (+10.4%). Treatment's engagement gains are encouraging, but the revenue-per-converted-user decline is a warning: the campaign may be converting lower-value user cohorts.

**Pillar 3 — User Experience**
The quality of the experience determines whether conversion is durable. Sub-drivers include Days to Convert (−27.8% ✓ — faster is better), Support Ticket Rate (+69.4% ⚠), and Refund Rate (+0.42%, not significant). The faster conversion speed is positive; the support ticket surge is the experiment's most significant operational risk.

**Guardrail Metrics:**
Five guardrails were defined. Two are at risk (support ticket rate, revenue per converted user). Three are safe (refund rate, days to convert, segment-level decline).

---

## 4. Experiment Result Summary

| Metric | Control | Treatment | Lift | Status |
|---|---|---|---|---|
| Users | 690 | 710 | — | Reference |
| Landing Page Visit | 63.6% | 72.4% | +13.8% | ✓ Positive |
| Trial Start | 25.1% | 29.0% | +15.7% | ✓ Positive |
| Onboarding Completion | 15.7% | 21.1% | +35.0% | ✓ Positive |
| **Paid Conversion Rate** | **3.19%** | **7.04%** | **+120.9%** | **✓ SIGNIFICANT** |
| ARPU | ₹51.97 | ₹54.25 | +4.4% | ✓ Positive |
| Rev / Converted User | ₹1,630 | ₹770 | −52.8% | ⚠ Risk |
| Refund Rate | 0.00% | 0.42% | — | ✓ (ns) |
| Support Ticket Rate | 0.220 | 0.373 | +69.4% | ⚠ Risk |
| Engagement Score | 57.03 | 62.94 | +10.4% | ✓ Significant |
| Days to Convert | 8.86d | 6.40d | −27.8% | ✓ Significant |

The funnel metrics (rows 2–4) confirm the campaign is working as designed: more users are entering and completing the activation journey. The outcome metric (row 5) confirms that this translates to paid conversions. Rows 6–11 reveal the texture of the conversion: faster, more engaged, but with a support burden and a revenue quality question.

---

## 5. Hypothesis Test Interpretation

**Test:** One-Tailed Z-Test for Proportions (H₁: p_treatment > p_control)
**α = 0.05**

| Statistic | Value |
|---|---|
| Z-statistic | 3.2640 |
| P-value | 0.000549 |
| Decision | REJECT H₀ |
| CI — Control | [2.11%, 4.78%] |
| CI — Treatment | [5.38%, 9.16%] |

**Interpretation:** The probability of observing a conversion lift of 120.9% by random chance alone is 0.055% — far below the 5% threshold. The confidence intervals for the two groups do not overlap, providing additional confirmation.

The test result is statistically significant and robust. The effect is not marginal — even at the lower bound of the Treatment CI (5.38%), Treatment still outperforms Control's upper bound (4.78%).

**Business translation:** For every 1,000 users exposed to the campaign, approximately 28 additional paid conversions are expected compared to the Control experience.

---

## 6. Guardrail Analysis

### Guardrail 1: Support Ticket Rate — ⚠ AT RISK

| Metric | Control | Treatment | Change | P-value |
|---|---|---|---|---|
| Avg support tickets/user | 0.220 | 0.373 | +69.4% | < 0.001 |

This is the most significant guardrail concern. Treatment users filed significantly more support tickets. This is statistically significant (t = −4.20, p < 0.001) and indicates that the new campaign creates confusion or friction *after* conversion that the current support team may not be scaled to handle.

**Risk:** Support costs could erode the revenue gains from higher conversion. At ₹X per support ticket, this increase may partially offset the ₹21,560 incremental revenue per 1,000 users estimated from the conversion lift.

**Action required:** Investigate which campaign elements are driving tickets (likely specific onboarding steps or product feature discovery). Increase support capacity before full launch.

### Guardrail 2: Revenue per Converted User — ⚠ MONITOR

| Metric | Control | Treatment | Change |
|---|---|---|---|
| Avg rev / converted user | ₹1,630 | ₹770 | −52.8% |

Treatment converters generate significantly less revenue per user than Control converters. However, this must be interpreted carefully:

- Control had 22 converters; Treatment had 50 converters
- Control's average is heavily influenced by 10 high-revenue outliers (max ₹8,610)
- Treatment has fewer outliers (max ₹2,660) but more converters
- On **total** revenue basis: Control converted users generated ₹35,862 vs Treatment ₹38,521 — Treatment is actually higher in aggregate

**Segment breakdown reveals:** The Basic plan segment shows minimal conversion lift (+7%) while generating lower revenue; Free plan shows explosive lift (+204%) with moderate revenue. The campaign is disproportionately converting Free plan users, who may be choosing lower-tier paid plans.

**Action required:** Monitor plan upgrade rates post-conversion and 90-day LTV. Consider adding higher-tier plan incentives to the campaign for Basic users.

### Guardrail 3: Refund Rate — ✓ SAFE

0 Control refunds vs 3 Treatment refunds (0.42%). Fisher exact test p = 0.25 — not statistically significant. 3 refunds in a 710-person group is within normal bounds. Monitor post-launch at scale.

### Guardrail 4: Days to Convert — ✓ IMPROVED

Treatment users convert in 6.4 days vs 8.9 days for Control (p = 0.004). Faster conversion is a positive signal — users are reaching the value proposition more quickly. This also reduces the risk of churn during the trial period.

### Guardrail 5: Segment-Level Decline — ✓ SAFE

All four regions and all device types show positive conversion lifts for Treatment. No segment was harmed by the campaign. (Details in Section 7.)

---

## 7. Segment-Level Insight

### By Region

| Region | Control Conv% | Treatment Conv% | Rel Lift |
|---|---|---|---|
| North | 3.48% | 8.89% | +155% ← strongest |
| South | 3.26% | 7.65% | +135% |
| East | 2.55% | 6.47% | +154% |
| West | 3.38% | 5.08% | +50% ← weakest |

The campaign is effective across all regions. West shows the weakest lift (+50%) — still positive and meaningful, but the campaign may be less relevant to Western-region user journeys. This warrants investigation.

### By Device Type

| Device | Control Conv% | Treatment Conv% | Rel Lift |
|---|---|---|---|
| Mobile | 2.58% | 7.41% | +187% |
| Desktop | 4.50% | 6.57% | +46% |
| Tablet | 1.82% | 7.14% | +292% ← notable |

Mobile (61.7% of users) drives the majority of absolute conversions and shows strong lift. Tablet shows exceptional lift (+292%) but is a small segment (8%). Desktop shows the lowest relative lift — the campaign may be less optimised for desktop UX.

**Recommendation:** Prioritise mobile optimisation for launch; consider a desktop-specific variant for the next iteration.

### By Plan Type

| Plan | Control Conv% | Treatment Conv% | Rel Lift |
|---|---|---|---|
| Free | 3.06% | 9.29% | +204% ← explosive |
| Premium | 2.75% | 6.25% | +127% |
| Basic | 3.62% | 3.88% | +7% ← nearly flat |

The Basic plan segment shows almost no response to the campaign. This is a notable finding — Basic users may already have high intent (and thus a high baseline conversion rate), or the campaign messaging does not resonate with their use case. The Free plan explosion is promising but is the driver of the revenue-per-converted-user concern (Free users converting to lower-tier paid plans).

---

## 8. Final Recommendation

**RECOMMENDATION: CONDITIONAL LAUNCH — Phase 1 targeted rollout with guardrail controls**

**Launch to:** Free plan users (highest lift, +204%) and Premium users (+127%) immediately.

**Hold for Basic users:** The +7% lift is too small to justify rollout. Redesign the Basic-specific campaign messaging before including this segment.

**Conditions before full launch:**
1. **Support ticket root cause analysis** within 2 weeks — identify the top 3 drivers of support tickets from Treatment users and resolve in-product or via documentation
2. **Support team capacity increase** of at least 50% before expanding beyond Phase 1
3. **90-day LTV monitoring** — track whether Treatment converters upgrade their plans or churn at higher rates than Control converters over the next 90 days
4. **Revenue quality checkpoint at 30 days** — if Treatment cohort LTV is tracking below Control, pause expansion

**Expected outcomes at Phase 1 scale (Free + Premium, ~70% of user base):**
- Estimated additional monthly conversions: ~20 per 1,000 users
- Estimated incremental monthly revenue: ~₹15,400 per 1,000 users
- Estimated support cost increase: requires quantification (action item)

---

## 9. Risks and Limitations

### Risks
1. **Support ticket surge at scale**: If the 69.4% increase in support tickets is not addressed, it will become unsustainable at full deployment. This is the single biggest risk.
2. **Revenue quality**: Treatment converters generated less revenue per user in this experiment. If this pattern holds at scale, the LTV benefit of the campaign may be lower than the conversion rate alone suggests.
3. **Basic segment exclusion**: Excluding ~33% of users from the campaign creates an operational complexity. Ensure the two-experience system can be maintained without degrading either cohort.
4. **Seasonality**: The experiment ran January–May 2025. Conversion patterns may differ during other periods (e.g., lower intent during summer holidays).

### Limitations
1. **Small converter base (n=72)**: While the conversion rate difference is highly significant, the absolute number of converters is small. Revenue and LTV estimates carry wide uncertainty bands.
2. **30-day window only**: The experiment captures 30-day outcomes. Longer-term behaviour (churn, plan upgrades, LTV) is unknown and critical for evaluating true campaign value.
3. **No holdout for support tickets**: It is not possible to confirm from this experiment alone whether treatment users file more tickets because of the campaign specifically or because converted users are inherently more engaged with the product.
4. **Outliers in revenue**: Control's revenue average is heavily influenced by a small number of high-value conversions. Removing outliers would likely show Treatment ARPU is comparable to Control — but the data has not been adjusted.
5. **Single experiment period**: Results should be replicated in at least one additional experiment period before treating the effect size as definitive.

---

## 10. Next Steps

| Priority | Action | Owner | Timeline |
|---|---|---|---|
| 1 | Root cause analysis of support ticket increase | Product + CX | 2 weeks |
| 2 | Scale support team capacity by 50% | Operations | Before Phase 1 launch |
| 3 | Launch to Free + Premium segments (Phase 1) | Engineering | Week 3 |
| 4 | 30-day monitoring dashboard: conversion, tickets, LTV | Analytics | Week 3 |
| 5 | Design Basic-segment campaign variant | Marketing | 4 weeks |
| 6 | 90-day LTV cohort analysis | Analytics | Week 13 |
| 7 | Go/No-Go decision for full launch | Leadership | Week 13 |
| 8 | Desktop UX variant A/B test | Product | Next experiment cycle |

---

*Experiment data: `analysis/experiment_analysis.xlsx` | Statistical evidence: `screenshots/hypothesis_test_output.png` | Full summary: `outputs/experiment_summary.xlsx`*
