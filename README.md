# SQL - Sales Analysis

## Overview
This project delivers a deep analysis of customer lifetime value, retention, and revenue patterns—critical for driving sustainable growth. Using advanced SQL techniques like window functions, cohort grouping, percentile-based segmentation, and churn logic, the analysis reveals a major dependence on high-value customers and severe retention challenges far below industry benchmarks. The insights enable the business to shift from acquisition-heavy growth to retention-focused strategies, optimize customer value, and address structural risks affecting long-term profitability.


## Business Questions
1. Who are the most valuable customers, and how is value distributed across the customer base?
2. How has customer value evolved over time across different cohorts?
3. Are we effectively retaining customers, or are we overly reliant on acquiring new ones?

## Analysis Approach

### 1. Customer Segmentation
- Calculated total LTV per customer by aggregating net revenue from the cohort analysis table.

- Segmented customers into Low, Mid, and High-Value tiers using the 25th and 75th percentiles of total LTV distribution.

- Summarized each segment's total and average LTV, along with customer count, to assess overall value contribution.

🖥️Query: [1_customer_segmentation](/1_customer_segmentation.sql)

**📈 Visualization:**
![Customer Segmentation](/Images/1_customer_segments.png)

📊**Key Findings:**
- High-Value customers, though only 25% of the base, drive nearly two-thirds (65%) of total lifetime value. With an average LTV of over $10,900 per customer, this segment represents a disproportionately important group for retention, upsell, and long-term relationship efforts.

- Mid-Value customers account for the largest segment by count (50%) and contribute 32% of total LTV. While their average value (~$2,700) is significantly lower than High-Value customers, they present a scalable opportunity for growth if value per customer can be increased through targeted interventions.

- Low-Value customers make up 25% of the base but contribute less than 3% of overall LTV, with an average customer value under $400. This segment may not justify high-touch investment, and could benefit from automation or cost-efficient engagement strategies.

💡**Business Insights**
- Double down on High-Value customers with retention and loyalty strategies
Since this group contributes ~65% of total LTV, focus on personalized experiences, early-access offers, or premium programs to keep them engaged. Even a small increase in retention or referral from this group could drive significant revenue impact.

- Design upgrade campaigns for Mid-Value customers
With ~50% of customers and moderate average LTV, this segment is primed for growth. Use targeted upselling, bundling, or incentive-based loyalty programs to encourage them to transition into the High-Value bracket.

- Minimize spend on Low-Value customers and automate their touchpoints
Given their low contribution (<3% of LTV), these customers are best served through low-cost digital channels like email nurture flows, self-service tools, or community support — freeing up budget to invest where it matters more.

### 2. Cohort Analysis
- Calculated revenue and total customer per cohort.
- Cohorts were counted by the year of first purchase.
- Analyzed customer retention at a cohort level.



🖥️Query: [2_cohort_analysis.sql](/2_cohort_analysis.sql)

**📈 Visualization:**

![Cohort Analysis](/Images/2_cohort_analysis.png)

📊**Key Findings:**

- Alarming decrease in customer revenue: Revenue per customer dropped by over 60% from $5,272 in 2015 to $2,038 in 2024, signaling potential value erosion.

- Steady downward trend: The decline is consistent year-over-year, especially sharp after 2021, suggesting a systemic issue rather than a temporary dip.

- Recent cohorts underperforming: The 2023 and 2024 cohorts show the lowest revenue per customer, raising concerns about customer quality, pricing strategy, or retention.

💡**Business Insights**
- Diminishing customer value: Newer cohorts generate significantly less revenue, suggesting weaker acquisition quality or reduced customer engagement.

- Product or pricing mismatch: The steady decline points to potential erosion in product-market fit or ineffective pricing strategies.

- Monetization and retention issues: Lower revenue may stem from faster churn or under-monetized users, highlighting gaps in onboarding, upselling, or retention efforts.

### 3. Retention Analysis
- **Identify Last Purchase per Customer**: Use window functions to determine each customer’s most recent purchase date within their cohort.

- **Define Churn vs. Active**: Classify customers as Churned if their last purchase was more than 6 months before the latest sales date, and Active otherwise.

- **Cohort-Level Retention Breakdown**: Aggregate customers by cohort year and status (Active vs. Churned) to calculate counts and percentage retention within each cohort.

🖥️Query: [3_retention_analysis](/3_retention_analysis.sql)

**📈 Visualization:**
![Retention Analysis](/Images/3_retention_analysis.png)

