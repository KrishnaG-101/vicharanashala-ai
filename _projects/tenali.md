---
layout: default
title: Tenali
page_title: Tenali — Learning Numeracy Through Play
parent: Products
order: 9
permalink: /projects/tenali/
quote: "Wit sharper than any sword."
quote_author: "Said of Tenali Raman"
---

<style>
  /* Scoped mobile tightening — match Vibe pattern */
  @media (max-width: 600px) {
    .page-content .wrapper hr { margin: 1.4rem 0; }
    .page-content .wrapper h2 { margin-top: 1.3rem; }
    .page-content .wrapper .tnl-modes { grid-template-columns: 1fr; }
    .page-content .wrapper .shot-carousel { margin: 1rem 0 1.2rem; }
    .page-content .wrapper .stat-row { gap: 1.5rem; padding: 1.2rem 0; }
    .page-content .wrapper .stat .stat-number { font-size: 1.6rem; }
  }
</style>

<div class="initiative-page-hero product-page-hero">
  <a href="{{ site.baseurl }}/products/" class="initiative-back"><i class="ph ph-arrow-left"></i> Products</a>
  <p class="story-label"><i class="ph ph-puzzle-piece"></i> Products</p>
  <h1 class="initiative-page-h">Tenali</h1>
</div>

{% include page-quote.html %}

<div class="product-page-meta">
  <span class="product-page-status">Deployed</span>
  <a href="https://tenali.fun" target="_blank" rel="noopener" class="product-try-link">Try it now ↗</a>
</div>

<p class="product-page-tagline">Adaptive math practice with 69 puzzle types, live multiplayer, and step-by-step explanations.</p>

---

## **About**

**Tenali** is named after the legendary **Tenali Raman** — the witty Indian scholar who outwitted entire courts with logic, not just facts. The platform sits on the same idea: math isn't memorised, it's *outwitted*.

Every question is calibrated to the learner — the next one lands where the last one left you.

Tenali covers foundational numeracy through to algebra in a game-like structure that keeps learners invested. Live and free at <a href="https://tenali.fun" target="_blank" rel="noopener">tenali.fun</a>.

**Why it works:** every question is generated on the fly from 91+ topics — arithmetic, geometry, algebra, calculus, vocab, GK — and there is no question database. Practice is infinite, never repeats, and the engine chooses the next question based on what the learner just showed they know. Difficulty isn't a setting; it's a per-learner trajectory.

A learner moves through four stages every session:

<div class="tnl-marquee tnl-marquee--4" id="tnl-workflow-marquee">
  <div class="tnl-marquee-track" id="tnl-workflow-track">
    <div class="audience-card">
      <i class="ph ph-globe audience-card-icon"></i>
      <div class="audience-card-title">1 · Open</div>
      <p class="audience-card-desc">Land on the home grid at tenali.fun — 90+ colorful topic cards. Guest mode works fully; JWT login is optional.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-target audience-card-icon"></i>
      <div class="audience-card-title">2 · Pick</div>
      <p class="audience-card-desc">Choose a mode: Goal Practice, Battle Arena, Detective Agency, Guided Journey, Random Mix, Custom Lesson, or a topic card.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-play audience-card-icon"></i>
      <div class="audience-card-title">3 · Play</div>
      <p class="audience-card-desc">20 adaptive questions. Correct bumps adaptScore; wrong drops it. Tap "Solve" at any time for a step-by-step walkthrough.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-trophy audience-card-icon"></i>
      <div class="audience-card-title">4 · Earn</div>
      <p class="audience-card-desc">Coins, XP, streak, badges. Progress saved in MongoDB — pick up tomorrow from where you stopped.</p>
    </div>
  </div>
</div>

