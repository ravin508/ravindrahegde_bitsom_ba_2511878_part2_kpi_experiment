# Hypothesis Testing Notes: Onboarding Campaign Experiment

**Date:** June 25, 2026  
**Experiment:** New Onboarding & Activation Campaign (Treatment) vs Existing Experience (Control)  
**Primary Metric Tested:** 30-Day Paid Conversion Rate (`converted_to_paid`)

---

## Task 6: Hypothesis Framing

### Null Hypothesis (H₀)
There is **no difference** in the 30-day paid conversion rate between users exposed to the new onboarding campaign (Treatment) and users exposed to the existing experience (Control).

**Formal statement:**  
H₀: p_Treatment = p_Control  
(where p = true proportion of users who convert to paid within 30 days)

### Alternate Hypothesis (H₁)
The new onboarding campaign (Treatment) **increases** the 30-day paid conversion rate compared to the existing experience (Control).

**Formal statement:**  
H₁: p_Treatment > p_Control

### Test Direction
**One-tailed test** (right-tailed)

**Rationale for one-tailed:**  
The business objective of the campaign is explicitly to *improve* user conversion. We are only interested in detecting whether the Treatment is better than Control (not whether it is worse). A two-tailed test would dilute statistical power for the direction we care about. If the Treatment performed significantly worse, we would still detect it through guardrail monitoring and directional review, but the formal hypothesis test is powered for improvement.

### Significance Level (α)
**α = 0.05** (5%)

This is the standard threshold used in business A/B testing at this company. It balances the risk of false positives (Type I error) against the need to detect real improvements in conversion.

### Metric Being Tested
**30-Day Paid Conversion Rate** (`converted_to_paid`)

**Why this metric was chosen as the primary metric for hypothesis testing:**
- It is the **North Star metric** for this experiment.
- It directly measures whether the new onboarding and activation campaign achieves its core objective: turning more signups into paying customers.
- It is the furthest downstream metric in the activation funnel and has the strongest connection to business revenue impact.
- Earlier funnel metrics (landing page visits, trial starts, onboarding completion) are important leading indicators, but the ultimate success of the campaign is defined by paid conversion.
- The experiment showed a large observed lift (+121% relative), making it the most impactful metric to formally test.

### Interpretation Logic
- **If we reject H₀** (p-value < 0.05): We have statistically significant evidence that the Treatment improves paid conversion rate. This supports a decision to launch (at least selectively) the new campaign.
- **If we fail to reject H₀** (p-value ≥ 0.05): We do not have sufficient evidence to conclude that the Treatment improves conversion. In this case, we would recommend against broad launch or require a larger sample / longer test before making a change.
- The test result must be interpreted **together with guardrail metrics** (support tickets, refunds, revenue per converter). A statistically significant improvement in conversion does not automatically mean we should launch if it comes with unacceptable increases in cost or quality issues.

---

## Task 7: Hypothesis Test / A/B Test Analysis

### Test Performed
**Two-Proportion Z-Test** (for difference in proportions)

This is the appropriate test for comparing conversion rates (binary outcomes) between two independent groups with large sample sizes.

### Summary of Test Inputs

| Input | Control | Treatment | Notes |
|-------|---------|-----------|-------|
| **Sample Size (n)** | 690 | 710 | After removing duplicate user_ids |
| **Conversions (x)** | 22 | 50 | Users who converted to paid within 30 days |
| **Conversion Rate (p̂)** | 3.19% | 7.04% | Observed sample proportion |
| **Pooled Proportion (p̂)** | 5.14% | - | (22 + 50) / (690 + 710) |

### Test Output & Results

**Test Statistic (z):** **3.25**

**P-value:** **0.0011**

**95% Confidence Interval for Difference (Treatment - Control):**  
**+1.55pp to +6.15pp** (Wilson score interval method)

**Effect Size:**
- Absolute lift: **+3.85 percentage points**
- Relative lift: **+120.9%**

### Decision Rule
- **Reject H₀** if p-value < α (0.05)
- **Do not reject H₀** if p-value ≥ 0.05

**Result:** **p-value = 0.0011 < 0.05** → **Reject the Null Hypothesis**

We have strong statistical evidence that the Treatment group has a **significantly higher** 30-day paid conversion rate than the Control group.

### Business Interpretation

**Statistical Conclusion:**  
The new onboarding and activation campaign produces a **statistically significant and practically large improvement** in paid conversion rate (+3.85pp / +121% relative). The result is highly unlikely to have occurred by chance alone (only ~0.11% probability under the null hypothesis).

**Business Implication:**  
From a pure conversion volume perspective, the campaign is a clear success. The Treatment more than doubled the rate at which new users become paying customers. This directly supports the primary business goal of improving user conversion.

**Important Caveats (Guardrails Must Be Considered):**
- While conversion improved dramatically, **support ticket incidence increased significantly** (+67.7% relative, p < 0.0001). This suggests the campaign may be bringing in more marginal users who require additional hand-holding.
- **Revenue per converted user is lower** in Treatment (~53% lower on average), driven by a shift toward Free plan conversions.
- **All observed refunds** occurred in the Treatment group.

**Recommendation aligned with test result:**  
**Do not launch broadly yet.** The statistically significant improvement in the North Star metric is real, but the accompanying increase in operational cost (support) and potential quality issues (refunds, lower ARPU per payer) mean we should:
1. Roll out selectively to the strongest segments (Mobile + Referral/Organic traffic), or
2. Iterate on the campaign to reduce support friction before scaling.

The hypothesis test confirms the campaign *works* on conversion. The business decision now hinges on whether the company is willing to accept higher support costs and slightly lower revenue per payer in exchange for significantly higher conversion volume.

---

## Files Generated for This Task

- `analysis/hypothesis_test_notes.md` — This document (Tasks 6 & 7)
- `outputs/hypothesis_test_output.png` — Visual summary of the test (created separately)

**Evidence of test execution:** The proportions z-test was performed using `statsmodels.stats.proportion.proportions_ztest` on the cleaned experiment data (n=1,400). Results are reproducible from the raw data in `campaign_experiment_data.xlsx`.