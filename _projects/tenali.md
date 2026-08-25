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
    .page-content .wrapper .tnl-demo { padding: 1rem; }
    .page-content .wrapper .tnl-adapter { height: 38px; }
    .page-content .wrapper .tnl-modes { grid-template-columns: 1fr; }
    .page-content .wrapper .tnl-linear-modules { grid-template-columns: repeat(2, 1fr); }
    .page-content .wrapper .tnl-linear-feature-row { grid-template-columns: 1fr; }
    .page-content .wrapper .tnl-proctor-grid { grid-template-columns: 1fr; }
    .page-content .wrapper .tnl-proctor-feature-row { grid-template-columns: 1fr; }
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

<p class="product-page-tagline">Adaptive math quiz platform with 69 algorithmically generated puzzle types, real-time multiplayer, and step-by-step explanations. Where numbers lose their menace.</p>

---

## **The Adaptive Engine**

Tenali's defining feature is the difficulty engine that sits underneath every question. Watch it work — the score shifts with every answer, the band marker moves with it, and the next question is calibrated to wherever you are.

<div class="tnl-demo" id="tnl-demo">
  <div class="tnl-demo-row">
    <div class="tnl-question-card">
      <div class="tnl-question-meta">Q 4 · LINEAR EQUATIONS</div>
      <div class="tnl-question-text" id="tnl-qtext">Solve for x:  3x − 7 = 5x + 11</div>
      <div class="tnl-input-row">
        <input type="text" class="tnl-input" id="tnl-input" value="x = −9" readonly>
        <button class="tnl-btn" id="tnl-check">Check</button>
      </div>
    </div>
    <div class="tnl-adapter-wrap">
      <div class="tnl-adapter-label">AdaptScore <span id="tnl-score">1.20</span></div>
      <div class="tnl-adapter">
        <div class="tnl-adapter-band" data-band="0"></div>
        <div class="tnl-adapter-band" data-band="1"></div>
        <div class="tnl-adapter-band" data-band="2"></div>
        <div class="tnl-adapter-band" data-band="3"></div>
        <div class="tnl-adapter-marker" id="tnl-marker"></div>
      </div>
      <div class="tnl-adapter-names">
        <span>easy</span><span>medium</span><span>hard</span><span>✦</span>
      </div>
      <div class="tnl-feed" id="tnl-feed"></div>
    </div>
  </div>
  <div class="tnl-demo-caption" id="tnl-caption">Watch how the score shifts with every answer.</div>
</div>

<script>
(function() {
  var root = document.getElementById('tnl-demo');
  if (!root) return;
  var marker = document.getElementById('tnl-marker');
  var scoreEl = document.getElementById('tnl-score');
  var feed = document.getElementById('tnl-feed');
  var caption = document.getElementById('tnl-caption');
  var input = document.getElementById('tnl-input');
  var btn = document.getElementById('tnl-check');
  var qtext = document.getElementById('tnl-qtext');
  var bands = root.querySelectorAll('.tnl-adapter-band');
  var reduceMotion = window.matchMedia && window.matchMedia('(prefers-reduced-motion: reduce)').matches;

  var score = 1.20;
  var beat = 0;

  function bandFor(s) {
    if (s < 0.75) return 0;
    if (s < 1.5)  return 1;
    if (s < 2.25) return 2;
    return 3;
  }

  function positionMarker() {
    var pct = Math.max(0, Math.min(3, score)) / 3 * 100;
    marker.style.left = 'calc(' + pct + '% - 7px)';
    bands.forEach(function(b) { b.classList.remove('is-active'); });
    bands[bandFor(score)].classList.add('is-active');
    scoreEl.textContent = score.toFixed(2);
  }

  function showFeed(text, good) {
    if (reduceMotion) return;
    feed.textContent = text;
    feed.className = 'tnl-feed ' + (good ? 'is-good' : 'is-bad') + ' is-visible';
    setTimeout(function() { feed.classList.remove('is-visible'); }, 1400);
  }

  function tick() {
    if (reduceMotion) return;
    scoreEl.classList.remove('is-tick');
    void scoreEl.offsetWidth;
    scoreEl.classList.add('is-tick');
  }

  function applyDelta(d, text, good, nextScore) {
    score = Math.max(0, Math.min(3, nextScore));
    positionMarker();
    tick();
    showFeed(text, good);
  }

  positionMarker();

  btn.addEventListener('click', function() {
    beat++;
    if (beat === 1) {
      input.value = 'x = 4';
      input.classList.add('is-wrong');
      applyDelta(-0.55, '−0.55', false, 0.65);
      caption.textContent = 'Wrong answer — score drops, band shifts back.';
    } else if (beat === 2) {
      input.value = 'x = −9';
      input.classList.remove('is-wrong');
      input.classList.add('is-right');
      applyDelta(0.95, '+0.95', true, 1.60);
      caption.textContent = 'Correct — score climbs, next question is harder.';
    } else if (beat === 3) {
      qtext.textContent = 'Solve:  x² − 5x + 6 = 0';
      input.value = 'x = 2, 3';
      input.classList.remove('is-right');
      applyDelta(1.05, '+1.05', true, 2.65);
      caption.textContent = 'Easy in. Extra-hard out. Every question calibrated to you.';
    } else {
      // loop: subtle drift
      var drift = (Math.random() - 0.5) * 0.4;
      applyDelta(drift, (drift > 0 ? '+' : '') + drift.toFixed(2), drift > 0, Math.max(0.4, Math.min(2.9, score + drift)));
    }
  });

  // Auto-play once on load (skip if reduced motion)
  if (!reduceMotion) {
    setTimeout(function() { btn.click(); }, 1400);
    setTimeout(function() { btn.click(); }, 3200);
    setTimeout(function() { btn.click(); }, 5000);
    setInterval(function() {
      if (beat >= 3) btn.click();
    }, 6500);
  }
})();
</script>