<script>
(function() {
  var track = document.getElementById('tnl-workflow-track');
  if (!track) return;
  var reduceMotion = window.matchMedia && window.matchMedia('(prefers-reduced-motion: reduce)').matches;

  // Clone for seamless RTL loop
  var originals = Array.prototype.slice.call(track.children);
  originals.forEach(function(card) { track.appendChild(card.cloneNode(true)); });

  var halfWidth = track.scrollWidth / 2;
  var position = 0;                    // start at left edge
  var velocity = reduceMotion ? 0 : 0.4;
  var paused = false;

  function apply() { track.style.transform = 'translate3d(' + position + 'px, 0, 0)'; }

  function frame() {
    if (!paused && velocity !== 0) {
      position -= velocity;            // move LEFT (RTL)
      if (-position >= halfWidth) position += halfWidth; // wrap
      apply();
    }
    requestAnimationFrame(frame);
  }
  apply();
  requestAnimationFrame(frame);

  var marquee = track.parentElement;
  if (marquee) {
    marquee.addEventListener('mouseenter', function() { paused = true; });
    marquee.addEventListener('mouseleave', function() { paused = false; });
  }
})();
</script>

<img src="{{ site.baseurl }}/assets/images/tenali/home-grid.png" alt="Tenali home grid — 90+ topic cards color-coded by domain" loading="lazy" style="width:100%; border:1px solid #e2e2de; border-radius:6px; margin-top:1.5rem;">

---

## **The Problem**

Math anxiety starts early and compounds. Most platforms gamify trivia — points, streaks, badges — without asking the real question: *is the next question the right one for this learner right now?*

---

## **What We Built**

Pick a topic, get a question; the next one is calibrated to what you just showed you know. One engine runs across all 91+ puzzle topics — arithmetic, geometry, algebra, calculus, vocab, GK.

<div class="shot-carousel" id="tenali-shot-carousel">
  <div class="shot-carousel-viewport">
<div class="shot-slide active">
    <img src="{{ site.baseurl }}/assets/images/tenali/home-grid.png" alt="Tenali home grid">
    <figcaption>Home grid — 90+ topics, color-coded by domain.</figcaption>
  </div>
  <div class="shot-slide">
    <img src="{{ site.baseurl }}/assets/images/tenali/goal-practice.png" alt="Tenali goal practice — Tables Desk">
    <figcaption>Goal practice — pick a target score, hit it before time runs out.</figcaption>
  </div>
  <div class="shot-slide">
    <img src="{{ site.baseurl }}/assets/images/tenali/solve-explanation.png" alt="Tenali Tatsavit — Fit the Line">
    <figcaption>Tatsavit — explore slope and intercept by feel.</figcaption>
  </div>
  <div class="shot-slide">
    <img src="{{ site.baseurl }}/assets/images/tenali/battle-arena.png" alt="Tenali Battle Arena — live 1v1 duel">
    <figcaption>Battle Arena — live 1v1 fastest-finger duels.</figcaption>
  </div>
  <div class="shot-slide">
    <img src="{{ site.baseurl }}/assets/images/tenali/detective-agency.png" alt="Tenali Detective Agency — chained mystery">
    <figcaption>Detective Agency — chained clues, procedurally generated.</figcaption>
  </div>
  <div class="shot-slide">
    <img src="{{ site.baseurl }}/assets/images/tenali/guided-journey.png" alt="Tenali Guided Learning Journey">
    <figcaption>Guided Journey — next concept unlocks only after mastery.</figcaption>
  </div>
    <button class="shot-carousel-arrow shot-carousel-prev" aria-label="Previous screen"><i class="ph ph-caret-left"></i></button>
    <button class="shot-carousel-arrow shot-carousel-next" aria-label="Next screen"><i class="ph ph-caret-right"></i></button>
  </div>
  <div class="shot-carousel-nav">
    <button class="shot-carousel-dot active" data-index="0" aria-label="Screen 1"></button>
    <button class="shot-carousel-dot" data-index="1" aria-label="Screen 2"></button>
    <button class="shot-carousel-dot" data-index="2" aria-label="Screen 3"></button>
    <button class="shot-carousel-dot" data-index="3" aria-label="Screen 4"></button>
    <button class="shot-carousel-dot" data-index="4" aria-label="Screen 5"></button>
    <button class="shot-carousel-dot" data-index="5" aria-label="Screen 6"></button>
  </div>
