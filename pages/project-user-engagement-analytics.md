---
layout: page
title: User Engagement & Retention Analytics
description: Analytics framework for measuring and improving user engagement at scale
---

<div class="page-hero">
  <h1>User Engagement & Retention Analytics</h1>
  <p class="subtitle">KPI framework and experimentation platform — Fetch Rewards</p>
</div>

<section>
  <div class="section-container">
    <div class="about-content">

      <div class="case-study-meta" style="margin-bottom: 2rem;">
        <span>SQL</span>
        <span>Python</span>
        <span>pandas</span>
        <span>A/B Testing</span>
        <span>Tableau</span>
        <span>Snowflake</span>
      </div>

      <div class="case-study-section">
        <h4>Business Problem</h4>
        <p>As <a href="https://fetch.com" target="_blank" rel="noopener">Fetch Rewards</a> scaled to millions of active users, leadership wanted to understand what drives engagement and retention — and more importantly, predict and prevent churn before it happens. The existing reporting was retrospective and fragmented: teams could see that users were churning but couldn't explain why, couldn't identify at-risk users early enough to intervene, and had no way to quantify the revenue impact of retention changes. The question shifted from "how many users are active" to "which users are we about to lose, and what can we do about it."</p>
      </div>

      <div class="case-study-section">
        <h4>Challenges</h4>
        <ul style="list-style: none; padding: 0; margin-top: 0.5rem;">
          <li style="margin-bottom: 0.75rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Defining engagement in a multi-action product</strong> — Users interact through receipt scans, offer redemptions, referrals, and in-app games. A user scanning daily but never redeeming offers looks very different from one who redeems weekly but scans rarely — yet both could be "engaged." Defining a composite engagement signal that captures real value was non-trivial</li>
          <li style="margin-bottom: 0.75rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Survivorship bias in retention analysis</strong> — Naive retention metrics overcount healthy users and undercount early drop-offs, especially when acquisition spikes from marketing campaigns flood the cohorts with low-intent users</li>
          <li style="color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Actionability gap</strong> — Standard retention dashboards tell you what happened but not what to do about it. The challenge was building analytics that connect to interventions — which user segments respond to re-engagement nudges, which offers bring lapsed users back, and which users are lost regardless</li>
        </ul>
      </div>

      <div class="case-study-section">
        <h4>Approach</h4>
        <p><strong style="color: #0f172a;">Composite Engagement Scoring</strong> — Designed a weighted engagement score combining multiple behavioral signals — scan frequency, offer redemptions, session depth, and recency — into a single metric that reflects true user value. Segmented millions of users into behavioral tiers (power, regular, casual, at-risk) to enable targeted analysis and interventions.</p>
        <p><strong style="color: #0f172a;">Cohort & Retention Analysis</strong> — Built cohort-based retention analysis using SQL and Python (pandas) on millions of user records, controlling for acquisition channel and campaign timing to account for survivorship bias. Tracked D1, D7, D30, D90 retention curves by segment. Identified early behavioral predictors of long-term retention — users who completed a specific sequence of actions within the first week retained at significantly higher rates.</p>
        <p><strong style="color: #0f172a;">Platform & Version-Level Analysis</strong> — Dissected user behavior across iOS and Android platforms to identify platform-specific patterns in engagement and drop-off. Mapped the complete user flow — app open, receipt snap, receipt processing, information extraction, and reward attribution — to pinpoint exactly where users were dropping off and whether the bottlenecks differed across platforms. Narrowed the analysis further to app version level to isolate behavior changes tied to specific feature releases, helping the product team understand whether a retention shift was a platform issue, a feature regression, or a broader trend.</p>
        <p><strong style="color: #0f172a;">Churn Prediction & Intervention</strong> — Built predictive models to identify at-risk users before they lapse. Connected churn risk scores to actionable intervention strategies — targeted push notifications, personalized offer recommendations, and re-engagement campaigns. Measured the incremental impact of each intervention through controlled experiments.</p>
        <p><strong style="color: #0f172a;">Experimentation Support</strong> — Designed the analytics layer for A/B testing product changes. Defined primary and guardrail metrics, sample size calculations, and sequential testing methodology. Built automated experiment dashboards for product managers to self-serve results.</p>
        <p><strong style="color: #0f172a;">Executive Reporting</strong> — Built dashboards and automated reporting pipelines using SQL and Python, tracking engagement health, retention trends, churn risk distribution, and intervention effectiveness. Replaced fragmented team-level reports with a single source of truth for weekly business reviews.</p>
      </div>

      <div class="case-study-section">
        <h4>Evaluation Strategy</h4>
        <ul style="list-style: none; padding: 0; margin-top: 0.5rem;">
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Retention cohorts</strong> — D1, D7, D30, D90 retention tracked by acquisition channel and user segment</li>
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Engagement intensity</strong> — Scans per user per week, offers redeemed, session frequency</li>
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Feature adoption</strong> — Adoption curves and impact on retention for new product features</li>
          <li style="color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Experiment velocity</strong> — Number of experiments shipped, statistical power achieved, decision turnaround time</li>
        </ul>
      </div>

      <div class="case-study-section">
        <h4>Impact</h4>
        <p>Established the company's first unified engagement and retention analytics framework, adopted across product, marketing, and leadership. The KPI framework became the foundation for weekly business reviews and board-level reporting. Cohort analysis directly informed product decisions around onboarding flow optimization, resulting in measurable improvements in early retention. The experimentation framework enabled the product team to ship data-driven feature changes with confidence, increasing experiment velocity across the organization.</p>
      </div>

      <p style="margin-top: 2rem;"><a href="/pages/projects.html">&larr; Back to Projects</a></p>

    </div>
  </div>
</section>