---

## **About**

<div class="split-media">
<p>Tenali covers the full journey from foundational numeracy through to algebra, using a game-like structure that keeps learners invested. Every question is generated on the fly — there is no question database — so practice is infinite and never repeats. The platform is live and free to use at <a href="https://tenali.fun" target="_blank" rel="noopener">tenali.fun</a>, with one Node process serving the React app, the puzzle APIs, the JWT auth, the Socket.IO Battle Arena, and the multi-language code playground.</p>

<img src="{{ site.baseurl }}/assets/images/tenali/home-grid.png" alt="Tenali home grid — 90+ topic cards color-coded by domain" loading="lazy" style="width:100%; border:1px solid #e2e2de; border-radius:6px;">
</div>

---

## **The Problem**

In most classrooms, math anxiety starts early and compounds. Worksheets pile up, drills repeat, and the gap between what a learner can do and what they believe they can do widens. The platforms that try to fix this usually gamify trivia — points, streaks, badges — without addressing the underlying question: *is the next question the right one for this learner right now?*

---

## **What We Built**

A math learning surface where the difficulty adjusts to the learner, not the other way around. Pick a topic, get a question; answer it, and the next one is calibrated to what you just showed you know. The same engine runs across all 91+ puzzle topics — arithmetic, geometry, algebra, calculus, even vocab and GK — so practice stays coherent no matter where a learner starts.

<div class="shot-carousel" id="tenali-shot-carousel">
  <div class="shot-carousel-viewport">
    <div class="shot-slide active">
      <img src="{{ site.baseurl }}/assets/images/tenali/home-grid.png" alt="Tenali home grid">
      <figcaption>Home grid — 90+ topics color-coded by domain (blue arithmetic, green geometry, purple algebra, orange games).</figcaption>
    </div>
    <div class="shot-slide">
      <img src="{{ site.baseurl }}/assets/images/tenali/goal-practice.png" alt="Tenali goal practice — Tables Desk">
      <figcaption>Goal practice — pick a target score, hit it before the session ends.</figcaption>
    </div>
    <div class="shot-slide">
      <img src="{{ site.baseurl }}/assets/images/tenali/solve-explanation.png" alt="Tenali Tatsavit — Fit the Line">
      <figcaption>Tatsavit — interactive line-fitter for exploring slope and intercept by feel.</figcaption>
    </div>
    <div class="shot-slide">
      <img src="{{ site.baseurl }}/assets/images/tenali/battle-arena.png" alt="Tenali Battle Arena — live 1v1 duel">
      <figcaption>Battle Arena — live 1-vs-1 fastest-finger duels over Socket.IO.</figcaption>
    </div>
    <div class="shot-slide">
      <img src="{{ site.baseurl }}/assets/images/tenali/detective-agency.png" alt="Tenali Detective Agency — chained mystery">
      <figcaption>Detective Agency — story-driven mystery puzzles with chained clues.</figcaption>
    </div>
    <div class="shot-slide">
      <img src="{{ site.baseurl }}/assets/images/tenali/guided-journey.png" alt="Tenali Guided Learning Journey">
      <figcaption>Guided Journey — linear curriculum; the next concept unlocks only after the previous is mastered.</figcaption>
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

## **Linear Algebra Lab**

A curated 56-mission journey through linear algebra — from ratios on a plane to matrix factorisation and PageRank — built on Tenali's adaptive engine. Six modules, four difficulty bands each, every question anchored to a real-life story.