</div>

<script>
(function() {
  var root = document.getElementById('tenali-shot-carousel');
  if (!root) return;
  var slides = root.querySelectorAll('.shot-slide');
  var dots = root.querySelectorAll('.shot-carousel-dot');
  var prevBtn = root.querySelector('.shot-carousel-prev');
  var nextBtn = root.querySelector('.shot-carousel-next');
  var current = 0;
  var timer;
  function goTo(i) {
    slides[current].classList.remove('active');
    dots[current].classList.remove('active');
    current = (i + slides.length) % slides.length;
    slides[current].classList.add('active');
    dots[current].classList.add('active');
  }
  dots.forEach(function(d, i) { d.addEventListener('click', function() { clearInterval(timer); goTo(i); timer = setInterval(function(){goTo(current+1);}, 4500); }); });
  if (prevBtn) prevBtn.addEventListener('click', function() { clearInterval(timer); goTo(current - 1); timer = setInterval(function(){goTo(current+1);}, 4500); });
  if (nextBtn) nextBtn.addEventListener('click', function() { clearInterval(timer); goTo(current + 1); timer = setInterval(function(){goTo(current+1);}, 4500); });
  timer = setInterval(function() { goTo(current + 1); }, 4500);
})();
</script>

---

## **Key Features**

<div class="tnl-marquee">
  <button class="tnl-marquee-arrow tnl-marquee-arrow--left" id="tnl-features-left" aria-label="Scroll features left"><i class="ph ph-caret-left"></i></button>
  <button class="tnl-marquee-arrow tnl-marquee-arrow--right" id="tnl-features-right" aria-label="Scroll features right"><i class="ph ph-caret-right"></i></button>
  <div class="tnl-marquee-track" id="tnl-features-track">
    <div class="audience-card">
      <i class="ph ph-chart-line-up audience-card-icon"></i>
      <div class="audience-card-title">Adaptive Difficulty</div>
      <p class="audience-card-desc">A float adaptScore (0–3) shifts with every answer. Maps to bands easy → medium → hard → extrahard.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-swords audience-card-icon"></i>
      <div class="audience-card-title">Battle Arena</div>
      <p class="audience-card-desc">Live 1v1 fastest-finger duels over Socket.IO. Same question, first correct answer wins.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-magnifying-glass audience-card-icon"></i>
      <div class="audience-card-title">Detective Agency</div>
      <p class="audience-card-desc">Chain of math clues; solving one unlocks the next. Hundreds of procedurally generated cases.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-graduation-cap audience-card-icon"></i>
      <div class="audience-card-title">Guided Journey</div>
      <p class="audience-card-desc">Linear curriculum with concept checkpoints. Server enforces progression: locked → blue → bronze → silver → gold.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-flask audience-card-icon"></i>
      <div class="audience-card-title">Concept Lab</div>
      <p class="audience-card-desc">5-stage mastery loop — Predict → Grid → Guided → Independent → Review.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-puzzle-piece audience-card-icon"></i>
      <div class="audience-card-title">Spaced Repetition</div>
      <p class="audience-card-desc">Recently-missed questions are promoted back into rotation by Bayesian Knowledge Tracing.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-shield-check audience-card-icon"></i>
      <div class="audience-card-title">Proctoring</div>
      <p class="audience-card-desc">Optional exam-mode supervision via face-api.js — focus score, tab switches, look-aways.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-trophy audience-card-icon"></i>
      <div class="audience-card-title">Gamification</div>
      <p class="audience-card-desc">Coins, XP, streak, pinned badges, album-style Collections. Persisted across sessions.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-shuffle audience-card-icon"></i>
      <div class="audience-card-title">Random Mix &amp; Custom Lesson</div>
      <p class="audience-card-desc">Random Mix pulls from your weakest areas. Custom Lesson lets you pick exactly which topics and counts.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-terminal-window audience-card-icon"></i>
      <div class="audience-card-title">Code Playground</div>
      <p class="audience-card-desc">Run code in 50+ languages. Python-Tutor-style visualizer with code + arrow + memory boxes.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-translate audience-card-icon"></i>
      <div class="audience-card-title">i18n &amp; RTL</div>
      <p class="audience-card-desc">Built-in locale switching for multi-language classrooms, including right-to-left scripts.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-keyboard audience-card-icon"></i>
      <div class="audience-card-title">Accessibility</div>
      <p class="audience-card-desc">Keyboard navigation, ARIA roles, high-contrast toggle, reduced-motion friendly animations.</p>
    </div>
  </div>
