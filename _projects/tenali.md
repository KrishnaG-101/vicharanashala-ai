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

<p class="product-page-tagline">Adaptive math practice featuring 69 puzzle types, live multiplayer, and step-by-step explanations.</p>

---

## **About**

**Tenali** is named after the legendary **Tenali Raman**—the witty Indian scholar who outwitted entire courts with logic rather than just facts. The platform is built on this very idea: math isn't memorized; it's *outwitted*.

Every question is dynamically calibrated to the learner—the next one lands precisely where the last one left off.

Tenali covers everything from foundational numeracy to advanced algebra in a game-like structure that keeps learners deeply invested. Live and free at <a href="https://tenali.fun" target="_blank" rel="noopener">tenali.fun</a>.

**Why it works:** Every question is generated on the fly from over 91 topics—including arithmetic, geometry, algebra, calculus, vocabulary, and general knowledge. Because there is no static question database, practice is truly infinite and never repeats. The engine chooses the next question based entirely on what the learner just demonstrated they know. Difficulty isn't a toggleable setting; it's a personalized, per-learner trajectory.

A learner moves through four stages in every session:

<div class="tnl-marquee tnl-marquee--4" id="tnl-workflow-marquee">
  <button class="tnl-marquee-arrow tnl-marquee-arrow--left" id="tnl-workflow-left" aria-label="Scroll workflow left"><i class="ph ph-caret-left"></i></button>
  <button class="tnl-marquee-arrow tnl-marquee-arrow--right" id="tnl-workflow-right" aria-label="Scroll workflow right"><i class="ph ph-caret-right"></i></button>
  <div class="tnl-marquee-track" id="tnl-workflow-track">
    <div class="audience-card">
      <i class="ph ph-globe audience-card-icon"></i>
      <div class="audience-card-title">1 · Open</div>
      <p class="audience-card-desc">Land on the home grid at tenali.fun and browse 91+ colorful topic cards. Guest mode works fully; JWT login is optional.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-target audience-card-icon"></i>
      <div class="audience-card-title">2 · Pick</div>
      <p class="audience-card-desc">Choose from 8 distinct modes—like Goal Practice, Battle Arena, or Guided Journey—or dive straight into a topic card.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-play audience-card-icon"></i>
      <div class="audience-card-title">3 · Play</div>
      <p class="audience-card-desc">Solve 20 adaptive questions. Correct answers increase your adaptScore; incorrect ones lower it. Tap "Solve" anytime for a step-by-step walkthrough.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-trophy audience-card-icon"></i>
      <div class="audience-card-title">4 · Earn</div>
      <p class="audience-card-desc">Earn coins, XP, streaks, and badges. Progress is saved in MongoDB, so you can pick up tomorrow right where you left off.</p>
    </div>
  </div>
</div>

<img class="tnl-screenshot" src="{{ site.baseurl }}/assets/images/tenali/home-grid.png" alt="Tenali home grid — 91+ topic cards color-coded by domain" loading="lazy">

<script>
(function() {
  var shots = document.querySelectorAll('.tnl-screenshot');
  if (!shots.length) return;
  var reduceMotion = window.matchMedia && window.matchMedia('(prefers-reduced-motion: reduce)').matches;

  // Reveal on scroll into view
  if (!('IntersectionObserver' in window)) {
    shots.forEach(function(s) { s.classList.add('is-in'); });
  } else {
    var io = new IntersectionObserver(function(entries) {
      entries.forEach(function(e) {
        if (e.isIntersecting) {
          e.target.classList.add('is-in');
          io.unobserve(e.target);
        }
      });
    }, { threshold: 0.2 });
    shots.forEach(function(s) { io.observe(s); });
  }

  // Mouse-tracking 3D tilt + cursor spotlight
  if (reduceMotion) return;
  shots.forEach(function(shot) {
    var raf = null;
    var targetX = 0, targetY = 0, currentX = 0, currentY = 0;

    function onMove(e) {
      var rect = shot.getBoundingClientRect();
      var px = (e.clientX - rect.left) / rect.width;   // 0..1
      var py = (e.clientY - rect.top) / rect.height;   // 0..1
      shot.style.setProperty('--mx', (px * 100) + '%');
      shot.style.setProperty('--my', (py * 100) + '%');
      targetY = (px - 0.5) * 14;   // rotateY
      targetX = -(py - 0.5) * 10;  // rotateX
      if (!raf) raf = requestAnimationFrame(update);
    }

    function onLeave() {
      targetX = 0; targetY = 0;
      if (!raf) raf = requestAnimationFrame(update);
    }

    function update() {
      currentX += (targetX - currentX) * 0.15;
      currentY += (targetY - currentY) * 0.15;
      shot.style.setProperty('--tiltX', currentX.toFixed(2) + 'deg');
      shot.style.setProperty('--tiltY', currentY.toFixed(2) + 'deg');
      if (Math.abs(targetX - currentX) > 0.05 || Math.abs(targetY - currentY) > 0.05) {
        raf = requestAnimationFrame(update);
      } else {
        shot.style.setProperty('--tiltX', '0deg');
        shot.style.setProperty('--tiltY', '0deg');
        raf = null;
      }
    }

    shot.addEventListener('mousemove', onMove);
    shot.addEventListener('mouseleave', onLeave);
  });
})();
</script>