<div class="tnl-linear">
  <div class="tnl-linear-band">
    <span class="tnl-linear-label"><i class="ph ph-function"></i> LINEAR ALGEBRA LAB</span>
    <h2 class="tnl-linear-h">56 missions. 6 modules. One coherent journey.</h2>
    <p class="tnl-linear-p">From <em>Ram and Lakshman's piggy-bank points</em> to <em>how Google ranks pages</em>. Each question is a story; the math is what you take away.</p>
  </div>

  <div class="tnl-linear-canvas" id="tnl-linear-canvas">
    <div class="tnl-linear-canvas-meta">
      <span id="tnl-linear-equation">y = 2x</span>
      <span>·</span>
      <span id="tnl-linear-slope">slope = 2</span>
    </div>
    <svg viewBox="0 0 500 280" xmlns="http://www.w3.org/2000/svg" id="tnl-linear-svg">
      <defs>
        <marker id="tnl-arr" markerWidth="8" markerHeight="8" refX="6" refY="3" orient="auto"><path d="M0,0 L6,3 L0,6 Z" fill="#767676"/></marker>
      </defs>
      <line x1="40" y1="240" x2="480" y2="240" stroke="#767676" stroke-width="1" marker-end="url(#tnl-arr)"/>
      <line x1="40" y1="240" x2="40" y2="20"  stroke="#767676" stroke-width="1" marker-end="url(#tnl-arr)"/>
      <text x="468" y="258" fill="#767676" font-size="12" font-family="Inter">x</text>
      <text x="50"  y="32"  fill="#767676" font-size="12" font-family="Inter">y</text>
      <line x1="40"  y1="180" x2="480" y2="180" stroke="#e2e2de" stroke-width="0.5" stroke-dasharray="2,4"/>
      <line x1="40"  y1="120" x2="480" y2="120" stroke="#e2e2de" stroke-width="0.5" stroke-dasharray="2,4"/>
      <line x1="40"  y1="60"  x2="480" y2="60"  stroke="#e2e2de" stroke-width="0.5" stroke-dasharray="2,4"/>
      <line x1="140" y1="240" x2="140" y2="20"  stroke="#e2e2de" stroke-width="0.5" stroke-dasharray="2,4"/>
      <line x1="240" y1="240" x2="240" y2="20"  stroke="#e2e2de" stroke-width="0.5" stroke-dasharray="2,4"/>
      <line x1="340" y1="240" x2="340" y2="20"  stroke="#e2e2de" stroke-width="0.5" stroke-dasharray="2,4"/>
      <line x1="440" y1="240" x2="440" y2="20"  stroke="#e2e2de" stroke-width="0.5" stroke-dasharray="2,4"/>
      <path id="tnl-linear-path" d="M 40 240 L 440 60" stroke="#e07020" stroke-width="2" fill="none" pathLength="100" stroke-dasharray="100" stroke-dashoffset="100"/>
      <g id="tnl-linear-dots"></g>
    </svg>
  </div>

  <div class="tnl-linear-modules">
    <div class="tnl-linear-module is-active" data-module="1" data-slope="2" data-label="y = 2x">
      <div class="tnl-linear-module-num">M1</div>
      <div class="tnl-linear-module-body">
        <div class="tnl-linear-module-title">Ratios &amp; Lines</div>
        <div class="tnl-linear-module-count">14 missions</div>
      </div>
    </div>
    <div class="tnl-linear-module" data-module="2" data-slope="1" data-label="y = x">
      <div class="tnl-linear-module-num">M2</div>
      <div class="tnl-linear-module-body">
        <div class="tnl-linear-module-title">Coordinate Geometry</div>
        <div class="tnl-linear-module-count">10 missions</div>
      </div>
    </div>
    <div class="tnl-linear-module" data-module="3" data-slope="0.5" data-label="y = 0.5x">
      <div class="tnl-linear-module-num">M3</div>
      <div class="tnl-linear-module-body">
        <div class="tnl-linear-module-title">Linear Transforms</div>
        <div class="tnl-linear-module-count">15 missions</div>
      </div>
    </div>
    <div class="tnl-linear-module" data-module="4" data-slope="-1" data-label="y = −x">
      <div class="tnl-linear-module-num">M4</div>
      <div class="tnl-linear-module-body">
        <div class="tnl-linear-module-title">Matrices</div>
        <div class="tnl-linear-module-count">9 missions</div>
      </div>
    </div>
    <div class="tnl-linear-module" data-module="5" data-slope="3" data-label="y = 3x">
      <div class="tnl-linear-module-num">M5</div>
      <div class="tnl-linear-module-body">
        <div class="tnl-linear-module-title">Determinants &amp; Inverses</div>
        <div class="tnl-linear-module-count">5 missions</div>
      </div>
    </div>
    <div class="tnl-linear-module" data-module="6" data-slope="-2" data-label="y = −2x">
      <div class="tnl-linear-module-num">M6</div>
      <div class="tnl-linear-module-body">
        <div class="tnl-linear-module-title">Recommenders &amp; PageRank</div>
        <div class="tnl-linear-module-count">6 missions</div>
      </div>
    </div>
  </div>

  <div class="tnl-linear-question">
    <div class="tnl-linear-question-meta">
      <span class="tnl-linear-pill">M1 · Q1.1</span>
      <span class="tnl-linear-qprogress">73% complete</span>
    </div>
    <div class="tnl-linear-progress"><div class="tnl-linear-progress-bar"></div></div>
    <div class="tnl-linear-story">"Ram's money is twice Lakshman's. If Lakshman has ₹10, how much does Ram have?"</div>
    <div class="tnl-linear-qtext">Find Ram's savings.</div>
    <div class="tnl-linear-sub">R = 2L · L = 10</div>
    <div class="tnl-linear-options">
      <div class="tnl-linear-option" data-correct="true">
        <span class="tnl-linear-letter">A</span>
        <span class="tnl-linear-opt-text">Twenty rupees amount</span>
        <span class="tnl-linear-mark">✓</span>
      </div>
      <div class="tnl-linear-option" data-correct="false">
        <span class="tnl-linear-letter">B</span>
        <span class="tnl-linear-opt-text">Same as Lakshman has</span>
      </div>
      <div class="tnl-linear-option" data-correct="false">
        <span class="tnl-linear-letter">C</span>
        <span class="tnl-linear-opt-text">Five rupees amount</span>
      </div>
      <div class="tnl-linear-option" data-correct="false">
        <span class="tnl-linear-letter">D</span>
        <span class="tnl-linear-opt-text">Thirty rupees amount</span>
      </div>
    </div>
  </div>

  <div class="tnl-linear-feature-row">
    <div class="audience-card">
      <i class="ph ph-book-open audience-card-icon"></i>
      <div class="audience-card-title">Real-life stories</div>
      <p class="audience-card-desc">Every question is anchored to a story — piggy banks, cricket squads, bakeries, factories. Math emerges from context.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-list-numbers audience-card-icon"></i>
      <div class="audience-card-title">Curated MCQs</div>
      <p class="audience-card-desc">56 missions across four difficulty bands — easy, medium, hard, real-life application. Each one hand-authored.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-chart-line-up audience-card-icon"></i>
      <div class="audience-card-title">Adaptive difficulty</div>
      <p class="audience-card-desc">Same engine as the rest of Tenali — your adaptScore drifts up and down with every correct / wrong answer.</p>
    </div>
  </div>
