---
layout: page
title: Offer Performance & Campaign Analytics
description: Data-driven framework for measuring and optimizing brand offer performance
---

<div class="page-hero">
  <h1>Offer Performance & Campaign Analytics</h1>
  <p class="subtitle">Measuring what moves the needle for brand partners, Fetch Rewards</p>
</div>

<section>
  <div class="section-container">
    <div class="about-content">

      <div class="case-study-meta" style="margin-bottom: 2rem;">
        <span>SQL</span>
        <span>Python</span>
        <span>Causal Inference</span>
        <span>Looker</span>
        <span>Snowflake</span>
      </div>

      <div class="case-study-section">
        <h4>Business Problem</h4>
        <p>Fetch Rewards partners with 600+ brands (CPG companies, retailers, restaurants) who run promotional offers on the platform, rewarding users with bonus points for purchasing specific products. These brand partnerships are a core revenue driver for Fetch. However, there was no standardized way to measure offer effectiveness, compare campaign performance across brands, or provide partners with clear attribution on whether their spend was driving incremental purchases versus rewarding behavior that would have happened anyway.</p>
      </div>

      <div class="case-study-section">
        <h4>Challenges</h4>
        <ul style="list-style: none; padding: 0; margin-top: 0.5rem;">
          <li style="margin-bottom: 0.75rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Incrementality measurement</strong>: distinguishing between purchases driven by the offer versus purchases that would have occurred regardless is a fundamental attribution challenge</li>
          <li style="margin-bottom: 0.75rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Diverse offer mechanics</strong>: offers varied widely in structure (buy X get Y points, spend thresholds, category-level vs SKU-level), making standardized comparison difficult</li>
          <li style="color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Partner reporting expectations</strong>: brand partners expected clear, defensible ROI metrics tied to actual purchase behavior, not just engagement proxies like impressions or clicks</li>
        </ul>
      </div>

      <div class="case-study-section">
        <h4>Approach</h4>
        <p><strong style="color: #0f172a;">Offer Performance Framework</strong>: designed a standardized metrics framework for measuring offer effectiveness across all campaign types. Defined core KPIs: redemption rate, cost per redemption, incremental sales lift, brand switching rate, repeat purchase rate, and customer acquisition cost for new-to-brand buyers.</p>
        <p><strong style="color: #0f172a;">Incrementality Analysis</strong>: built a causal inference framework to measure the true incremental impact of offers. Used matched control groups (propensity score matching) and difference-in-differences methodology to isolate the effect of offer exposure from organic purchasing behavior. This gave partners defensible evidence of whether their campaigns were driving new purchases.</p>
        <p><strong style="color: #0f172a;">Campaign Reporting & Insights</strong>: built automated campaign reporting pipelines that generated post-campaign performance reports for brand partners. Reports included redemption trends, audience composition, basket analysis (what else did offer redeemers buy), and competitive context (market share shifts during campaign period).</p>
        <p><strong style="color: #0f172a;">Optimization Recommendations</strong>: analyzed historical campaign data to identify patterns in high-performing offers (optimal point values, timing, targeting segments, and offer structures). Provided data-backed recommendations to the partnerships team for campaign design and renewal discussions.</p>
      </div>

      <div class="case-study-section">
        <h4>Key Metrics</h4>
        <ul style="list-style: none; padding: 0; margin-top: 0.5rem;">
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Redemption rate</strong>: percentage of exposed users who redeemed the offer</li>
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Incremental sales lift</strong>: causal estimate of additional purchases driven by the campaign</li>
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">New-to-brand rate</strong>: percentage of redeemers who had not previously purchased the brand</li>
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Repeat purchase rate</strong>: post-campaign retention of offer redeemers</li>
          <li style="color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Partner ROI</strong>: revenue attributed per dollar of offer spend</li>
        </ul>
      </div>

      <div class="case-study-section">
        <h4>Impact</h4>
        <p>Established the company's first standardized offer performance measurement framework, adopted by the partnerships and sales teams for all brand campaign reporting. The incrementality framework gave partners clear, defensible evidence of campaign ROI, strengthening renewal conversations and enabling data-driven campaign optimization. Automated reporting reduced the analytics team's ad-hoc reporting burden, freeing up capacity for deeper strategic analysis. Optimization insights directly informed campaign design, improving offer performance over successive campaigns.</p>
      </div>

      <p style="margin-top: 2rem;"><a href="/pages/projects.html">&larr; Back to Projects</a></p>

    </div>
  </div>
</section>
