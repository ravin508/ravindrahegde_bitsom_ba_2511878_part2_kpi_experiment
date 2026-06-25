# Executive Recommendation Memo: Onboarding Campaign A/B Test

**To:** Leadership Team (Product, Growth, Marketing, CS, Finance)  
**From:** Business Analytics  
**Subject:** Decision on New Onboarding & Activation Campaign Launch

---

## Recommendation

**Do not launch the new campaign (Treatment) to all users at this time.**

**Preferred path:**  
**Selective/segmented rollout** to high-performing segments (Mobile users, Referral/Organic/Paid Search traffic, North region) **combined with continued testing** on the full population with refinements to address support friction and refund signals. Implement strict guardrail monitoring.

---

## Key Findings (1,400 users; balanced groups)

### Strong Wins on Primary Metrics
- **Paid conversion rate:** Control 3.19% → Treatment **7.04%** (+3.85pp / **+121% relative**, p=0.001 **)
- Funnel lifts: visited_landing_page +8.8pp (p<0.001), completed_onboarding +5.5pp (p=0.008)
- Converters in Treatment activate **faster** (6.4 vs 8.9 days, p=0.008) and show **higher engagement** scores

### Guardrail Concerns (Triggered)
- **Support tickets significantly higher** in Treatment (mean 0.37 vs 0.22; 24.8% vs 14.8% of users, p<0.0001)
- **Refunds concentrated in Treatment:** 3 cases (0.42% overall rate, p=0.087 marginal) — all among paid converters (6% refund rate in Treatment paid users vs 0% Control)
- **Lower revenue per converter:** Treatment paid users generate ~53% less revenue on average (driven by shift to Free plan: 68% vs 50%)
- ARPU overall directionally positive but not significant due to variance

### Segment Insights
- **Best segments (strong lift, good sample):** Mobile (+4.8pp), Referral (+8.5pp), Organic, Paid Search, Free plan, North region
- **Weaker/flat:** Social traffic (slight negative), Basic plan (flat), Desktop/West (smaller lifts)

---

## Why This Decision?

The campaign delivers **clear activation volume wins** but triggers the exact risks highlighted in the experiment brief: increased support load and signals of lower-quality conversions (refunds + lower ARPU per payer). Launching broadly without fixing the support/refund drivers risks higher ops costs and margin erosion that could outweigh conversion gains.

The lift is large enough (+121% on paid conversion) that we should **capture it where it is cleanest** (Mobile + high-intent traffic sources) while iterating on the experience to reduce friction for broader rollout.

---

## Proposed Next Actions (Priority Order)

1. **Immediate (1-2 weeks):** Qualitative investigation — review the 3 Treatment refunds and categorize top support ticket reasons for Treatment cohort. Identify fixable onboarding/campaign messaging issues.
2. **Short-term (2-4 weeks):** Launch phased rollout to **Mobile + Referral/Organic traffic** (strongest lifts) with weekly guardrail dashboard (tickets, refunds, engagement). Set auto-pause triggers (e.g., refund rate >2% or ticket incidence >22%).
3. **Parallel:** Continue full-population experiment with **refined Treatment variant** (toned-down claims, better FAQ/in-app support prompts) aimed at support reduction.
4. **Medium-term:** Once root causes addressed and guardrails stabilized, expand to all users. Request 90-day retention/LTV data for final LTV impact validation.

---

## Decision Options Summary

| Option                    | Pros                              | Cons / Risks                     | Recommendation |
|---------------------------|-----------------------------------|----------------------------------|----------------|
| Launch to all            | Captures full conversion upside  | High support cost; refund risk; lower quality payers | **No** |
| Reject entirely          | Avoids guardrail issues          | Discards large, sig conversion lift | **No** |
| Selective + monitor      | Captures best segments; limits risk | Slightly lower total volume     | **Yes (preferred)** |
| Continue testing only    | More data; time to fix issues    | Delays any rollout              | Yes (parallel) |

---

## Bottom Line

**The new campaign works on volume but needs refinement on quality and support experience before broad launch.** We have a clear path to capture most of the upside quickly via segmentation while protecting the business on guardrails. This balanced approach aligns with our growth goals and risk tolerance.

Ready to discuss in next leadership sync. Detailed analysis and segment tables available in full README.md.

**Attachments:** `README.md` (full analysis), `funnel_results.csv`