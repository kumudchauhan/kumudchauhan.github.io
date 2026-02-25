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
        <ul style="list-style: none; padding: 0; margin-top: 0.5rem;">
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;">Fetch processes 11M+ receipts daily, extracting hundreds of millions of line items that need to be matched to an internal product catalog</li>
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;">The matching system needed to operate at scale with low latency, handle noisy and inconsistent input data, and maintain high precision to avoid revenue misattribution</li>
          <li style="color: #475569; line-height: 1.7;">For the full business context and problem reframing, see the <a href="/pages/casestudy-product-matching.html">Product & Strategy Case Study</a></li>
        </ul>
        <p style="margin-top: 1rem; margin-bottom: 0.5rem;"><strong style="color: #0f172a;">Example: Receipt Line Item to Catalog Match</strong></p>
        <table style="width: 100%; border-collapse: collapse; font-size: 0.9rem; margin-top: 0.5rem;">
          <thead>
            <tr style="border-bottom: 2px solid #e2e8f0;">
              <th style="text-align: left; padding: 0.5rem 0.75rem; color: #0f172a;">Receipt Line Item</th>
              <th style="text-align: left; padding: 0.5rem 0.75rem; color: #0f172a;">Catalog Product</th>
              <th style="text-align: left; padding: 0.5rem 0.75rem; color: #0f172a;">Match Type</th>
            </tr>
          </thead>
          <tbody>
            <tr style="border-bottom: 1px solid #e2e8f0;">
              <td style="padding: 0.5rem 0.75rem; color: #475569;">ORG MILK 1GAL</td>
              <td style="padding: 0.5rem 0.75rem; color: #475569;">Organic Whole Milk 1 Gallon</td>
              <td style="padding: 0.5rem 0.75rem; color: #475569;">SKU match</td>
            </tr>
            <tr style="border-bottom: 1px solid #e2e8f0;">
              <td style="padding: 0.5rem 0.75rem; color: #475569;">CHKN BRST BNLS</td>
              <td style="padding: 0.5rem 0.75rem; color: #475569;">Fresh Chicken Breast</td>
              <td style="padding: 0.5rem 0.75rem; color: #475569;">Semantic</td>
            </tr>
            <tr style="border-bottom: 1px solid #e2e8f0;">
              <td style="padding: 0.5rem 0.75rem; color: #475569;">EVOO 500ML</td>
              <td style="padding: 0.5rem 0.75rem; color: #475569;">Extra Virgin Olive Oil 500ml</td>
              <td style="padding: 0.5rem 0.75rem; color: #475569;">Semantic</td>
            </tr>
            <tr style="border-bottom: 1px solid #e2e8f0;">
              <td style="padding: 0.5rem 0.75rem; color: #475569;">PNT BTR CRMY 16OZ</td>
              <td style="padding: 0.5rem 0.75rem; color: #475569;">Peanut Butter Creamy 16oz</td>
              <td style="padding: 0.5rem 0.75rem; color: #475569;">Semantic</td>
            </tr>
            <tr>
              <td style="padding: 0.5rem 0.75rem; color: #475569;">GRD BEEF 80/20</td>
              <td style="padding: 0.5rem 0.75rem; color: #475569;">Ground Beef 80/20</td>
              <td style="padding: 0.5rem 0.75rem; color: #475569;">UPC match</td>
            </tr>
          </tbody>
        </table>
        <p style="margin-top: 0.5rem; color: #64748b; font-size: 0.85rem; line-height: 1.6;">Items with valid SKU/UPC identifiers are resolved via direct lookup. Items with abbreviated, noisy, or missing identifiers require semantic matching.</p>
      </div>

      <div class="case-study-section">
        <h4>Accuracy Was Not the Bottleneck</h4>
        <ul style="list-style: none; padding: 0; margin-top: 0.5rem;">
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;">Based on the root-cause analysis and the upper bound established through a human benchmark study (<a href="/pages/casestudy-product-matching.html">details in case study</a>), building better semantic search algorithms and sentence transformer models was the obvious choice to close the gap to the ceiling</li>
          <li style="color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">The core technical challenge was not model accuracy alone, but designing a system that balanced precision and recall under revenue risk constraints</strong>, handling catalog gaps, noisy input data, and entity resolution failures at scale</li>
        </ul>
      </div>

      <div class="case-study-section">
        <h4>Modeling Approach</h4>

        <!-- Pipeline Diagram -->
        <div style="margin: 1.5rem 0 2rem; padding: 1.5rem; background: #f8fafc; border-radius: 8px; border: 1px solid #e2e8f0;">
          <p style="text-align: center; font-weight: 600; color: #0f172a; margin-bottom: 1.25rem; font-size: 0.95rem;">Retrieval & Ranking Pipeline</p>

          <!-- Row 1: Input -->
          <div style="display: flex; justify-content: center; margin-bottom: 0.5rem;">
            <div style="background: #1e293b; color: #fff; padding: 0.6rem 1.25rem; border-radius: 6px; font-size: 0.85rem; font-weight: 500; text-align: center;">Receipt Line Items</div>
          </div>
          <div style="text-align: center; color: #94a3b8; font-size: 1.2rem; margin-bottom: 0.5rem;">&#8595;</div>

          <!-- Row 2: Direct Match -->
          <div style="display: flex; justify-content: center; margin-bottom: 0.5rem;">
            <div style="background: #fff; border: 2px solid #e2e8f0; padding: 0.6rem 1.25rem; border-radius: 6px; font-size: 0.85rem; text-align: center;">
              <strong style="color: #0f172a;">Direct Match Lookup</strong><br>
              <span style="color: #64748b; font-size: 0.8rem;">SKU / UPC / Barcode</span>
            </div>
          </div>

          <!-- Row 2b: Branch -->
          <div style="display: flex; justify-content: center; align-items: flex-start; gap: 2rem; margin-bottom: 0.5rem;">
            <div style="text-align: center;">
              <span style="color: #16a34a; font-size: 0.8rem; font-weight: 500;">Match found</span>
              <div style="color: #94a3b8; font-size: 1.2rem;">&#8595;</div>
              <div style="background: #f0fdf4; border: 2px solid #bbf7d0; padding: 0.5rem 1rem; border-radius: 6px; font-size: 0.8rem; color: #166534; font-weight: 500;">Matched Product</div>
            </div>
            <div style="text-align: center;">
              <span style="color: #dc2626; font-size: 0.8rem; font-weight: 500;">No match</span>
              <div style="color: #94a3b8; font-size: 1.2rem;">&#8595;</div>
            </div>
          </div>

          <!-- Row 3: SBERT + FAISS -->
          <div style="display: flex; justify-content: center; margin-bottom: 0.5rem;">
            <div style="background: #fff; border: 2px solid #e2e8f0; padding: 0.6rem 1.25rem; border-radius: 6px; font-size: 0.85rem; text-align: center;">
              <strong style="color: #0f172a;">Candidate Retrieval</strong><br>
              <span style="color: #64748b; font-size: 0.8rem;">SBERT Bi-Encoder + FAISS (Top-K)</span>
            </div>
          </div>
          <div style="text-align: center; color: #94a3b8; font-size: 1.2rem; margin-bottom: 0.5rem;">&#8595;</div>

          <!-- Row 4: Cross-Encoder -->
          <div style="display: flex; justify-content: center; margin-bottom: 0.5rem;">
            <div style="background: #fff; border: 2px solid #e2e8f0; padding: 0.6rem 1.25rem; border-radius: 6px; font-size: 0.85rem; text-align: center;">
              <strong style="color: #0f172a;">Cross-Encoder Reranking</strong><br>
              <span style="color: #64748b; font-size: 0.8rem;">ms-marco-MiniLM-L-6-v2</span>
            </div>
          </div>
          <div style="text-align: center; color: #94a3b8; font-size: 1.2rem; margin-bottom: 0.5rem;">&#8595;</div>

          <!-- Row 5: Confidence -->
          <div style="display: flex; justify-content: center; margin-bottom: 0.5rem;">
            <div style="background: #fff; border: 2px solid #e2e8f0; padding: 0.6rem 1.25rem; border-radius: 6px; font-size: 0.85rem; text-align: center;">
              <strong style="color: #0f172a;">Confidence Calibration</strong><br>
              <span style="color: #64748b; font-size: 0.8rem;">Precision-Coverage Threshold</span>
            </div>
          </div>

          <!-- Row 5b: Branch -->
          <div style="display: flex; justify-content: center; align-items: flex-start; gap: 2rem; margin-top: 0.5rem;">
            <div style="text-align: center;">
              <span style="color: #16a34a; font-size: 0.8rem; font-weight: 500;">High confidence</span>
              <div style="color: #94a3b8; font-size: 1.2rem;">&#8595;</div>
              <div style="background: #f0fdf4; border: 2px solid #bbf7d0; padding: 0.5rem 1rem; border-radius: 6px; font-size: 0.8rem; color: #166534; font-weight: 500;">Auto-Assigned</div>
            </div>
            <div style="text-align: center;">
              <span style="color: #f59e0b; font-size: 0.8rem; font-weight: 500;">Low confidence</span>
              <div style="color: #94a3b8; font-size: 1.2rem;">&#8595;</div>
              <div style="background: #fffbeb; border: 2px solid #fde68a; padding: 0.5rem 1rem; border-radius: 6px; font-size: 0.8rem; color: #92400e; font-weight: 500;">Manual Review</div>
            </div>
          </div>
        </div>
        <!-- End Pipeline Diagram -->

        <p style="margin-bottom: 0.75rem;"><strong style="color: #0f172a;">Gold Dataset</strong></p>
        <ul style="list-style: none; padding: 0; margin-top: 0;">
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;">Created a 50K+ stratified labeled dataset by merchant, frequency (head vs long-tail), OCR quality, and category</li>
          <li style="margin-bottom: 0.75rem; color: #475569; line-height: 1.7;">Defined annotation guidelines, achieved high inter-annotator agreement, and established the evaluation foundation</li>
        </ul>
        <p style="margin-bottom: 0.75rem;"><strong style="color: #0f172a;">Existing Direct Match</strong></p>
        <ul style="list-style: none; padding: 0; margin-top: 0;">
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;">Fetch already had a deterministic lookup system matching receipt items via SKU, UPC, and barcode identifiers</li>
          <li style="margin-bottom: 0.75rem; color: #475569; line-height: 1.7;">Handled a portion of items with exact matches, but left a significant gap for items with noisy, abbreviated, or missing identifiers</li>
        </ul>
        <p style="margin-bottom: 0.75rem;"><strong style="color: #0f172a;">Semantic Search Algorithm</strong></p>
        <ul style="list-style: none; padding: 0; margin-top: 0;">
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;">Designed a semantic matching pipeline using Sentence-BERT (SBERT) embeddings</li>
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;">Experimented with multiple sentence transformer models: all-MiniLM-L6-v2 (384-dim), all-mpnet-base-v2 (768-dim), and BERT-based variants, evaluating tradeoffs between embedding quality, latency, and memory footprint</li>
          <li style="margin-bottom: 0.75rem; color: #475569; line-height: 1.7;">Fine-tuned using cosine similarity loss and MultipleNegativesRankingLoss (MNR) on domain-specific product pairs to learn receipt-to-catalog semantic similarity</li>
        </ul>
        <p style="margin-bottom: 0.75rem;"><strong style="color: #0f172a;">Input Representation Experiments</strong></p>
        <ul style="list-style: none; padding: 0; margin-top: 0;">
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;">Experimented with different input text representations to enrich the embedding model with more contextual information</li>
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;">Tested product name alone, and various combinations of product name + size, unit, retailer, SKU, and price</li>
          <li style="margin-bottom: 0.75rem; color: #475569; line-height: 1.7;">Richer input representations improved matching for ambiguous or abbreviated items where name alone was insufficient</li>
        </ul>
        <p style="margin-bottom: 0.75rem;"><strong style="color: #0f172a;">Data Augmentation</strong></p>
        <ul style="list-style: none; padding: 0; margin-top: 0;">
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;">Synthetic generation of noisy product descriptions: abbreviations, misspellings, reordered tokens, and dropped fields</li>
          <li style="margin-bottom: 0.75rem; color: #475569; line-height: 1.7;">Helped the model generalize across retailers and receipt formats without overfitting to clean catalog text</li>
        </ul>
        <p style="margin-bottom: 0.75rem;"><strong style="color: #0f172a;">Vector Index (FAISS)</strong></p>
        <ul style="list-style: none; padding: 0; margin-top: 0;">
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;">Normalized embeddings indexed using FAISS (Facebook AI Similarity Search) with an inner product index for cosine similarity search</li>
          <li style="margin-bottom: 0.75rem; color: #475569; line-height: 1.7;">Sub-millisecond approximate nearest neighbor retrieval across the full catalog, scaling efficiently as the taxonomy grew without requiring model retraining</li>
        </ul>
        <p style="margin-bottom: 0.75rem;"><strong style="color: #0f172a;">Candidate Retrieval</strong></p>
        <ul style="list-style: none; padding: 0; margin-top: 0;">
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;">Multi-strategy candidate generation combining direct lookup, fuzzy matching (Levenshtein, TF-IDF), and SBERT + FAISS semantic retrieval</li>
          <li style="margin-bottom: 0.75rem; color: #475569; line-height: 1.7;">Optimized for Recall@10, ensuring the correct product appeared in the candidate pool</li>
        </ul>
        <p style="margin-bottom: 0.75rem;"><strong style="color: #0f172a;">Ranking & Precision Optimization</strong></p>
        <ul style="list-style: none; padding: 0; margin-top: 0;">
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;">Retrieval stage (SBERT + FAISS) uses a bi-encoder architecture, encoding query and catalog items independently for fast similarity search</li>
          <li style="margin-bottom: 0.75rem; color: #475569; line-height: 1.7;">Reranking via cross-encoder model (ms-marco-MiniLM-L-6-v2) that takes both receipt item and candidate product as a single input pair, enabling deeper token-level interaction and more accurate relevance scoring</li>
        </ul>
        <p style="margin-bottom: 0.75rem;"><strong style="color: #0f172a;">Confidence Calibration</strong></p>
        <ul style="list-style: none; padding: 0; margin-top: 0;">
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;">Tuned confidence thresholds on the 50K+ gold dataset to find the optimal operating point on the precision-coverage tradeoff curve</li>
          <li style="color: #475569; line-height: 1.7;">Only high-confidence matches auto-assigned; lower-confidence items routed for review</li>
        </ul>
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
        <h4>Key Takeaways & Challenges</h4>
        <ul style="list-style: none; padding: 0; margin-top: 0.5rem;">
          <li style="margin-bottom: 0.75rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Noisy identifiers and short descriptions</strong>: receipt line items often contained abbreviated product names (e.g., "GV 2% MLK 1GL" for "Great Value 2% Reduced Fat Milk, 1 Gallon"), partial UPC/SKU codes with trailing zeros or mismatched formats, making direct text matching unreliable</li>
          <li style="margin-bottom: 0.75rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">OCR errors in physical receipts</strong>: scanned paper receipts introduced misspellings, merged words, and missing characters (e.g., "CHBNI VAN YGT" for "Chobani Vanilla Greek Yogurt"), further degrading match quality</li>
          <li style="margin-bottom: 0.75rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Large, evolving taxonomy</strong>: the product catalog was continuously growing, requiring the system to generalize to new products without retraining</li>
          <li style="color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Data drift and continuous inference on unseen items</strong>: millions of new and unknown items were inferred daily against fixed catalog embeddings, requiring iterative retraining, gold dataset refresh, and ongoing monitoring to maintain match quality as product distributions shifted over time</li>
        </ul>
        <p style="margin-top: 0.75rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Continuous improvement</strong>: error analysis and active learning via uncertainty sampling to identify high-value training examples and iteratively improve model performance.</p>
      </div>

      <div class="case-study-section">
        <h4>Production Deployment</h4>
        <p style="margin-bottom: 0.75rem;"><strong style="color: #0f172a;">Load Testing & Latency Optimization</strong></p>
        <ul style="list-style: none; padding: 0; margin-top: 0;">
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;">Conducted load testing to validate throughput and latency under production traffic volumes</li>
          <li style="margin-bottom: 0.75rem; color: #475569; line-height: 1.7;">Converted trained PyTorch models to ONNX format for optimized inference, reducing latency and increasing throughput for real-time serving</li>
        </ul>
        <p style="margin-bottom: 0.75rem;"><strong style="color: #0f172a;">Telemetry & Monitoring</strong></p>
        <ul style="list-style: none; padding: 0; margin-top: 0;">
          <li style="margin-bottom: 0.75rem; color: #475569; line-height: 1.7;">Set up telemetry for model performance metrics, tracking latency percentiles (p90, p95, p99), throughput, and error rates across inference endpoints</li>
        </ul>
        <p style="margin-bottom: 0.75rem;"><strong style="color: #0f172a;">Scaling</strong></p>
        <ul style="list-style: none; padding: 0; margin-top: 0;">
          <li style="color: #475569; line-height: 1.7;">Horizontal scaling with auto-scaling SageMaker endpoints to handle traffic spikes and sustained high-volume processing across millions of daily line items</li>
        </ul>
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