---

## **The Problem**

Math anxiety is a cycle that starts early and compounds over time. Traditional learning platforms simply gamify trivia—using arbitrary points, streaks, and superficial badges—without ever asking the fundamental question: *Is this specific question the right one for this learner at this exact moment?* Endless repetitive practice doesn't build intuition; it just builds memory.

---

## **What We Built**

Tenali flips the model. Pick a topic and get a question. The next question isn't pulled from a static list—it is precisely calibrated based on what you just demonstrated you know. A single, unified engine powers over 91 puzzle topics, spanning arithmetic, geometry, algebra, calculus, vocabulary, and general knowledge.

<div class="shot-carousel" id="tenali-shot-carousel">
  <div class="shot-carousel-viewport">
    <div class="shot-slide active">
      <img src="{{ site.baseurl }}/assets/images/tenali/home-grid.png" alt="Tenali home grid">
      <figcaption>Home grid — 91+ topics, color-coded by domain.</figcaption>
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
      <p class="audience-card-desc">A floating adaptScore (0–3) shifts with every answer. It seamlessly maps to difficulty bands: easy → medium → hard → extra-hard.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-swords audience-card-icon"></i>
      <div class="audience-card-title">Battle Arena</div>
      <p class="audience-card-desc">Live 1v1 fastest-finger duels over Socket.IO. Players get the same question, and the first correct answer wins.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-magnifying-glass audience-card-icon"></i>
      <div class="audience-card-title">Detective Agency</div>
      <p class="audience-card-desc">A chain of math clues where solving one unlocks the next. Explore hundreds of procedurally generated cases.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-graduation-cap audience-card-icon"></i>
      <div class="audience-card-title">Guided Journey</div>
      <p class="audience-card-desc">A linear curriculum with concept checkpoints. Server enforces progression through ranks: locked → blue → bronze → silver → gold.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-flask audience-card-icon"></i>
      <div class="audience-card-title">Concept Lab</div>
      <p class="audience-card-desc">A dynamic 5-stage mastery loop: Predict → Grid → Guided → Independent → Review.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-puzzle-piece audience-card-icon"></i>
      <div class="audience-card-title">Spaced Repetition</div>
      <p class="audience-card-desc">Recently missed questions are automatically promoted back into rotation powered by Bayesian Knowledge Tracing (BKT).</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-shield-check audience-card-icon"></i>
      <div class="audience-card-title">Proctoring</div>
      <p class="audience-card-desc">Optional exam-mode supervision via face-api.js—monitoring focus score, tab switches, and look-aways.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-trophy audience-card-icon"></i>
      <div class="audience-card-title">Gamification</div>
      <p class="audience-card-desc">Collect coins, XP, streaks, and pinned badges. Build album-style Collections that persist across your sessions.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-shuffle audience-card-icon"></i>
      <div class="audience-card-title">Random Mix &amp; Custom Lesson</div>
      <p class="audience-card-desc">Random Mix pulls heavily from your weakest areas. Custom Lesson lets you hand-pick exactly which topics and counts you want.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-terminal-window audience-card-icon"></i>
      <div class="audience-card-title">Code Playground</div>
      <p class="audience-card-desc">Run code in 50+ languages. Features a Python-Tutor-style visualizer with code, arrow pointers, and memory boxes.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-translate audience-card-icon"></i>
      <div class="audience-card-title">i18n &amp; RTL</div>
      <p class="audience-card-desc">Built-in locale switching tailored for multi-language classrooms, with full support for right-to-left scripts.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-keyboard audience-card-icon"></i>
      <div class="audience-card-title">Accessibility</div>
      <p class="audience-card-desc">Fully accessible with keyboard navigation, ARIA roles, high-contrast toggles, and reduced-motion friendly animations.</p>
    </div>
  </div>