</div>

<script>
(function() {
  var track = document.getElementById('tnl-features-track');
  var leftBtn = document.getElementById('tnl-features-left');
  var rightBtn = document.getElementById('tnl-features-right');
  if (!track) return;

  var reduceMotion = window.matchMedia && window.matchMedia('(prefers-reduced-motion: reduce)').matches;

  // Clone once for seamless looping
  var originals = Array.prototype.slice.call(track.children);
  originals.forEach(function(card) { track.appendChild(card.cloneNode(true)); });

  var halfWidth = track.scrollWidth / 2; // track contains originals + clones
  var position = 0;            // current translateX (negative = scrolled left)
  var velocity = reduceMotion ? 0 : 0.4; // px per frame (≈24px/s @60fps); 0 if reduced motion
  var paused = false;
  var resumeTimer = null;

  function apply() { track.style.transform = 'translate3d(' + position + 'px, 0, 0)'; }

  function frame() {
    if (!paused && velocity !== 0) {
      position -= velocity;
      // wrap seamlessly: when we've scrolled one full half, snap back
      if (-position >= halfWidth) position += halfWidth;
      apply();
    }
    requestAnimationFrame(frame);
  }
  requestAnimationFrame(frame);

  function cardStep() {
    var card = track.querySelector('.audience-card');
    return card ? card.getBoundingClientRect().width + 16 : 280;
  }

  function nudge(direction) {
    position += direction * cardStep(); // direction: -1 = scroll left, +1 = scroll right
    if (-position >= halfWidth) position += halfWidth;
    if (position > 0) position -= halfWidth;
    apply();
    paused = true;
    if (resumeTimer) clearTimeout(resumeTimer);
    resumeTimer = setTimeout(function() { paused = false; }, 1800);
  }

  if (leftBtn)  leftBtn.addEventListener('click',  function() { nudge(-1); });
  if (rightBtn) rightBtn.addEventListener('click', function() { nudge(1); });

  // Hover the marquee → pause
  var marquee = track.parentElement;
  if (marquee) {
    marquee.addEventListener('mouseenter', function() { paused = true; });
    marquee.addEventListener('mouseleave', function() { paused = false; });
  }
})();
</script>

---

## **Eight Modes at a Glance**

Eight ways to play. Same engine, different shape on top.