</div>

<script>
(function() {
  var canvas = document.getElementById('tnl-linear-canvas');
  if (!canvas) return;
  var path = document.getElementById('tnl-linear-path');
  var dotsG = document.getElementById('tnl-linear-dots');
  var eqLabel = document.getElementById('tnl-linear-equation');
  var slopeLabel = document.getElementById('tnl-linear-slope');
  var modules = document.querySelectorAll('.tnl-linear-module');
  var reduceMotion = window.matchMedia && window.matchMedia('(prefers-reduced-motion: reduce)').matches;

  function lineFor(slope) {
    // y goes up = y decreases in svg coords; origin (40, 240); x range 40..440
    var x1 = 40, x2 = 440;
    var y1 = 240 - slope * (x1 - 40);
    var y2 = 240 - slope * (x2 - 40);
    return { x1: x1, y1: y1, x2: x2, y2: y2, slope: slope };
  }

  function drawDots(line) {
    dotsG.innerHTML = '';
    var xs = [120, 200, 280, 360];
    xs.forEach(function(x) {
      var y = 240 - line.slope * (x - 40);
      if (y < 18 || y > 270) return;
      var c = document.createElementNS('http://www.w3.org/2000/svg', 'circle');
      c.setAttribute('cx', x);
      c.setAttribute('cy', y);
      c.setAttribute('r', 4);
      c.setAttribute('fill', '#e07020');
      dotsG.appendChild(c);
    });
  }

  function redraw(slope, label) {
    var line = lineFor(slope);
    eqLabel.textContent = label;
    slopeLabel.textContent = 'slope = ' + slope;
    path.setAttribute('d', 'M ' + line.x1 + ' ' + line.y1 + ' L ' + line.x2 + ' ' + line.y2);
    if (reduceMotion) {
      path.style.strokeDashoffset = 0;
      drawDots(line);
      return;
    }
    path.style.strokeDashoffset = 100;
    // restart animation
    void path.getBoundingClientRect();
    path.style.strokeDashoffset = 0;
    setTimeout(function() { drawDots(line); }, 350);
  }

  modules.forEach(function(m) {
    m.addEventListener('click', function() {
      modules.forEach(function(x) { x.classList.remove('is-active'); });
      m.classList.add('is-active');
      redraw(parseFloat(m.dataset.slope), m.dataset.label);
    });
  });

  // initial draw
  var first = document.querySelector('.tnl-linear-module.is-active');
  if (first) redraw(parseFloat(first.dataset.slope), first.dataset.label);

  // MCQ option click
  var options = document.querySelectorAll('.tnl-linear-option');
  options.forEach(function(opt) {
    opt.addEventListener('click', function() {
      if (opt.classList.contains('is-locked')) return;
      options.forEach(function(o) { o.classList.add('is-locked'); });
      options.forEach(function(o) {
        if (o.dataset.correct === 'true') o.classList.add('is-correct');
        else o.classList.add('is-faded');
      });
      opt.classList.add('is-correct', 'is-clicked');
      // ripple
      if (!reduceMotion) {
        var r = document.createElement('span');
        r.className = 'tnl-linear-ripple';
        opt.appendChild(r);
        setTimeout(function() { r.remove(); }, 700);
      }
    });
  });
})();
</script>

---

## **Key Features**

<div class="audience-grid">
  <div class="audience-card">
    <i class="ph ph-chart-line-up audience-card-icon"></i>
    <div class="audience-card-title">Adaptive Difficulty Engine</div>
    <p class="audience-card-desc">Each quiz instance maintains a float adaptScore (0 – 3). Correct answers add +0.15 to +0.5; wrong answers subtract −0.4 to −0.6. The score maps to bands easy → medium → hard → extrahard, which drives the difficulty parameter for every new question.</p>
  </div>
  <div class="audience-card">
    <i class="ph ph-swords audience-card-icon"></i>
    <div class="audience-card-title">Battle Arena</div>
    <p class="audience-card-desc">Live 1-vs-1 fastest-finger duels via Socket.IO. Two players see the same question; the first correct answer wins the round. Streak-based matchmaking.</p>
  </div>
  <div class="audience-card">
    <i class="ph ph-magnifying-glass audience-card-icon"></i>
    <div class="audience-card-title">Detective Agency</div>
    <p class="audience-card-desc">Story-driven mystery puzzles — each case is a chain of math clues; solving one unlocks the next. Hundreds of procedurally generated mysteries.</p>
  </div>
  <div class="audience-card">
    <i class="ph ph-lightbulb audience-card-icon"></i>
    <div class="audience-card-title">Solve-for-Explanation</div>
    <p class="audience-card-desc">Wrap any POST *-api/check call with { solve: true } and the server returns a step-by-step walkthrough from generateExplanation() — covers 50+ puzzle types.</p>
  </div>
  <div class="audience-card">
    <i class="ph ph-graduation-cap audience-card-icon"></i>
    <div class="audience-card-title">Guided Learning Journey</div>
    <p class="audience-card-desc">Linear curriculum with concept checkpoints. Server enforces progression via UserTopicProgress — locked → blue → bronze → silver → gold.</p>
  </div>
  <div class="audience-card">
    <i class="ph ph-flask audience-card-icon"></i>
    <div class="audience-card-title">Concept Lab</div>
    <p class="audience-card-desc">A 5-stage concept mastery loop — Predict → Grid → Guided → Independent → Review — for moving from intuition to fluency on a single concept.</p>
  </div>
  <div class="audience-card">
    <i class="ph ph-puzzle-piece audience-card-icon"></i>
    <div class="audience-card-title">Spaced Repetition</div>
    <p class="audience-card-desc">Recently-missed questions are promoted back into rotation by lib/spacingLadder.js, driven by Bayesian Knowledge Tracing (lib/bkt.js).</p>
  </div>