</div>

---

## **Eight Modes at a Glance**

Eight distinct ways to play. Same underlying engine, beautifully different shapes on top.

<div class="tnl-marquee tnl-marquee--2" id="tnl-modes-marquee">
  <button class="tnl-marquee-arrow tnl-marquee-arrow--left" id="tnl-modes-left" aria-label="Scroll modes left"><i class="ph ph-caret-left"></i></button>
  <button class="tnl-marquee-arrow tnl-marquee-arrow--right" id="tnl-modes-right" aria-label="Scroll modes right"><i class="ph ph-caret-right"></i></button>
  <div class="tnl-marquee-track" id="tnl-modes-track">
    <div class="audience-card">
      <i class="ph ph-target audience-card-icon"></i>
      <div class="audience-card-title">Goal Practice</div>
      <p class="audience-card-desc">Pick a target score on a specific topic and chase it down. The engine adapts as you progress.</p>
      <span class="scenario-stat"><i class="ph ph-trend-up"></i> Hit your target or beat it</span>
    </div>
    <div class="audience-card">
      <i class="ph ph-swords audience-card-icon"></i>
      <div class="audience-card-title">Battle Arena</div>
      <p class="audience-card-desc">Two players, one question. First correct answer wins. Real-time streaks drive the matchmaking.</p>
      <span class="scenario-stat"><i class="ph ph-globe"></i> Multiplayer over Socket.IO</span>
    </div>
    <div class="audience-card">
      <i class="ph ph-magnifying-glass audience-card-icon"></i>
      <div class="audience-card-title">Detective Agency</div>
      <p class="audience-card-desc">A sequence of chained math clues; solving one unlocks the next. Hundreds of procedurally generated cases.</p>
      <span class="scenario-stat"><i class="ph ph-path"></i> Chained clue progression</span>
    </div>
    <div class="audience-card">
      <i class="ph ph-lightbulb audience-card-icon"></i>
      <div class="audience-card-title">Math Riddles</div>
      <p class="audience-card-desc">Uncover the hidden rule. Explore 48 hand-authored riddles across find-rule, sequence, logic, and image formats.</p>
      <span class="scenario-stat"><i class="ph ph-shuffle"></i> 48 hand-authored riddles</span>
    </div>
    <div class="audience-card">
      <i class="ph ph-graduation-cap audience-card-icon"></i>
      <div class="audience-card-title">Guided Learning Journey</div>
      <p class="audience-card-desc">A linear curriculum with defined concept checkpoints. The next concept unlocks only upon mastery.</p>
      <span class="scenario-stat"><i class="ph ph-lock-key"></i> Server-enforced progression</span>
    </div>
    <div class="audience-card">
      <i class="ph ph-shuffle audience-card-icon"></i>
      <div class="audience-card-title">Random Mix</div>
      <p class="audience-card-desc">Automatically pulls questions from wherever your adaptScore indicates you're weakest.</p>
      <span class="scenario-stat"><i class="ph ph-chart-line-up"></i> Targets weak areas</span>
    </div>
    <div class="audience-card">
      <i class="ph ph-sliders audience-card-icon"></i>
      <div class="audience-card-title">Custom Lesson</div>
      <p class="audience-card-desc">Take control by hand-picking exact topics and question counts for a customized session.</p>
      <span class="scenario-stat"><i class="ph ph-pencil"></i> You decide the mix</span>
    </div>
    <div class="audience-card">
      <i class="ph ph-function audience-card-icon"></i>
      <div class="audience-card-title">Linear Algebra Lab</div>
      <p class="audience-card-desc">56 missions spread across 6 modules: ratios, coordinate geometry, linear transformations, matrices, determinants, and PageRank.</p>
      <span class="scenario-stat"><i class="ph ph-chart-network"></i> 6 modules · 4 difficulty bands</span>
    </div>
  </div>
</div>

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

