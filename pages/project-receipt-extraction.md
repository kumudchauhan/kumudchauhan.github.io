---
layout: page
title: Digital Receipt Information Extraction System
description: Patented ML system for extracting key information from digital receipts at scale
---

<div class="page-hero">
  <h1>Digital Receipt Information Extraction System</h1>
  <p class="subtitle">Patented production ML system, Fetch Rewards</p>
</div>

<section>
  <div class="section-container">
    <div class="about-content">

      <div class="case-study-meta" style="margin-bottom: 2rem;">
        <span>PyTorch</span>
        <span>BERT</span>
        <span>Hugging Face</span>
        <span>Amazon SageMaker</span>
        <span>MLflow</span>
        <span>Comet</span>
      </div>

      <div class="case-study-section">
        <h4>Business Problem</h4>
        <p>Millions of digital receipts (emails, e-receipts) flow into Fetch daily as unstructured HTML documents. The system needed to automatically extract structured purchase data at two levels: <strong style="color: #0f172a;">item-level information</strong> (product description, price, quantity, product number/UPC/SKU) and <strong style="color: #0f172a;">retailer-level information</strong> (retailer name, order total, store address, email, and other available metadata). Accurate extraction at both levels was critical for product matching, reward attribution, and partner reporting. For the full business context and product strategy, see the <a href="/pages/casestudy-receipt-platform.html">Product & Leadership Case Study</a>.</p>
      </div>

      <div class="case-study-section">
        <h4>Challenges</h4>
        <p>This was a greenfield problem with several unique constraints:</p>
        <ul style="list-style: none; padding: 0; margin-top: 0.75rem;">
          <li style="margin-bottom: 0.75rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">No existing research for HTML receipts</strong>: SOTA models like LayoutLM relied on OCR and bounding boxes, designed for scanned documents, not HTML</li>
          <li style="margin-bottom: 0.75rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Latency tradeoff</strong>: an OCR-based pipeline added significant latency and degraded user experience</li>
          <li style="margin-bottom: 0.75rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Token length limitation</strong>: transformer models were capped at 512 tokens; receipts often exceeded that. This was 2021, well before generative AI models with long context capabilities</li>
          <li style="margin-bottom: 0.75rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Complex non-purchase content in HTML</strong>: digital receipts contained substituted items, returned items, recommended/promoted products, and unicode characters embedded in the markup, all of which needed to be distinguished from actual purchased items</li>
          <li style="margin-bottom: 0.75rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Restaurant and fast food ambiguity</strong>: toppings, modifiers, customizations, and combo sub-items created confusion for the model in distinguishing actual line items from their sub-items (e.g., is "Extra Cheese" a separate purchased item or a topping?)</li>
          <li style="color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Marketing noise mixed with purchase data</strong>: promotional banners, suggested products, and loyalty program messages were embedded directly in the HTML alongside real order items</li>
        </ul>
      </div>

      <div class="case-study-section">
        <h4>Approach</h4>
        <p>I designed an approach that worked directly on HTML, bypassing OCR entirely. Raw unstructured HTML receipts were pre-processed by stripping CSS styling, extracting text, and replacing certain HTML tags with special tokens to preserve the visually rich layout structure of receipts.</p>
        <p>To build domain knowledge, I performed Masked Language Modeling (MLM) on transformer models using millions of digital receipts, training the language model to understand eReceipt-specific patterns and vocabulary.</p>
        <p>For the labeled dataset, I used stratified random sampling and clustering techniques to ensure coverage across different receipt formats and to handle the long-tail distribution of retailers. The model was then supervised fine-tuned for a Named Entity Recognition (NER) task using BIO encoding, with an encoder-based transformer backbone and a token classification head to extract entities like product name, price, quantity, and retailer.</p>
        <p>The system started with a placeholder model, allowing me and my team to build the training and inference infrastructure in parallel while iteratively optimizing model accuracy and latency.</p>
        <p><strong style="color: #0f172a;">Iterative improvement strategy</strong>: prioritized model accuracy improvements in phases: first high-volume retailers (covering the majority of receipt traffic), then partner retailers and restaurants (directly tied to brand offer revenue), and finally tackling the long tail of less common formats and edge cases.</p>
      </div>

      <div class="case-study-section">
        <h4>Development & Evaluation Pipeline</h4>
        <p>Building this system required standing up the entire ML lifecycle from scratch. I started by hand-labeling training data myself to establish ground truth, then used that foundation to build and train an internal data annotation team for supervised fine-tuning at scale. Since receipts contain sensitive user data, I developed ML models to mask PII from digital receipts before handing them over to the annotation team.</p>
        <p>To improve performance on edge cases and low-volume formats, I leveraged active learning and data augmentation techniques:</p>
        <ul style="list-style: none; padding: 0; margin-top: 0.5rem;">
          <li style="margin-bottom: 0.75rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Training data enrichment via active learning</strong>: ran the model's predictions on unseen receipts, ingested those predictions into the annotation tool for human correction, and incorporated the corrected examples back into the training set. This bootstrapping strategy rapidly scaled labeled data coverage for underrepresented retailers and formats</li>
          <li style="color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Data augmentation</strong>: randomly substituted entity values (product names, prices, totals, retailer names) within receipt templates to generate synthetic training examples. This helped the model learn structural patterns independent of specific content, improving generalization on complex, edge-case, and low-volume retailer formats</li>
        </ul>
        <p style="margin-top: 0.75rem;"><strong style="color: #0f172a;">Evaluation Strategy:</strong></p>
        <ul style="list-style: none; padding: 0; margin-top: 0.5rem;">
          <li style="margin-bottom: 0.75rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Offline evaluation</strong>: held-out test datasets tracking precision, recall, and entity-level accuracy across model versions</li>
          <li style="margin-bottom: 0.75rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Shadow deployment infrastructure</strong>: built a separate shadow pipeline to run candidate models in parallel against the existing system, enabling side-by-side comparison on live traffic without impacting users</li>
          <li style="margin-bottom: 0.75rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Dashboards & reporting</strong>: built evaluation dashboards to track and compare metrics across model versions</li>
          <li style="margin-bottom: 0.75rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Entity-level error analysis</strong>: tracked false positives and false negatives by entity type (product description, price, quantity, retailer). For product entities, analyzed whether false positives were actual purchased items versus returned items, substituted products, or promotional recommendations misclassified as purchases</li>
          <li style="color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Price and amount confusion matrix</strong>: evaluated model confusion across price-related fields (item price, discount, coupon, subtotal, tax, order total) at both item-level and retailer-level, where misclassification between these fields had direct impact on reward attribution accuracy</li>
        </ul>
        <p style="margin-top: 0.75rem;">Post-deployment, I established a human-in-the-loop mechanism (weekly audits on real-time production data by an internal data integrity team, supported by a custom app for auditing and correcting model responses). Corrected examples were fed back into the training data for model retraining, creating a continuous improvement loop.</p>
      </div>

      <div class="case-study-section">
        <h4>Training Infrastructure</h4>
        <p>Model training built on PyTorch, Hugging Face, and transformer models with distributed GPU training. MLflow and Comet for experiment tracking and reproducibility. Amazon SageMaker for training pipelines, real-time inference, and auto-scaling endpoints. Automated retraining pipeline with CI/CD for model deployment. Dataset versioning, model versioning, and continuous monitoring for data and model drift.</p>
      </div>

      <div class="case-study-section">
        <h4>Impact</h4>
        <p>Designed and delivered a production-grade ML system processing hundreds of millions of receipts across thousands of retailers and formats, serving as a critical component of Fetch's core product experience. The in-house solution replaced external vendor dependency, saving millions in operational costs. The system met senior leadership expectations on accuracy based on human evaluations on production data. Enabled accurate offer matching and reward attribution for millions of active users. The novel approach to HTML-based receipt understanding resulted in a <a href="https://patents.google.com/patent/US12288151B2/en" target="_blank" rel="noopener">US patent</a>.</p>
      </div>

      <p style="margin-top: 2rem;"><a href="/pages/casestudy-receipt-platform.html">Read the Product & Leadership Case Study &rarr;</a></p>
      <p style="margin-top: 0.5rem;"><a href="/pages/projects.html">&larr; Back to Projects</a></p>

    </div>
  </div>
</section>