</div>

<div class="grid-extra-wrap" id="tenali-features-extra-wrap">
  <div class="audience-grid audience-grid--continued">
    <div class="audience-card">
      <i class="ph ph-trophy audience-card-icon"></i>
      <div class="audience-card-title">Gamification</div>
      <p class="audience-card-desc">Coins, XP, streak, pinned badges, album-style Collections. Earned on every correct answer; persisted in MongoDB for next time.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-shuffle audience-card-icon"></i>
      <div class="audience-card-title">Random Mix &amp; Custom Lesson</div>
      <p class="audience-card-desc">Random Mix pulls a question from your weakest areas. Custom Lesson lets you pick exactly which topics appear and how many of each.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-terminal-window audience-card-icon"></i>
      <div class="audience-card-title">Code Playground</div>
      <p class="audience-card-desc">Run code in 50+ languages via /api/playground2/run. Python-Tutor-style visualizer with code + arrow + memory boxes.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-translate audience-card-icon"></i>
      <div class="audience-card-title">i18n &amp; RTL</div>
      <p class="audience-card-desc">Built-in locale switching via /src/locales for multi-language classrooms, including right-to-left scripts.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-keyboard audience-card-icon"></i>
      <div class="audience-card-title">Accessibility</div>
      <p class="audience-card-desc">Keyboard navigation (1–4 / a–d for MCQs, Enter to advance), ARIA roles, high-contrast toggle, reduced-motion friendly animations.</p>
    </div>
  </div>
</div>

<div class="grid-view-more">
  <button class="grid-view-more-btn" id="tenali-features-more">View more ↓</button>
</div>

<script>
(function() {
  var btn = document.getElementById('tenali-features-more');
  var wrap = document.getElementById('tenali-features-extra-wrap');
  if (!btn || !wrap) return;
  var inner = wrap.firstElementChild;
  var expanded = false;
  function expand() {
    wrap.classList.add('is-expanded');
    wrap.style.maxHeight = inner.scrollHeight + 'px';
  }
  function collapse() {
    wrap.style.maxHeight = inner.scrollHeight + 'px';
    void wrap.offsetHeight;
    wrap.classList.remove('is-expanded');
    wrap.style.maxHeight = '0px';
  }
  btn.addEventListener('click', function() {
    expanded = !expanded;
    if (expanded) { expand(); } else { collapse(); }
    btn.textContent = expanded ? 'View less ↑' : 'View more ↓';
  });
})();
</script>

---

## **Seven Modes at a Glance**

Seven ways to play. The same engine runs underneath — different shape on top.

<div class="scenario-tabs">
  <div class="scenario-tab-bar">
    <button class="scenario-tab active" onclick="showTnlMode('goal', this)">Goal Practice</button>
    <button class="scenario-tab" onclick="showTnlMode('battle', this)">Battle Arena</button>
    <button class="scenario-tab" onclick="showTnlMode('detective', this)">Detective</button>
    <button class="scenario-tab" onclick="showTnlMode('riddles', this)">Riddles</button>
    <button class="scenario-tab" onclick="showTnlMode('journey', this)">Guided Journey</button>
    <button class="scenario-tab" onclick="showTnlMode('random', this)">Random Mix</button>
    <button class="scenario-tab" onclick="showTnlMode('custom', this)">Custom Lesson</button>
  </div>

  <div class="scenario-panel active" id="tnl-mode-goal">
    <div class="scenario-panel-head"><i class="ph ph-target scenario-icon"></i><span class="scenario-title">Goal Practice</span></div>
    <p>Pick a target score on a chosen topic and chase it. The engine adapts as you go — too easy, the next question steps up; too hard, it eases back so you keep moving.</p>
    <span class="scenario-stat"><i class="ph ph-trend-up"></i> Hit your target or beat it</span>
  </div>
  <div class="scenario-panel" id="tnl-mode-battle">
    <div class="scenario-panel-head"><i class="ph ph-swords scenario-icon"></i><span class="scenario-title">Battle Arena</span></div>
    <p>Live fastest-finger duels. Two players, one question, the first correct answer wins the round. Streaks build ratings; ratings drive matchmaking.</p>
    <span class="scenario-stat"><i class="ph ph-globe"></i> Multiplayer over Socket.IO</span>
  </div>
  <div class="scenario-panel" id="tnl-mode-detective">
    <div class="scenario-panel-head"><i class="ph ph-magnifying-glass scenario-icon"></i><span class="scenario-title">Detective Agency</span></div>
    <p>Story-driven mysteries. Each case is a chain of math clues — solving one unlocks the next. Hundreds of procedurally generated cases.</p>
    <span class="scenario-stat"><i class="ph ph-path"></i> Chained clue progression</span>
  </div>
  <div class="scenario-panel" id="tnl-mode-riddles">
    <div class="scenario-panel-head"><i class="ph ph-lightbulb scenario-icon"></i><span class="scenario-title">Math Riddles</span></div>
    <p>Find the hidden rule in a puzzle. 48 riddles — find-rule, sequence, logic, image — designed to reward pattern recognition over speed.</p>
    <span class="scenario-stat"><i class="ph ph-shuffle"></i> 48 hand-authored riddles</span>
  </div>
  <div class="scenario-panel" id="tnl-mode-journey">
    <div class="scenario-panel-head"><i class="ph ph-graduation-cap scenario-icon"></i><span class="scenario-title">Guided Learning Journey</span></div>
    <p>Linear curriculum with concept checkpoints. The next concept unlocks only after the previous one is mastered — bronze unlocks silver unlocks gold.</p>
    <span class="scenario-stat"><i class="ph ph-lock-key"></i> Server-enforced progression</span>
  </div>
  <div class="scenario-panel" id="tnl-mode-random">
    <div class="scenario-panel-head"><i class="ph ph-shuffle scenario-icon"></i><span class="scenario-title">Random Mix</span></div>
    <p>A quiz that adapts to your weakest topics. Pulls from wherever your adaptScore is lowest, so practice lands where it matters.</p>
    <span class="scenario-stat"><i class="ph ph-chart-line-up"></i> Targets weak areas</span>
  </div>
  <div class="scenario-panel" id="tnl-mode-custom">
    <div class="scenario-panel-head"><i class="ph ph-sliders scenario-icon"></i><span class="scenario-title">Custom Lesson</span></div>
    <p>Hand-pick topics and question counts. Build the exact practice set you want — ten of one topic, twenty of another, no surprises.</p>
    <span class="scenario-stat"><i class="ph ph-pencil"></i> You decide the mix</span>
  </div>