<div class="tnl-core-team">
  <div class="tnl-core-card">
    <div class="tnl-core-avatar">
      <span class="tnl-core-initials">SR</span>
      <img src="{{ site.baseurl }}/assets/images/team/s-r-s-iyengar.jpg" alt="S. R. S. Iyengar" loading="lazy">
    </div>
    <div class="tnl-core-name">S. R. S. Iyengar</div>
    <div class="tnl-core-role">Owner</div>
  </div>
  <div class="tnl-core-card">
    <div class="tnl-core-avatar">
      <span class="tnl-core-initials">JG</span>
      <img src="{{ site.baseurl }}/assets/images/team/jinal-gupta.jpg" alt="Jinal Gupta" loading="lazy">
    </div>
    <div class="tnl-core-name">Jinal Gupta</div>
    <div class="tnl-core-role">Mentor · Maintainer</div>
  </div>
  <div class="tnl-core-card">
    <div class="tnl-core-avatar">
      <span class="tnl-core-initials">SH</span>
      <img src="{{ site.baseurl }}/assets/images/team/s-hamsalekha.jpg" alt="S. Hamsalekha" loading="lazy">
    </div>
    <div class="tnl-core-name">S. Hamsalekha</div>
    <div class="tnl-core-role">Mentor · Maintainer</div>
  </div>
  <div class="tnl-core-card">
    <div class="tnl-core-avatar">
      <span class="tnl-core-initials">MA</span>
      <img src="{{ site.baseurl }}/assets/images/team/mudit-agrawal.jpg" alt="Mudit Agrawal" loading="lazy">
    </div>
    <div class="tnl-core-name">Mudit Agrawal</div>
    <div class="tnl-core-role">Maintainer</div>
  </div>
  <div class="tnl-core-card">
    <div class="tnl-core-avatar">
      <span class="tnl-core-initials">KG</span>
      <img src="{{ site.baseurl }}/assets/images/team/krishna-gelra.jpg" alt="Krishna Gelra" loading="lazy">
    </div>
    <div class="tnl-core-name">Krishna Gelra</div>
    <div class="tnl-core-role">Maintainer</div>
  </div>
</div>

<script>
(function() {
  document.querySelectorAll('.tnl-core-avatar img').forEach(function(img) {
    var initials = img.previousElementSibling;
    img.addEventListener('error', function() {
      img.style.display = 'none';
      if (initials) initials.style.display = 'flex';
    });
    img.addEventListener('load', function() {
      if (initials) initials.style.display = 'none';
    });
  });
})();
</script>

<div class="tnl-marquee tnl-contrib-marquee" id="tnl-contrib-marquee">
  <button class="tnl-marquee-arrow tnl-marquee-arrow--left" id="tnl-contrib-left" aria-label="Scroll contributors left"><i class="ph ph-caret-left"></i></button>
  <button class="tnl-marquee-arrow tnl-marquee-arrow--right" id="tnl-contrib-right" aria-label="Scroll contributors right"><i class="ph ph-caret-right"></i></button>
  <div class="tnl-marquee-track" id="tnl-contrib-track">
    <span class="contributor-chip tnl-contrib-chip">Lakshmi Varshini Nandula</span>
    <span class="contributor-chip tnl-contrib-chip">Sameer Mishra</span>
    <span class="contributor-chip tnl-contrib-chip">Vaibhav Satish</span>
    <span class="contributor-chip tnl-contrib-chip">Diptosubhro Datta</span>
    <span class="contributor-chip tnl-contrib-chip">Ritish Karmakar</span>
    <span class="contributor-chip tnl-contrib-chip">Ahana Banerjee</span>
    <span class="contributor-chip tnl-contrib-chip">K. C. Dharshan</span>
    <span class="contributor-chip tnl-contrib-chip">Saniya Jos</span>
    <span class="contributor-chip tnl-contrib-chip">Harsh Yadav</span>
    <span class="contributor-chip tnl-contrib-chip">Shubh Dixit</span>
    <span class="contributor-chip tnl-contrib-chip">Shreejal Bangera</span>
    <span class="contributor-chip tnl-contrib-chip">Poorvi Pravallika Pandraju</span>
    <span class="contributor-chip tnl-contrib-chip">Rukmender T</span>
    <span class="contributor-chip tnl-contrib-chip">Tanvish Desai</span>
    <span class="contributor-chip tnl-contrib-chip">Disha Bansal</span>
    <span class="contributor-chip tnl-contrib-chip">Remy Baastin Rayappan</span>
    <span class="contributor-chip tnl-contrib-chip">Anshul Kanodia</span>
    <span class="contributor-chip tnl-contrib-chip">Vasuki</span>
  </div>
