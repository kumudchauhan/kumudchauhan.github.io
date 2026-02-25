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
        <span>PyTorch</span>
        <span>Hugging Face</span>
        <span>SBERT</span>
        <span>FAISS</span>
        <span>Cross-Encoders</span>
        <span>Amazon SageMaker</span>
        <span>Snowflake</span>
        <span>SQL</span>
        <span>Python</span>
      </div>

      <div class="case-study-section">
        <h4>Business Problem</h4>
        <p>Fetch processes 11M+ receipts daily, extracting hundreds of millions of line items that need to be matched to an internal product catalog. The matching system needed to operate at scale with low latency, handle noisy and inconsistent input data, and maintain high precision to avoid revenue misattribution. For the full business context and problem reframing, see the <a href="/pages/casestudy-product-matching.html">Product & Strategy Case Study</a>.</p>
      </div>

      <div class="case-study-section">
        <h4>Accuracy Was Not the Bottleneck</h4>
        <p>Based on the root-cause analysis and the upper bound established through a human benchmark study (<a href="/pages/casestudy-product-matching.html">details in case study</a>), building better semantic search algorithms and sentence transformer models was the obvious choice to close the gap to the ceiling. The core technical challenge was not model accuracy alone, but designing a system that balanced precision and recall under revenue risk constraints, handling catalog gaps, noisy input data, and entity resolution failures at scale.</p>
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
        <p><strong style="color: #0f172a;">Existing Direct Match</strong>: Fetch already had a deterministic lookup system matching receipt items via SKU, UPC, and barcode identifiers. This handled a portion of items with exact matches, but left a significant gap for items with noisy, abbreviated, or missing identifiers.</p>
        <p><strong style="color: #0f172a;">Semantic Search Algorithm</strong>: to close this gap, I designed a semantic matching pipeline using Sentence-BERT (SBERT) embeddings. Experimented with multiple sentence transformer models including all-MiniLM-L6-v2 (384-dim), all-mpnet-base-v2 (768-dim), and BERT-based variants, evaluating tradeoffs between embedding quality, latency, and memory footprint. Fine-tuned using cosine similarity loss and MultipleNegativesRankingLoss (MNR) on domain-specific product pairs to learn receipt-to-catalog semantic similarity.</p>
        <p><strong style="color: #0f172a;">Input Representation Experiments</strong>: experimented with different input text representations to enrich the embedding model with more contextual information. Tested product name alone, and various combinations of product name + size, unit, retailer, SKU, and price. Richer input representations improved matching for ambiguous or abbreviated items where description alone was insufficient.</p>
        <p><strong style="color: #0f172a;">Data Augmentation</strong>: implemented data augmentation strategies to improve model robustness, including synthetic generation of noisy product descriptions (abbreviations, misspellings, reordered tokens, and dropped fields) to simulate real-world receipt variability. This helped the model generalize across retailers and receipt formats without overfitting to clean catalog text.</p>
        <p><strong style="color: #0f172a;">Vector Index (FAISS)</strong>: normalized embeddings were indexed using FAISS (Facebook AI Similarity Search) with an inner product index for cosine similarity search. This enabled sub-millisecond approximate nearest neighbor retrieval across the full catalog, scaling efficiently as the product taxonomy grew without requiring model retraining.</p>
        <p><strong style="color: #0f172a;">Candidate Retrieval</strong>: implemented multi-strategy candidate generation combining the existing direct lookup, fuzzy matching (Levenshtein, TF-IDF), and SBERT + FAISS semantic retrieval. The goal was to maximize Recall@10, ensuring the correct product appeared in the candidate pool.</p>
        <p><strong style="color: #0f172a;">Ranking & Precision Optimization</strong>: the retrieval stage (SBERT + FAISS) uses a bi-encoder architecture, encoding query and catalog items independently for fast similarity search. For reranking, I used a cross-encoder model (ms-marco-MiniLM-L-6-v2) that takes both the receipt item and candidate product as a single input pair, enabling deeper token-level interaction and more accurate relevance scoring than bi-encoder similarity alone.</p>
        <p><strong style="color: #0f172a;">Confidence Calibration</strong>: tuned confidence thresholds on the 50K+ gold dataset to find the optimal operating point on the precision-coverage tradeoff curve. This controlled the automation boundary, ensuring only high-confidence matches were auto-assigned while lower-confidence items were routed for review.</p>
      </div>

      <div class="case-study-section">
        <h4>Evaluation Strategy</h4>
        <p><strong style="color: #0f172a;">Offline ML Metrics</strong></p>
        <ul style="list-style: none; padding: 0; margin-top: 0.5rem;">
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Recall@10</strong>: measuring whether the correct product appeared in the top-10 candidates</li>
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Top-1 accuracy</strong>: measuring exact match at the top rank</li>
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">MRR (Mean Reciprocal Rank)</strong>: measuring ranking quality across candidates</li>
          <li style="color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Precision at operating threshold</strong>: ensuring automation didn't introduce revenue risk</li>
        </ul>
        <p style="margin-top: 0.75rem;"><strong style="color: #0f172a;">Business Metrics</strong></p>
        <ul style="list-style: none; padding: 0; margin-top: 0.5rem;">
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Points awarded accuracy</strong>: correctness of reward points attributed to users based on matched products</li>
          <li style="color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Dollar value of rewards</strong>: financial accuracy of rewards distributed, directly tied to partner billing and revenue reconciliation</li>
        </ul>
        <p style="margin-top: 0.75rem;">The 50K+ stratified gold dataset served as the foundation for all offline evaluation, and shadow deployments enabled safe comparison on live traffic before production release.</p>
      </div>

      <div class="case-study-section">
        <h4>Impact</h4>
        <ul style="list-style: none; padding: 0; margin-top: 0.5rem;">
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Coverage</strong>: 45% improvement in automated product assignment</li>
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Operations</strong>: ~30% reduction in manual review workload</li>
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Attribution</strong>: significantly improved partner attribution reliability, maintaining high precision at the operating threshold, enabling more accurate offer targeting and partner reporting for CPG partners</li>
          <li style="color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Scale</strong>: scalable architecture supporting millions of line items from 11M+ daily receipts, covering over $400M GMV, rewarding $500K+ every day</li>
        </ul>
      </div>

      <p style="margin-top: 2rem;"><a href="/pages/casestudy-product-matching.html">Read the Product & Strategy Case Study &rarr;</a></p>
      <p style="margin-top: 0.5rem;"><a href="/pages/projects.html">&larr; Back to Projects</a></p>

    </div>
  </div>
</section>