</div>

<script>
function showTnlMode(id, btn) {
  document.querySelectorAll('[id^="tnl-mode-"]').forEach(function(p) { p.classList.remove('active'); });
  document.querySelectorAll('.scenario-tab').forEach(function(t) { t.classList.remove('active'); });
  document.getElementById('tnl-mode-' + id).classList.add('active');
  btn.classList.add('active');
}
</script>

---

## **The 91 Puzzles**

Every puzzle type shares the same two-route contract — `GET /<type>-api/question` and `POST /<type>-api/check`. To fetch a step-by-step explanation, send `{ solve: true }` in the POST body. Categories:

<div class="audience-grid">
  <div class="audience-card">
    <i class="ph ph-plus-circle audience-card-icon"></i>
    <div class="audience-card-title">Arithmetic &amp; Number</div>
    <p class="audience-card-desc">20 types — Addition, Column ops, Decimals, Fractions, Indices, Surds, Sequences, Ratio, Percentages, Profit &amp; Loss, Banking, GST.</p>
  </div>
  <div class="audience-card">
    <i class="ph ph-coins audience-card-icon"></i>
    <div class="audience-card-title">Commerce &amp; Statistics</div>
    <p class="audience-card-desc">8 types — Shares &amp; Dividends, Rounding, Standard Form, SDT, Number Bases, HCF &amp; LCM, Prime Factors, Bounds.</p>
  </div>
  <div class="audience-card">
    <i class="ph ph-function audience-card-icon"></i>
    <div class="audience-card-title">Algebra</div>
    <p class="audience-card-desc">15 types — Variation, Linear &amp; Simultaneous, Quadratics, Polynomials, Remainder &amp; Binomial, Functions, plus multiple MCQ gyms.</p>
  </div>
  <div class="audience-card">
    <i class="ph ph-shapes audience-card-icon"></i>
    <div class="audience-card-title">Geometry &amp; Trig</div>
    <p class="audience-card-desc">14 types — Trig, Inverse Trig, Circular Measure, Inequalities, Coordinate Geometry, Probability, Sets, Bearings, Matrices.</p>
  </div>
  <div class="audience-card">
    <i class="ph ph-grid-four audience-card-icon"></i>
    <div class="audience-card-title">Linear Algebra &amp; Vectors</div>
    <p class="audience-card-desc">6 types — LA Mission Quiz, Vectors, Dot Products, Transformations, Mensuration. Plus the curated 56-mission Linear Algebra Lab.</p>
  </div>
  <div class="audience-card">
    <i class="ph ph-gamepad audience-card-icon"></i>
    <div class="audience-card-title">Calculus &amp; Games</div>
    <p class="audience-card-desc">15+ types — Differentiation, Integration, Limits, Conics, Sudoku, Darts, Riddles, Curiosity, plus Conceptual, Vocabulary (7,662 words) and GK (991 questions).</p>
  </div>
</div>

---

## **Architecture**

React 19 single-page application, served by a single Express 5 process with Mongoose 9 against MongoDB and Socket.IO 4 for live multiplayer. JWT auth with bcrypt 10 rounds, express-rate-limit, CORS allowlist, env-sourced seed users. Frontend uses Vite 8, framer-motion, Three.js, mafs, and face-api.js for the proctoring layer. The scoring pipeline mirrors operational data and recomputes from scratch on every run.

The whole thing runs on a single VPS — tenali.fun — with one Node process serving the React app, the puzzle APIs, the JWT auth, the Socket.IO Battle Arena, and the multi-language code playground. No question database: every question is generated on the fly, so practice is infinite and never repeats.

---

## **In the Room**

Tenali runs inside the platforms learners are already using. No separate app, no extra login. The experience changes from inside.

