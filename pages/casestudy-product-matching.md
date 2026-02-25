---
layout: page
title: "Case Study: Designing a Revenue-Aligned Product Matching System at Scale"
description: Product strategy and analytical leadership case study at Fetch Rewards
---

<div class="page-hero">
  <h1>Designing a Revenue-Aligned Product Matching System at Scale</h1>
  <p class="subtitle">Tech Lead, Senior Data Scientist | Fetch Rewards</p>
  <p style="color: #2563eb; font-size: 0.95rem; font-weight: 500; margin-top: 0.25rem;">Revenue-First Thinking · Diagnostic Analysis · Hybrid ML Architecture</p>
  <p style="color: #64748b; font-size: 0.95rem; margin-top: 0.5rem;">6M+ daily active users · 11M+ receipts/day · hundreds of millions of line items</p>
</div>

<section>
  <div class="section-container">
    <div class="about-content">

      <div class="case-study-section">
        <h4>The Business Problem</h4>
        <p>With 6M+ daily active users and 11M+ receipts processed every day, Fetch's system extracted hundreds of millions of line items from receipts. Each line item needed to be matched to a known product in an internal taxonomy to power offer eligibility, brand attribution, partner billing, and rewards calculation. This matching pipeline was a core revenue driver, directly connecting user purchases to 600+ brand partners.</p>
        <p style="margin-top: 0.75rem;">At the time, a significant portion of these items were not being automatically matched, requiring heavy manual review and limiting the value of receipt data at scale. Improving automated product assignment was a strategic priority.</p>
        <p style="margin-top: 0.75rem;">But early discussions framed the problem as: "We need higher match accuracy."</p>
        <p style="margin-top: 0.75rem;">Before building ML models, gaining clarity and understanding the key problem is important to establish the goal. I asked:</p>
        <ul style="list-style: none; padding: 0; margin-top: 0.5rem;">
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• What does "higher accuracy" mean in terms of business outcomes?</li>
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Which product categories and retailers matter most?</li>
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• What is the revenue impact of unmatched items?</li>
          <li style="color: #475569; line-height: 1.7;">• What are the constraints of the current product catalog?</li>
        </ul>
        <p style="margin-top: 0.75rem;"><strong style="color: #0f172a;">This reframed the initiative from a modeling problem to a product systems problem.</strong></p>
      </div>

      <div class="case-study-section">
        <h4>Diagnostic Deep Dive: Understanding Failure</h4>
        <p>Instead of immediately iterating on ML models, I conducted a structured failure analysis.</p>
        <p style="margin-top: 0.75rem;"><strong style="color: #0f172a;">Sampling Approach</strong></p>
        <p style="color: #475569; line-height: 1.7;">Stratified sample of 50,000 recent unmatched line items, balanced across merchants, frequency bands, OCR quality, and categories.</p>
        <p style="margin-top: 0.75rem;"><strong style="color: #0f172a;">Key Questions</strong></p>
        <ul style="list-style: none; padding: 0; margin-top: 0.5rem;">
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Are failures due to algorithm limitations or catalog gaps?</li>
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Are unmatched items concentrated in specific categories?</li>
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Do they represent high-revenue products?</li>
          <li style="color: #475569; line-height: 1.7;">• What is the realistic performance ceiling?</li>
        </ul>
      </div>

      <div class="case-study-section">
        <h4>The Pareto Insight (80/20 Rule)</h4>
        <p>The distribution followed a classic 80/20 pattern. A small percentage of SKUs drove the vast majority of revenue-relevant volume. Meanwhile, a large volume of unmatched items belonged to:</p>
        <ul style="list-style: none; padding: 0; margin-top: 0.5rem;">
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Produce and commodity grocery</li>
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Pharmacy prescriptions</li>
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Gas station receipts</li>
          <li style="color: #475569; line-height: 1.7;">• Restaurant toppings and substitutions</li>
        </ul>
        <p style="margin-top: 0.75rem;">These categories were not partner-priority segments, carried lower revenue impact, and distorted raw match rate metrics.</p>
        <p style="margin-top: 0.75rem;">Among the revenue-relevant unmatched items, failures were driven by:</p>
        <ul style="list-style: none; padding: 0; margin-top: 0.5rem;">
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• <strong style="color: #0f172a;">OCR errors</strong>: scanned paper receipts introduced misspellings, merged words, and missing characters, degrading text-based matching</li>
          <li style="color: #475569; line-height: 1.7;">• <strong style="color: #0f172a;">Entity resolution</strong>: abbreviated product names, inconsistent brand naming, partial UPC/SKU codes, and varying unit formats across retailers made direct matching unreliable</li>
        </ul>
        <p style="margin-top: 0.75rem;">This led to a pivotal shift: <strong style="color: #0f172a;">optimize for revenue-weighted match accuracy, not raw match rate.</strong></p>
      </div>

      <div class="case-study-section">
        <h4>Measuring the System Ceiling</h4>
        <p>Before committing to aggressive targets, I designed a human benchmark study. Provided unmatched items to trained annotators, restricted them to the existing internal catalog, and measured maximum achievable match rate.</p>
        <p style="margin-top: 0.75rem;"><strong style="color: #0f172a;">This established a realistic upper bound under current catalog conditions.</strong></p>
        <p style="margin-top: 0.75rem;"><strong style="color: #0f172a;">Insight</strong>: performance is constrained not just by modeling, but by catalog completeness. This prevented unrealistic commitments and informed roadmap prioritization.</p>
      </div>

      <div class="case-study-section">
        <h4>Strategic Reframing</h4>
        <p>The solution became a two-track strategy:</p>
        <p style="margin-top: 0.75rem;"><strong style="color: #0f172a;">Track 1: Raise the Ceiling</strong></p>
        <ul style="list-style: none; padding: 0; margin-top: 0.5rem;">
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Identify high-frequency, revenue-relevant catalog gaps</li>
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Partner with catalog and data integrity teams</li>
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Prioritize enrichment for high-impact brands</li>
          <li style="color: #475569; line-height: 1.7;">• Map low-impact items to generic taxonomy buckets, avoiding unnecessary expansion of low-value segments</li>
        </ul>
        <p style="margin-top: 0.75rem;"><strong style="color: #0f172a;">Track 2: Close the Gap to Ceiling</strong></p>
        <p style="color: #475569; line-height: 1.7;">Redesigned the matching system as a hybrid retrieval architecture:</p>
        <ul style="list-style: none; padding: 0; margin-top: 0.5rem;">
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Entity normalization layer (OCR correction, brand mapping, unit standardization)</li>
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Multi-stage candidate generation: deterministic UPC matching, fuzzy matching, TF-IDF similarity, Sentence-BERT embeddings, approximate nearest neighbor search</li>
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Transformer-based reranking</li>
          <li style="color: #475569; line-height: 1.7;">• Confidence calibration to balance precision and recall</li>
        </ul>
      </div>

      <div class="case-study-section">
        <h4>Precision vs Coverage - A Deliberate Tradeoff</h4>
        <p>The system needed to maximize coverage while maintaining strict precision. False positives were not just an accuracy issue, they directly caused incorrect brand attribution and billing errors, creating revenue risk for both Fetch and its partners. I implemented:</p>
        <ul style="list-style: none; padding: 0; margin-top: 0.5rem;">
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Recall@K optimization at retrieval stage</li>
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Calibrated confidence thresholds</li>
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Precision-coverage tradeoff curves</li>
          <li style="color: #475569; line-height: 1.7;">• Shadow deployment before automation</li>
        </ul>
        <p style="margin-top: 0.75rem;"><strong style="color: #0f172a;">This ensured safe incremental rollout.</strong></p>
      </div>

      <div class="case-study-section">
        <h4>From Problem Reframing to Technical Execution</h4>
        <p>The analysis above redefined the problem from "improve match accuracy" to "maximize revenue-weighted coverage under strict precision constraints." This reframing shaped every downstream technical decision: the retrieval architecture, the ranking strategy, the confidence calibration, and the evaluation framework.</p>
        <p style="margin-top: 0.75rem;">The technical implementation involved a hybrid retrieval and ranking system combining deterministic matching, fuzzy search, semantic embeddings (Sentence-BERT, FAISS), transformer-based reranking, and calibrated confidence thresholds. For the full ML architecture and evaluation details, see the <a href="/pages/project-semantic-search.html">Technical Deep-Dive</a>.</p>
      </div>

      <div class="case-study-section">
        <h4>Results & Impact</h4>
        <ul style="list-style: none; padding: 0; margin-top: 0.5rem;">
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Coverage</strong>: 45% improvement in automated product assignment</li>
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Attribution</strong>: significantly improved partner attribution reliability</li>
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Operations</strong>: ~30% reduction in manual review workload</li>
          <li style="color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Scale</strong>: scalable architecture supporting millions of line items from 11M+ daily receipts, covering over $400M GMV, rewarding $500K+ every day</li>
        </ul>
      </div>

      <p style="margin-top: 2rem;"><a href="/pages/project-semantic-search.html">Read the ML Technical Deep-Dive &rarr;</a></p>
      <p style="margin-top: 0.5rem;"><a href="/pages/projects.html">&larr; Back to Projects</a></p>

    </div>
  </div>
</section>