<div class="tnl-marquee tnl-marquee--2" id="tnl-modes-marquee">
  <button class="tnl-marquee-arrow tnl-marquee-arrow--left" id="tnl-modes-left" aria-label="Scroll modes left"><i class="ph ph-caret-left"></i></button>
  <button class="tnl-marquee-arrow tnl-marquee-arrow--right" id="tnl-modes-right" aria-label="Scroll modes right"><i class="ph ph-caret-right"></i></button>
  <div class="tnl-marquee-track" id="tnl-modes-track">
    <div class="audience-card">
      <i class="ph ph-target audience-card-icon"></i>
      <div class="audience-card-title">Goal Practice</div>
      <p class="audience-card-desc">Pick a target score on a topic and chase it. The engine adapts as you go.</p>
      <span class="scenario-stat"><i class="ph ph-trend-up"></i> Hit your target or beat it</span>
    </div>
    <div class="audience-card">
      <i class="ph ph-swords audience-card-icon"></i>
      <div class="audience-card-title">Battle Arena</div>
      <p class="audience-card-desc">Two players, one question, first correct answer wins. Streaks drive matchmaking.</p>
      <span class="scenario-stat"><i class="ph ph-globe"></i> Multiplayer over Socket.IO</span>
    </div>
    <div class="audience-card">
      <i class="ph ph-magnifying-glass audience-card-icon"></i>
      <div class="audience-card-title">Detective Agency</div>
      <p class="audience-card-desc">Chained math clues; solving one unlocks the next. Hundreds of cases, procedurally generated.</p>
      <span class="scenario-stat"><i class="ph ph-path"></i> Chained clue progression</span>
    </div>
    <div class="audience-card">
      <i class="ph ph-lightbulb audience-card-icon"></i>
      <div class="audience-card-title">Math Riddles</div>
      <p class="audience-card-desc">Find the hidden rule. 48 riddles — find-rule, sequence, logic, image.</p>
      <span class="scenario-stat"><i class="ph ph-shuffle"></i> 48 hand-authored riddles</span>
    </div>
    <div class="audience-card">
      <i class="ph ph-graduation-cap audience-card-icon"></i>
      <div class="audience-card-title">Guided Learning Journey</div>
      <p class="audience-card-desc">Linear curriculum with concept checkpoints. Next concept unlocks only after mastery.</p>
      <span class="scenario-stat"><i class="ph ph-lock-key"></i> Server-enforced progression</span>
    </div>
    <div class="audience-card">
      <i class="ph ph-shuffle audience-card-icon"></i>
      <div class="audience-card-title">Random Mix</div>
      <p class="audience-card-desc">Pulls from wherever your adaptScore is lowest.</p>
      <span class="scenario-stat"><i class="ph ph-chart-line-up"></i> Targets weak areas</span>
    </div>
    <div class="audience-card">
      <i class="ph ph-sliders audience-card-icon"></i>
      <div class="audience-card-title">Custom Lesson</div>
      <p class="audience-card-desc">Hand-pick topics and question counts.</p>
      <span class="scenario-stat"><i class="ph ph-pencil"></i> You decide the mix</span>
    </div>
    <div class="audience-card">
      <i class="ph ph-function audience-card-icon"></i>
      <div class="audience-card-title">Linear Algebra Lab</div>
      <p class="audience-card-desc">56 missions across 6 modules — ratios, coordinate geometry, linear transforms, matrices, determinants, PageRank.</p>
      <span class="scenario-stat"><i class="ph ph-chart-network"></i> 6 modules · 4 difficulty bands</span>
    </div>
  </div>
</div>

<script>
(function() {
  var track = document.getElementById('tnl-modes-track');
  var leftBtn = document.getElementById('tnl-modes-left');
  var rightBtn = document.getElementById('tnl-modes-right');
  if (!track) return;
  var reduceMotion = window.matchMedia && window.matchMedia('(prefers-reduced-motion: reduce)').matches;

  // Clone for seamless RTL loop
  var originals = Array.prototype.slice.call(track.children);
  originals.forEach(function(card) { track.appendChild(card.cloneNode(true)); });

  var halfWidth = track.scrollWidth / 2;
  var position = 0;
  var velocity = reduceMotion ? 0 : 0.4;
  var paused = false;
  var resumeTimer = null;

  function apply() { track.style.transform = 'translate3d(' + position + 'px, 0, 0)'; }

  function frame() {
    if (!paused && velocity !== 0) {
      position -= velocity; // RTL
      if (-position >= halfWidth) position += halfWidth;
      apply();
    }
    requestAnimationFrame(frame);
  }
  apply();
  requestAnimationFrame(frame);

  function cardStep() {
    var card = track.querySelector('.audience-card');
    return card ? card.getBoundingClientRect().width + 16 : 320;
  }

  function nudge(direction) {
    position += direction * cardStep(); // direction: -1 = scroll left, +1 = scroll right
    if (-position >= halfWidth) position += halfWidth;
    if (position > 0) position -= halfWidth;
    apply();
    paused = true;
    if (resumeTimer) clearTimeout(resumeTimer);
    resumeTimer = setTimeout(function() { paused = false; }, 1800);
  }

  if (leftBtn)  leftBtn.addEventListener('click',  function() { nudge(-1); });
  if (rightBtn) rightBtn.addEventListener('click', function() { nudge(1); });

  var marquee = track.parentElement;
  if (marquee) {
    marquee.addEventListener('mouseenter', function() { paused = true; });
    marquee.addEventListener('mouseleave', function() { paused = false; });
  }
})();
</script>