<div class="scenario-tabs">
  <div class="scenario-tab-bar">
    <button class="scenario-tab active" onclick="showTnlRoom('learners', this)">Learners</button>
    <button class="scenario-tab" onclick="showTnlRoom('parents', this)">Parents</button>
    <button class="scenario-tab" onclick="showTnlRoom('schools', this)">Schools</button>
  </div>

  <div class="scenario-panel active" id="tnl-room-learners">
    <div class="scenario-panel-head"><i class="ph ph-student scenario-icon"></i><span class="scenario-title">Learners</span></div>
    <p>The hardest part of math isn't the math — it's staying engaged long enough to get past the awkward middle. Tenali keeps practice moving: the next question lands where the last one left you, and the explanation is always one tap away.</p>
    <p>Pick a topic, play 20 questions, see the band move. Pick up tomorrow from where you stopped.</p>
    <span class="scenario-stat"><i class="ph ph-trend-up"></i> Practice that adjusts to you</span>
  </div>
  <div class="scenario-panel" id="tnl-room-parents">
    <div class="scenario-panel-head"><i class="ph ph-house-line scenario-icon"></i><span class="scenario-title">Parents</span></div>
    <p>Open the parent view, see what your child practised today, where the bands sit, and which topics still glow red. No login dance, no app to install — just a glance.</p>
    <span class="scenario-stat"><i class="ph ph-eye"></i> Effort made visible</span>
  </div>
  <div class="scenario-panel" id="tnl-room-schools">
    <div class="scenario-panel-head"><i class="ph ph-buildings scenario-icon"></i><span class="scenario-title">Schools &amp; Programmes</span></div>
    <p>Run a cohort — an internship, a summer school, a numeracy intervention. The proctoring layer keeps tabs on engagement; the leaderboards make effort visible without making it a competition.</p>
    <span class="scenario-stat"><i class="ph ph-chart-bar"></i> Cohort-level signals</span>
  </div>
</div>

<script>
function showTnlRoom(id, btn) {
  document.querySelectorAll('[id^="tnl-room-"]').forEach(function(p) { p.classList.remove('active'); });
  document.querySelectorAll('.scenario-tab').forEach(function(t) { t.classList.remove('active'); });
  document.getElementById('tnl-room-' + id).classList.add('active');
  btn.classList.add('active');
}
</script>

---

## **Proctoring System**

Optional exam-mode supervision. Webcam + face-api.js emotion detection, focus / tab-switch event logging, and an admin-only dashboard for staff. The goal is to keep assessment honest without making learners feel surveilled.

<div class="tnl-proctor">
  <div class="tnl-proctor-band">
    <span class="tnl-proctor-label"><i class="ph ph-shield-check"></i> PROCTORING SYSTEM</span>
    <h2 class="tnl-proctor-h">Watchful without being intrusive.</h2>
    <p class="tnl-proctor-p">Focus is a signal, not a verdict. The proctoring layer measures engagement — where attention drifts, when tabs switch, whether the face is still at the screen — and surfaces it to the staff dashboard. Learners see their own score; teachers see the cohort.</p>
  </div>

  <div class="tnl-proctor-grid">
    <div class="tnl-proctor-viewport">
      <div class="tnl-proctor-mesh"></div>
      <div class="tnl-proctor-face-box"></div>
      <div class="tnl-proctor-badge"><i class="ph ph-check-circle"></i> Face Detected</div>
      <div class="tnl-proctor-gaze"><span class="tnl-proctor-eye"></span> Looking at tab</div>
      <div class="tnl-proctor-emotion"><span class="tnl-proctor-emo-icon">😐</span> Neutral · 92% conf</div>
      <div class="tnl-proctor-transcript">
        <span class="tnl-proctor-tx-text">Solve 3x² − 12 = 27 by isolating x² first</span><span class="tnl-proctor-cursor"></span>
      </div>
    </div>
    <div class="tnl-proctor-stats">
      <div class="tnl-proctor-stat-row">
        <span class="tnl-proctor-stat-label">Focus Score</span>
        <span class="tnl-proctor-stat-value tnl-good" id="tnl-focus-val">92%</span>
        <div class="tnl-proctor-stat-meter"><div class="tnl-proctor-stat-fill" id="tnl-focus-fill"></div></div>
      </div>
      <div class="tnl-proctor-stat-row">
        <span class="tnl-proctor-stat-label">Emotion (face-api.js)</span>
        <span class="tnl-proctor-stat-emotion"><span>😐</span> Neutral</span>
      </div>
      <div class="tnl-proctor-stat-row">
        <span class="tnl-proctor-stat-label">Tab switches</span>
        <span class="tnl-proctor-stat-value tnl-amber" id="tnl-tabs-val">0</span>
        <div class="tnl-proctor-stat-meter"><div class="tnl-proctor-stat-fill tnl-fill-amber" id="tnl-tabs-fill"></div></div>
      </div>
      <div class="tnl-proctor-stat-row">
        <span class="tnl-proctor-stat-label">Look-aways</span>
        <span class="tnl-proctor-stat-value" id="tnl-look-val">0</span>
        <div class="tnl-proctor-stat-meter"><div class="tnl-proctor-stat-fill" id="tnl-look-fill"></div></div>
      </div>
    </div>
  </div>

  <div class="tnl-proctor-admin">
    <img src="{{ site.baseurl }}/assets/images/tenali/proctor-admin.png" alt="Tenali proctoring admin dashboard" loading="lazy">
  </div>

  <div class="tnl-proctor-feature-row">
    <div class="audience-card">
      <i class="ph ph-camera audience-card-icon"></i>
      <div class="audience-card-title">Webcam + face-api.js</div>
      <p class="audience-card-desc">Real-time emotion detection. Neutral, focused, confused — the engine reads the room without storing frames.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-eye audience-card-icon"></i>
      <div class="audience-card-title">Focus tracking</div>
      <p class="audience-card-desc">Tab switches, look-aways, face-missing events — every signal logged, every signal reviewable by the learner and by staff.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-lock-key audience-card-icon"></i>
      <div class="audience-card-title">Admin-only dashboard</div>
      <p class="audience-card-desc">/api/proctor/sessions — staff-only routes, secured with requireAdmin. Live stats, flagged sessions, per-student history.</p>
    </div>
  </div>
