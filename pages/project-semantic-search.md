---
layout: page
title: Product Matching via Semantic Search
description: Semantic search and retrieval system using SBERT and FAISS
---

<div class="page-hero">
  <h1>Product Matching via Semantic Search</h1>
  <p class="subtitle">Calibrated retrieval and ranking system, Fetch Rewards</p>
</div>

<section>
  <div class="section-container">
    <div class="about-content">

      <div class="case-study-meta" style="margin-bottom: 2rem;">
        <span>SBERT</span>
        <span>FAISS</span>
        <span>Cross-Encoders</span>
        <span>Gradient Boosting</span>
        <span>TF-IDF</span>
        <span>Python</span>
      </div>

      <div class="case-study-section">
        <h4>Business Problem</h4>
        <p>When a user submits a receipt on Fetch, each line item needs to be matched to a known product in the catalog. This is how Fetch connects purchases to brand offers and rewards users with the right points. At the time, a significant portion of receipt line items were not being automatically matched, requiring heavy manual review and limiting the value of receipt data at scale. With millions of receipts flowing in daily, improving match coverage was critical to unlocking better offer targeting, accurate reward attribution, and reducing operational overhead.</p>
      </div>

      <div class="case-study-section">
        <h4>Problem Reframing</h4>
        <p>The issue was not just low match coverage, it was a precision-recall imbalance problem under revenue risk constraints. Increasing coverage (recall) risked incorrect brand attribution, while increasing precision reduced automation. The true objective became: maximize coverage of receipt item mapping while maintaining high precision. This reframing shifted the solution from "build a better classifier" to "design a calibrated retrieval and ranking system."</p>
      </div>

      <div class="case-study-section">
        <h4>Challenges</h4>
        <ul style="list-style: none; padding: 0; margin-top: 0.5rem;">
          <li style="margin-bottom: 0.75rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Noisy identifiers and short descriptions</strong>: receipt line items often contained abbreviated product names, partial UPC/SKU codes with trailing zeros or mismatched formats, making direct text matching unreliable</li>
          <li style="margin-bottom: 0.75rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">OCR errors in physical receipts</strong>: scanned paper receipts introduced misspellings, merged words, and missing characters, further degrading match quality</li>
          <li style="color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Large, evolving taxonomy</strong>: the product catalog was continuously growing, requiring the system to generalize to new products without retraining</li>
        </ul>
      </div>

      <div class="case-study-section">
        <h4>Approach</h4>
        <p><strong style="color: #0f172a;">Gold Dataset</strong>: created a 50K+ stratified labeled dataset, stratified by merchant, frequency (head vs long-tail), OCR quality, and category. Defined annotation guidelines and achieved high inter-annotator agreement. This became the evaluation foundation.</p>
        <p><strong style="color: #0f172a;">Candidate Retrieval (Recall First)</strong>: the root issue was that the correct product often wasn't even in the candidate pool. Implemented multi-strategy retrieval: deterministic rules (UPC, exact matches), fuzzy matching (Levenshtein, TF-IDF), semantic retrieval using Sentence-BERT embeddings, and FAISS approximate nearest neighbor indexing for scalable vector search.</p>
        <p><strong style="color: #0f172a;">Ranking & Precision Optimization</strong>: built a ranking layer using cross-encoder transformer models and a feature-based gradient boosting model combining embedding similarity, token overlap, brand match, unit consistency, and merchant priors.</p>
      </div>

      <div class="case-study-section">
        <h4>Evaluation Strategy</h4>
        <p>The leadership goal was to increase product assignment accuracy and coverage significantly. I reframed this vague mandate into a measurable objective: maximize coverage of receipt item mapping while maintaining high precision, since incorrect brand attribution had direct billing and revenue implications.</p>
        <p>This reframing shifted the solution from "build a better classifier" to "design a calibrated retrieval and ranking system." Key evaluation metrics were redesigned around this objective:</p>
        <ul style="list-style: none; padding: 0; margin-top: 0.5rem;">
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Recall@K</strong>: measuring whether the correct product appeared in the top-K candidates</li>
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Top-1 accuracy</strong>: measuring exact match at the top rank</li>
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">MRR (Mean Reciprocal Rank)</strong>: measuring ranking quality across candidates</li>
          <li style="color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Precision at operating threshold</strong>: ensuring automation didn't introduce revenue risk</li>
        </ul>
        <p style="margin-top: 0.75rem;">Evaluation was designed before modeling. The 50K+ stratified gold dataset served as the foundation for all offline evaluation, and shadow deployments enabled safe comparison on live traffic before production release.</p>
      </div>

      <div class="case-study-section">
        <h4>Impact</h4>
        <p>Significantly improved product match coverage and ranking accuracy, substantially reducing manual review effort. Maintained high precision at the chosen threshold, improving brand attribution reliability for CPG partners. Reduced operational costs and enabled more accurate offer targeting, reward attribution, and partner reporting across millions of receipts and billions of line items.</p>
      </div>

      <p style="margin-top: 2rem;"><a href="/pages/projects.html">&larr; Back to Projects</a></p>

    </div>
  </div>
</section>