</div>

<script>
// Refactored unified Smooth Scrolling Marquee logic
(function() {
  function initMarquee(trackId, leftBtnId, rightBtnId, itemSelector) {
    var track = document.getElementById(trackId);
    var leftBtn = document.getElementById(leftBtnId);
    var rightBtn = document.getElementById(rightBtnId);
    if (!track) return;

    var reduceMotion = window.matchMedia && window.matchMedia('(prefers-reduced-motion: reduce)').matches;

    // Clone once for seamless looping
    var originals = Array.prototype.slice.call(track.children);
    originals.forEach(function(el) { track.appendChild(el.cloneNode(true)); });

    var halfWidth = track.scrollWidth / 2;
    var position = 0;
    var targetPosition = 0;
    var velocity = reduceMotion ? 0 : 0.4;
    var paused = false;
    var isNudging = false;
    var resumeTimer = null;

    function apply() { track.style.transform = 'translate3d(' + position + 'px, 0, 0)'; }

    function frame() {
      if (isNudging) {
        // Smooth lerp (ease-out) for manual non-glitchy scrolling
        position += (targetPosition - position) * 0.12; 
        if (Math.abs(targetPosition - position) < 0.5) {
          position = targetPosition;
          isNudging = false;
        }
        
        // Wrap seamlessly if we cross the loop boundary
        if (-position >= halfWidth) {
          position += halfWidth;
          targetPosition += halfWidth;
        } else if (position > 0) {
          position -= halfWidth;
          targetPosition -= halfWidth;
        }
        apply();
      } else if (!paused && velocity !== 0) {
        position -= velocity;
        if (-position >= halfWidth) position += halfWidth;
        targetPosition = position; // Keep target in sync with auto-scroll
        apply();
      }
      requestAnimationFrame(frame);
    }
    apply();
    requestAnimationFrame(frame);

    function getStep() {
      if (itemSelector === '.tnl-contrib-chip') return 250; // Fixed scroll for chips
      var item = track.querySelector(itemSelector);
      return item ? item.getBoundingClientRect().width + 16 : 280;
    }

    function nudge(direction) {
      if (!isNudging) targetPosition = position;
      targetPosition += direction * getStep();
      isNudging = true;
      paused = true;
      if (resumeTimer) clearTimeout(resumeTimer);
      resumeTimer = setTimeout(function() { paused = false; }, 2000);
    }

    if (leftBtn)  leftBtn.addEventListener('click',  function() { nudge(-1); });
    if (rightBtn) rightBtn.addEventListener('click', function() { nudge(1); });

    var marquee = track.parentElement;
    if (marquee) {
      marquee.addEventListener('mouseenter', function() { paused = true; });
      marquee.addEventListener('mouseleave', function() { paused = false; });
    }
  }

  // Initialize all marquees with the new smooth engine
  initMarquee('tnl-workflow-track', 'tnl-workflow-left', 'tnl-workflow-right', '.audience-card');
  initMarquee('tnl-features-track', 'tnl-features-left', 'tnl-features-right', '.audience-card');
  initMarquee('tnl-modes-track', 'tnl-modes-left', 'tnl-modes-right', '.audience-card');
  initMarquee('tnl-contrib-track', 'tnl-contrib-left', 'tnl-contrib-right', '.tnl-contrib-chip');
})();
</script>

<a class="contributor-more" href="https://github.com/vicharanashala/tenali/graphs/contributors" target="_blank" rel="noopener">See the full list on GitHub <i class="ph ph-arrow-right"></i></a>

<div class="tnl-closing">
  <p class="tnl-closing-line">Step into the rhythm of math at <a href="https://tenali.fun" target="_blank" rel="noopener">tenali.fun</a>.</p>
  <div class="tnl-closing-actions">
    <a class="tnl-closing-btn tnl-closing-btn--primary" href="https://tenali.fun" target="_blank" rel="noopener"><i class="ph ph-play"></i> Try Tenali</a>
    <a class="tnl-closing-btn tnl-closing-btn--ghost" href="https://github.com/vicharanashala/tenali" target="_blank" rel="noopener"><i class="ph ph-github-logo"></i> View source</a>
  </div>
</div>
