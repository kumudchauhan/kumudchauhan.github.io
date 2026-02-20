---
layout: page
title: "Case Study: Scaling an AI-Powered Receipt Intelligence Platform"
description: Product strategy and technical leadership case study at Fetch Rewards
---

<div class="page-hero">
  <h1>A Scalable AI-Powered Receipt Intelligence System</h1>
  <p class="subtitle">Senior Data Scientist — Tech Lead | Fetch Rewards</p>
  <p style="color: #2563eb; font-size: 0.95rem; font-weight: 500; margin-top: 0.25rem;">Product Strategy · Technical Execution · Cross-Functional Delivery</p>
  <p style="color: #64748b; font-size: 0.95rem; margin-top: 0.5rem;">10M+ users · 1M+ receipts/day · 600+ brand partners</p>
</div>

<section>
  <div class="section-container">
    <div class="about-content">

      <div class="case-study-section">
        <h4>Executive Summary</h4>
        <p>I led the product strategy and cross-functional delivery of an in-house AI-powered receipt intelligence platform that replaced a high-cost third-party vendor. The solution improved product match accuracy across thousands of retailers, restaurants, and fast food chains, reduced operational overhead, and delivered multimillion-dollar annual cost savings while supporting 10M+ users and 600+ brand partners.</p>
      </div>

      <div class="case-study-section">
        <h4>The Business Problem</h4>
        <p>Fetch's receipt processing was handled by a third-party vendor, creating major issues:</p>
        <ul style="list-style: none; padding: 0; margin-top: 0.75rem;">
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">High recurring operational cost</strong> — Vendor pricing scaled with receipt volume, increasingly expensive as the user base grew</li>
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Limited control over accuracy and roadmap</strong> — No ability to iterate on extraction logic or prioritize improvements that mattered to our business</li>
          <li style="margin-bottom: 0.5rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Slow iteration cycles</strong> — Every improvement request or addition of a new partner/retailer went through the vendor's timeline, not ours</li>
          <li style="color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Poor customer support</strong> — Vendor dependency created bottlenecks in resolving user-facing issues quickly</li>
        </ul>
        <p style="margin-top: 1rem;">The business needed higher accuracy, faster iteration, lower cost, and scalable infrastructure. This case study covers the product strategy and leadership perspective. For the technical deep-dive into the ML system, see <a href="/pages/project-receipt-extraction.html">Digital Receipt Information Extraction System</a>.</p>
      </div>

      <div class="case-study-section">
        <h4>Product Vision</h4>
        <p>Build a scalable, in-house receipt intelligence platform that:</p>
        <ul style="list-style: none; padding: 0; margin-top: 0.5rem;">
          <li style="margin-bottom: 0.4rem; color: #475569; line-height: 1.7;">• Extracts structured purchase data from digital receipts (eReceipts)</li>
          <li style="margin-bottom: 0.4rem; color: #475569; line-height: 1.7;">• Improves match accuracy and reward attribution</li>
          <li style="margin-bottom: 0.4rem; color: #475569; line-height: 1.7;">• Improves customer experience</li>
          <li style="margin-bottom: 0.4rem; color: #475569; line-height: 1.7;">• Reduces vendor dependency and cost</li>
          <li style="margin-bottom: 0.4rem; color: #475569; line-height: 1.7;">• Integrates seamlessly into the mobile app experience</li>
          <li style="color: #475569; line-height: 1.7;">• Enables future experimentation and personalization</li>
        </ul>
        <p style="margin-top: 0.75rem;">The goal was not just technical replacement — it was strategic product ownership.</p>
      </div>

      <div class="case-study-section">
        <h4>Key Stakeholders</h4>
        <p>The receipt processing flow spans the full user journey: a user connects their email account, the app retrieves eReceipts via IMAP, the extraction service parses structured data from HTML, the matching system maps items to a product catalog, and rewards are attributed to the user and reported to brand partners.</p>
        <p style="margin-top: 0.5rem;">This required coordination across Product Management, Mobile Engineering, Backend Engineering, MLOps/SRE, QA, Brand Partnerships, and Operations. Downstream teams in analytics, reporting, and partner management depended on the quality of extracted data.</p>
        <p style="margin-top: 0.5rem;">My role was to integrate this system into Fetch's receipt processing flow without breaking downstream services, user experience, or revenue.</p>
      </div>

      <div class="case-study-section">
        <h4>Defining Success Metrics</h4>
        <p>Before building, aligned on measurable KPIs across three dimensions:</p>
        <p style="margin-top: 0.75rem;"><strong style="color: #0f172a;">Accuracy Metrics</strong></p>
        <ul style="list-style: none; padding: 0; margin-top: 0.25rem;">
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Product match accuracy</li>
          <li style="color: #475569; line-height: 1.7;">• Extraction precision & recall</li>
        </ul>
        <p style="margin-top: 0.75rem;"><strong style="color: #0f172a;">Business Metrics</strong></p>
        <ul style="list-style: none; padding: 0; margin-top: 0.25rem;">
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Reward attribution accuracy</li>
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Points awarded accuracy</li>
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Offer redemption accuracy</li>
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Partner reporting reliability</li>
          <li style="color: #475569; line-height: 1.7;">• Cost per receipt processed</li>
        </ul>
        <p style="margin-top: 0.75rem;"><strong style="color: #0f172a;">Operational Metrics</strong></p>
        <ul style="list-style: none; padding: 0; margin-top: 0.25rem;">
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Processing latency</li>
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Manual review volume</li>
          <li style="color: #475569; line-height: 1.7;">• System uptime</li>
        </ul>
        <p style="margin-top: 0.75rem;">Clear metrics helped align engineering effort with business impact.</p>
      </div>

      <div class="case-study-section">
        <h4>Strategy & Tradeoffs</h4>
        <p><strong style="color: #0f172a;">Build vs Buy Analysis</strong></p>
        <p>Evaluated vendor cost vs internal investment, speed to market vs long-term scalability, accuracy gains vs operational complexity, and better customer experience with quick debugging and fixes. The decision: invest in building an internal platform for long-term cost efficiency and product control.</p>
        <p style="margin-top: 0.75rem;"><strong style="color: #0f172a;">Key Tradeoffs Managed</strong></p>
        <ul style="list-style: none; padding: 0; margin-top: 0.5rem;">
          <li style="margin-bottom: 0.4rem; color: #475569; line-height: 1.7;">• Accuracy vs Processing Latency</li>
          <li style="margin-bottom: 0.4rem; color: #475569; line-height: 1.7;">• Model Complexity vs Operational Stability</li>
          <li style="margin-bottom: 0.4rem; color: #475569; line-height: 1.7;">• Automation vs Human-in-the-Loop Review</li>
          <li style="margin-bottom: 0.4rem; color: #475569; line-height: 1.7;">• On-Device Model vs Cloud-Based Inference</li>
          <li style="color: #475569; line-height: 1.7;">• Short-Term Fixes vs Scalable Architecture</li>
        </ul>
        <p style="margin-top: 0.5rem;">These decisions were made collaboratively across engineering and business teams.</p>
      </div>

      <div class="case-study-section">
        <h4>Roadmap & Execution</h4>
        <p><strong style="color: #0f172a;">Phase 1: Research & Foundation</strong></p>
        <ul style="list-style: none; padding: 0; margin-top: 0.25rem;">
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Research NLP models and benchmarking for receipt extraction</li>
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Build placeholder model to enable parallel infrastructure development</li>
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Collaboration with mobile engineers for IMAP integrations to retrieve HTML receipts</li>
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• PII masking pipeline</li>
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Training and inference pipeline setup</li>
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Build internal annotation team, data annotation infrastructure and tooling</li>
          <li style="color: #475569; line-height: 1.7;">• Establish standardized experimentation framework for ML model development</li>
        </ul>
        <p style="margin-top: 0.75rem;"><strong style="color: #0f172a;">Phase 2: Accuracy Optimization</strong></p>
        <ul style="list-style: none; padding: 0; margin-top: 0.25rem;">
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Improve extraction quality</li>
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Refine matching algorithms</li>
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Shadow testing against vendor output</li>
          <li style="color: #475569; line-height: 1.7;">• Introduce monitoring dashboards</li>
        </ul>
        <p style="margin-top: 0.75rem;"><strong style="color: #0f172a;">Phase 3: Operational Scaling</strong></p>
        <ul style="list-style: none; padding: 0; margin-top: 0.25rem;">
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• CI/CD automation</li>
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Production deployment on AWS</li>
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Load testing and horizontal scaling of inference endpoints</li>
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Define SLAs for receipt processing pipeline</li>
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Service telemetry (uptime, p90, p99 latency)</li>
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Monitoring & alerting system</li>
          <li style="color: #475569; line-height: 1.7;">• Human-in-the-loop feedback loop</li>
        </ul>
        <p style="margin-top: 0.75rem;"><strong style="color: #0f172a;">What I Owned</strong></p>
        <p style="margin-top: 0.25rem; color: #475569; line-height: 1.7; font-style: italic;">Dual role: hands-on IC on ML R&D while leading the team</p>
        <ul style="list-style: none; padding: 0; margin-top: 0.5rem;">
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Technical design of the ML pipeline</li>
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• R&D of NLP/ML models</li>
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Backlog prioritization and sprint planning</li>
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Cross-team coordination</li>
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Technical Design Review (TDR) presentations</li>
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• Annotation team management</li>
          <li style="margin-bottom: 0.3rem; color: #475569; line-height: 1.7;">• KPI monitoring</li>
          <li style="color: #475569; line-height: 1.7;">• UAT and release readiness</li>
        </ul>
      </div>

      <div class="case-study-section">
        <h4>Cross-Functional Leadership</h4>
        <p>I led an 8-member cross-functional team of data scientists, ML engineers, backend engineers, data analyst, and QA:</p>
        <ul style="list-style: none; padding: 0; margin-top: 0.5rem;">
          <li style="margin-bottom: 0.4rem; color: #475569; line-height: 1.7;">• Led daily standups and cross-team collaboration and agreements</li>
          <li style="margin-bottom: 0.4rem; color: #475569; line-height: 1.7;">• Translated ambiguous business goals into technical requirements</li>
          <li style="margin-bottom: 0.4rem; color: #475569; line-height: 1.7;">• Defined sprint-ready user stories</li>
          <li style="margin-bottom: 0.4rem; color: #475569; line-height: 1.7;">• Negotiated scope tradeoffs</li>
          <li style="margin-bottom: 0.4rem; color: #475569; line-height: 1.7;">• Removed blockers during execution</li>
          <li style="margin-bottom: 0.4rem; color: #475569; line-height: 1.7;">• Presented progress and impact to C-suite executives</li>
        </ul>
        <p style="margin-top: 0.5rem;">The platform touched multiple product surfaces — mobile app, backend services, and analytics dashboards — requiring tight coordination under startup-mode deadlines.</p>
      </div>

      <div class="case-study-section">
        <h4>Results & Impact</h4>
        <ul style="list-style: none; padding: 0; margin-top: 0.5rem;">
          <li style="margin-bottom: 0.75rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Accuracy</strong> — Significantly improved product match accuracy, meeting senior leadership expectations based on human evaluations on production data</li>
          <li style="margin-bottom: 0.75rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Cost</strong> — Delivered multimillion-dollar annual savings by replacing third-party vendor</li>
          <li style="margin-bottom: 0.75rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Operations</strong> — Reduced manual review workload through structured human-in-the-loop feedback loop</li>
          <li style="margin-bottom: 0.75rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Business</strong> — Improved reward attribution reliability for 600+ brand partners, enabling higher targeting precision and improved reporting trust</li>
          <li style="margin-bottom: 0.75rem; color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Scalability</strong> — Successfully processed 1M+ receipts per day at production scale</li>
          <li style="color: #475569; line-height: 1.7;"><strong style="color: #0f172a;">Innovation</strong> — Innovated a new state-of-the-art algorithm for digital receipt extraction directly from unstructured HTML layout/DOM, bypassing traditional OCR pipelines completely (<a href="/pages/project-receipt-extraction.html">ML Technical Deep-Dive</a> · <a href="https://patents.google.com/patent/US11727060B1" target="_blank">US Patent</a>)</li>
        </ul>
      </div>

      <div class="case-study-section">
        <h4>What Made This a Product Win — Not Just ML</h4>
        <p>This initiative succeeded because:</p>
        <ul style="list-style: none; padding: 0; margin-top: 0.5rem;">
          <li style="margin-bottom: 0.4rem; color: #475569; line-height: 1.7;">• Defined measurable business KPIs before building</li>
          <li style="margin-bottom: 0.4rem; color: #475569; line-height: 1.7;">• Treated it as a platform, not a one-off feature</li>
          <li style="margin-bottom: 0.4rem; color: #475569; line-height: 1.7;">• Balanced short-term business pressure with long-term architecture</li>
          <li style="margin-bottom: 0.4rem; color: #475569; line-height: 1.7;">• Adopted a fast experimentation and fail-early mindset</li>
          <li style="margin-bottom: 0.4rem; color: #475569; line-height: 1.7;">• Aligned stakeholders early</li>
          <li style="margin-bottom: 0.4rem; color: #475569; line-height: 1.7;">• Implemented monitoring & feedback loops</li>
          <li style="color: #475569; line-height: 1.7;">• A team of hardworking and talented data scientists, ML engineers, and backend engineers who made this possible</li>
        </ul>
      </div>

      <div class="case-study-section">
        <h4>Lessons Learned</h4>
        <ul style="list-style: none; padding: 0; margin-top: 0.5rem;">
          <li style="margin-bottom: 0.4rem; color: #475569; line-height: 1.7;">• Vendor dependency limits product innovation</li>
          <li style="margin-bottom: 0.4rem; color: #475569; line-height: 1.7;">• Early KPI alignment prevents misaligned engineering effort</li>
          <li style="margin-bottom: 0.4rem; color: #475569; line-height: 1.7;">• Monitoring and post-launch feedback are as critical as initial accuracy</li>
          <li style="margin-bottom: 0.4rem; color: #475569; line-height: 1.7;">• Cross-functional trust accelerates delivery more than technical brilliance alone</li>
          <li style="color: #475569; line-height: 1.7;">• Product success requires operational scalability, not just algorithmic performance</li>
        </ul>
      </div>

      <p style="margin-top: 2rem;"><a href="/pages/projects.html">&larr; Back to Projects</a></p>

    </div>
  </div>
</section>