---

## **By the Numbers**

<div class="stat-row will-animate" id="tenali-stat-row">
  <div class="stat"><span class="stat-number">69</span><span class="stat-label">Puzzle Families</span></div>
  <div class="stat"><span class="stat-number">91+</span><span class="stat-label">Topics &amp; Apps</span></div>
  <div class="stat"><span class="stat-number">7,662</span><span class="stat-label">Vocabulary Words</span></div>
  <div class="stat"><span class="stat-number">991</span><span class="stat-label">GK Questions</span></div>
  <div class="stat"><span class="stat-number">25+</span><span class="stat-label">Open-Source Contributors</span></div>
</div>

<script>
(function() {
  var row = document.getElementById('tenali-stat-row');
  if (!row) return;
  var reduceMotion = window.matchMedia && window.matchMedia('(prefers-reduced-motion: reduce)').matches;
  function countUp(el) {
    var text = el.textContent.trim();
    var match = text.match(/^(\D*)([\d,]+)(\D*)$/);
    if (!match) return;
    var prefix = match[1], target = parseInt(match[2].replace(/,/g, ''), 10), suffix = match[3];
    if (isNaN(target)) return;
    var duration = 900, start = null;
    function step(ts) {
      if (!start) start = ts;
      var progress = Math.min((ts - start) / duration, 1);
      var eased = 1 - Math.pow(1 - progress, 3);
      el.textContent = prefix + Math.round(target * eased).toLocaleString('en-US') + suffix;
      if (progress < 1) requestAnimationFrame(step);
      else el.textContent = prefix + target.toLocaleString('en-US') + suffix;
    }
    requestAnimationFrame(step);
  }
  function reveal() {
    row.classList.add('in-view');
    if (!reduceMotion) {
      row.querySelectorAll('.stat-number').forEach(countUp);
    }
  }
  if (!('IntersectionObserver' in window)) { reveal(); return; }
  var observer = new IntersectionObserver(function(entries) {
    entries.forEach(function(entry) {
      if (entry.isIntersecting) { reveal(); observer.unobserve(row); }
    });
  }, { threshold: 0.3 });
  observer.observe(row);
})();
</script>

---

## **Contributors**

<div class="contributor-list">
  <span class="contributor-chip">S. R. S. Iyengar</span>
  <span class="contributor-chip">Jinal Gupta</span>
  <span class="contributor-chip">Mudit Agrawal</span>
  <span class="contributor-chip">Lakshmi Varshini Nandula</span>
  <span class="contributor-chip">Sameer Mishra</span>
  <span class="contributor-chip">Vaibhav Satish</span>
  <span class="contributor-chip">Diptosubhro Datta</span>
  <span class="contributor-chip">Ritish Karmakar</span>
  <span class="contributor-chip">Ahana Banerjee</span>
  <span class="contributor-chip">K C Dharshan</span>
</div>

<a class="contributor-more" href="https://github.com/vicharanashala/tenali/graphs/contributors" target="_blank" rel="noopener">See the full list on GitHub <i class="ph ph-arrow-right"></i></a>

---

Step into the rhythm of math at [tenali.fun](https://tenali.fun){:target="_blank"}.

<a href="https://github.com/vicharanashala/tenali" target="_blank" rel="noopener" class="product-github-card">
  <i class="ph ph-github-logo"></i>
  <span>View source on GitHub ↗</span>
</a>
