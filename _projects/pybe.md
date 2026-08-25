---
layout: default
title: PyBe
page_title: PyBe — Python Tutor for Human Thinkers
parent: Products
order: 8
---

<div class="initiative-page-hero product-page-hero">
  <a href="{{ site.baseurl }}/products/" class="initiative-back"><i class="ph ph-arrow-left"></i> Products</a>
  <p class="story-label"><i class="ph ph-code"></i> Products</p>
  <h1 class="initiative-page-h">PyBe</h1>
</div>

{% include page-quote.html %}

<div class="product-page-meta">
  <span class="product-page-status">In Development</span>
</div>

<p class="product-page-tagline"><em>Not just code — conversation.<br>PyBe teaches machines in the language humans already know.</em></p>

<div class="product-page-section">
  <h2>The Problem</h2>
  <p>Most programming courses begin with syntax and hope reasoning follows. Learners memorise constructs, solve isolated exercises, and then stall the moment a problem arrives without a topic label attached to it. The gap is rarely Python itself — it is the step before Python: reading a situation, finding the problem inside it, and working out what kind of computation that situation actually calls for. That step tends to go untaught and unassessed, because the finished program is the only thing anyone ever looks at.</p>
</div>

<div class="product-page-section">
  <h2>What We Built</h2>
  <p>PyBe opens each session with a scenario rather than a syntax topic. Learners are guided to understand the situation, identify the underlying problem, build an abstraction, and only then express that reasoning in Python. The prototype is an interactive environment where learners explore scenarios, work through structured sessions, and receive feedback on their responses as they go. It keeps track of progress, concept mastery, misconceptions, prompt maturity and reflections — so the evidence of learning is the thinking, not only the correctness of the final program.</p>
  <p>The learning and evaluation mechanisms are rule-based and run locally, with no external AI services or API keys involved. That keeps the prototype light to run, and leaves a clear place for large language models, retrieval-augmented generation and richer feedback to be added as the platform matures.</p>
  <p>The shift underneath all of this is from code-first to reasoning-first: helping a learner understand <em>why</em> a particular computational construct fits before asking them to work out <em>how</em> to implement it.</p>
</div>

<a href="https://github.com/vicharanashala/pybe" target="_blank" rel="noopener" class="product-github-card">
  <i class="ph ph-github-logo"></i>
  <span>View source on GitHub ↗</span>
</a>