</div>

<script>
(function() {
  var reduceMotion = window.matchMedia && window.matchMedia('(prefers-reduced-motion: reduce)').matches;
  var focusVal = document.getElementById('tnl-focus-val');
  var focusFill = document.getElementById('tnl-focus-fill');
  var tabsVal = document.getElementById('tnl-tabs-val');
  var tabsFill = document.getElementById('tnl-tabs-fill');
  var lookVal = document.getElementById('tnl-look-val');
  var lookFill = document.getElementById('tnl-look-fill');
  if (!focusVal) return;

  function setPct(valEl, fillEl, pct) {
    valEl.textContent = pct + '%';
    if (fillEl) fillEl.style.setProperty('--final', pct + '%');
  }

  function setCount(valEl, fillEl, n, max) {
    valEl.textContent = n;
    if (fillEl) fillEl.style.setProperty('--final', Math.min((n / max) * 100, 100) + '%');
  }

  setPct(focusVal, focusFill, 92);
  setCount(tabsVal, tabsFill, 1, 5);
  setCount(lookVal, lookFill, 0, 5);

  if (reduceMotion) return;

  // tab-switch counter: cycles 0 → 1 → 2 → 3 → 0 ...
  var t = 0;
  setInterval(function() {
    t = (t + 1) % 5;
    var n = t;
    setCount(tabsVal, tabsFill, n, 5);
  }, 3800);

  // look-aways counter: cycles 0 → 1 → 0 → 1 ...
  var l = 0;
  setInterval(function() {
    l = (l + 1) % 3;
    setCount(lookVal, lookFill, l, 5);
  }, 6200);

  // focus score breathing
  setInterval(function() {
    var base = 88 + Math.round(Math.random() * 8);
    setPct(focusVal, focusFill, base);
  }, 5200);
})();
</script>

---

## **By the Numbers**

Tenali is built and kept running by a community of student and staff contributors.

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

## **Where It's Going**

The current build runs as one Node process on a single VPS. Here is what the lab is actively building toward.

<div class="roadmap">
  <div class="roadmap-item">
    <div class="roadmap-status"><span class="rm-badge rm-live">Live</span></div>
    <div class="roadmap-body">
      <div class="roadmap-title">Adaptive engine + 69 puzzle families</div>
      <div class="roadmap-desc">Difficult adjusts to the learner in real time, across every topic — arithmetic, geometry, algebra, calculus, vocab, GK.</div>
    </div>
  </div>
  <div class="roadmap-item">
    <div class="roadmap-status"><span class="rm-badge rm-progress">In Progress</span></div>
    <div class="roadmap-body">
      <div class="roadmap-title">Offline classroom experiments</div>
      <div class="roadmap-desc">Settings without reliable internet need Tenali to work differently at the listening and question-generation layer. Initial deployments planned.</div>
    </div>
  </div>
  <div class="roadmap-item">
    <div class="roadmap-status"><span class="rm-badge rm-upcoming">Upcoming</span></div>
    <div class="roadmap-body">
      <div class="roadmap-title">Mobile-native client</div>
      <div class="roadmap-desc">A dedicated mobile shell that respects the adaptive engine while reducing bandwidth and battery load on low-end devices.</div>
    </div>
  </div>
  <div class="roadmap-item">
    <div class="roadmap-status"><span class="rm-badge rm-upcoming">Research</span></div>
    <div class="roadmap-body">
      <div class="roadmap-title">What effort signals actually predict</div>
      <div class="roadmap-desc">Every Tenali cohort generates data on which engagement patterns correlate with learning outcomes. The research question — what does consistent SP accumulation actually predict, and which actions matter most?</div>
    </div>
  </div>
</div>

---

## **Summership**

A flagship initiative running on Tenali — a structured summer learning cohort that uses the adaptive engine to keep every learner in their zone, with the proctoring layer providing engagement signals to programme coordinators.

<div class="section-band">
  <h2>Summership — the cohort mode Tenali was built for.</h2>
  <p>Engagement tracked per session, per learner, per cohort. The same engine that keeps one student in their zone keeps a hundred.</p>
</div>

<img src="{{ site.baseurl }}/assets/images/tenali/summership.png" alt="Tenali Summership — guided learning journey tour" loading="lazy" style="width:100%; border:1px solid #e2e2de; border-radius:6px; margin-top:1.5rem;">

---

## **Contributors**

Tenali is built and maintained by a community of student and staff contributors.

<div class="contributor-list">
  <span class="contributor-chip">S. R. S. Iyengar</span>
  <span class="contributor-chip">Mudit Agrawal</span>
  <span class="contributor-chip">Jinal Gupta</span>
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