📊**Key Findings:**
- Churn rates are consistently high at 90–92%, with retention stuck at just 8–10% — significantly below e-commerce industry averages. Typical e-commerce customer retention rates range from 25% to 35% for first-time buyers converting to repeat customers, and 40–60% for returning customers (source: industry benchmarks like Shopify, Omniconvert, and Smile.io). This suggests a substantial gap and a strong need to improve post-purchase engagement, loyalty programs, and customer experience.

- Retention performance is remarkably stable across different customer cohort sizes, whether small (e.g., 2,825 total) or large (9,010 total). This suggests that churn is not directly correlated with cohort growth but likely driven by structural issues like product fit, engagement, or onboarding.

- Retention performance is remarkably stable across different customer cohort sizes, whether small (e.g., 2,825 total) or large (9,010 total). This suggests that churn is not directly correlated with cohort growth but likely driven by structural issues like product fit, engagement, or onboarding.

💡**Business Insights**
- High churn is a critical threat to sustainable revenue growth. With only 8–10% of customers retained per cohort—far below industry norms—the business is overly reliant on constant new customer acquisition, which is typically more expensive than retaining existing customers.

- Customer lifetime value (LTV) is being significantly suppressed by poor retention. Improving retention even modestly (e.g., from 9% to 15–20%) could dramatically increase average LTV, leading to higher profitability without proportionally increasing acquisition costs.
- Investigate root causes of churn through customer feedback, exit surveys, and behavior analysis, then prioritize fixing key pain points in product, service, or experience.


## Strategic Recommendations
### 1️⃣ Shift from Acquisition-Led to Retention-Driven Growth
→ Why:
With churn at 90–92%, the business model is unsustainable if growth relies primarily on acquiring new customers. Retaining existing customers is 3–7x more cost-effective than acquiring new ones and directly boosts LTV and profitability.

→ Action Steps:

- Redefine success metrics: Prioritize retention rate, repeat purchase rate, and LTV alongside acquisition metrics like CAC.

- Allocate budget toward post-purchase engagement, loyalty programs, and customer success initiatives.

- Implement win-back strategies for recently churned customers (e.g., special offers, check-ins, or reminders).

- Build a retention dashboard to track improvements cohort by cohort.

### 2️⃣ Redesign Onboarding and the First 30 Days Experience
→ Why:
Consistent churn across cohorts suggests customers aren’t seeing value fast enough. The first interaction period (first purchase to first repeat) is the biggest churn point.

→ Action Steps:

- Map the customer journey from first order to repeat purchase—identify drop-off points.

- Implement onboarding flows: Welcome emails, “how to get the most value” guides, proactive customer support, or unboxing experiences.

- Offer time-limited incentives (e.g., discounts, loyalty points) that nudge first-time buyers toward a second purchase quickly.

- Test whether faster delivery, surprise freebies, or proactive check-ins improve the repeat rate.

### 3️⃣ Deploy Segment-Specific Retention and Growth Tactics
→ Why:
Your High-Value customers (~25%) drive 65% of total revenue, while Low-Value customers (~25%) contribute less than 3%. A generic, one-size-fits-all strategy leaves growth on the table.

→ Action Steps:

- High-Value:

    💡Offer VIP perks (exclusive offers, priority support, or early access).

    💡Launch referral programs targeting this segment—they are likely your most powerful advocates.

- Mid-Value:

    💡Design upgrade paths: Bundling, upsells, personalized recommendations, or loyalty milestones to move them toward High-Value.

- Low-Value:

    💡Automate communication with this segment—email drip campaigns, SMS reminders, but avoid costly manual efforts.

    💡Focus acquisition less on audiences likely to fall into Low-Value, based on historical traits.

### 4️⃣ Address Product-Market Fit, Value Proposition, and Pricing
→ Why:
The revenue per customer is steadily declining across cohorts (from ~$5,272 in 2015 to ~$2,038 in 2024). This signals either a weakened value proposition, increasing competition, or a pricing misalignment.

→ Action Steps:

- Run qualitative research (customer interviews, churn surveys) to identify unmet needs or dissatisfaction.

- Explore pricing optimization: Test bundles, subscriptions, volume discounts, or premium tiers.

- Strengthen the product value: Improve quality, expand offerings, enhance UX, or differentiate from competitors.

- Update messaging to better communicate the most compelling product benefits that drive retention.

🏁 **Summary Focus**:

✅ Retention-first → Onboarding overhaul → Segment-driven growth → Fix product/pricing gaps


##Technical Details
- **Database:** PostgreSQL
- **Analysis Tools:** PostgreSQL, DBeaver, PGAdmin
- **Visualization:** Chat GPT


