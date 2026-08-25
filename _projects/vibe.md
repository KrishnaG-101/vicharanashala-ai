---
layout: default
title: ViBe
page_title: ViBe - The Future of Learning
parent: Products
order: 1
---

<div class="initiative-page-hero product-page-hero">
  <a href="{{ site.baseurl }}/products/" class="initiative-back"><i class="ph ph-arrow-left"></i> Products</a>
  <p class="story-label"><i class="ph ph-brain"></i> Products</p>
  <h1 class="initiative-page-h">ViBe</h1>
</div>

{% include page-quote.html %}


<style>
  /* Scoped to this page, mobile only — tighter rhythm to cut scroll length on phones */
  @media (max-width: 600px) {
    .page-content .wrapper hr { margin: 1.4rem 0; }
    .page-content .wrapper h2 { margin-top: 1.3rem; }
    .page-content .wrapper .audience-grid { gap: 0.8rem; margin-top: 1rem; }
    .page-content .wrapper .audience-card { padding: 1.1rem; }
    .page-content .wrapper .split-media { gap: 1rem; }
    .page-content .wrapper .video-card { margin: 1rem 0; }
    .page-content .wrapper .shot-carousel { margin: 1rem 0 1.4rem; }
    .page-content .wrapper .contributor-list { margin: 1rem 0 1.2rem; }
  }
</style>

*Like Vikram with Betaal at every stride,*
*ViBe questions you–till trust and confidence walk by your side.*

**[Try ViBe ↗](https://vibe.vicharanashala.ai){:target="_blank"}**

ViBe launched on 29th July 2025, when Education Minister Shri Dharmendra Pradhan unveiled it at the Akhil Bharatiya Shiksha Samagam. It's open-source and free to use, built and kept running by a community of developers and educators. You can look at the code or help build it on our [GitHub Repository](https://github.com/vicharanashala/vibe).

---

## **About**

<div class="split-media">
<p>ViBe turns passive video-watching into active learning. It gives students a clear, step-by-step way to learn, gives teachers useful insights without extra work, and is built so students trust the process and feel sure about what they know.</p>

{% include video-thumb.html id="6AYCVKDIeTs" title="ViBe – Concept Video" %}
</div>

---

## **Who It's For**

<div class="audience-grid">
  <div class="audience-card">
    <i class="ph ph-graduation-cap audience-card-icon"></i>
    <div class="audience-card-title">Students</div>
    <p class="audience-card-desc">Learn in short video segments with quizzes built in. Earn points, track your own progress, ask questions right on the video, and get instant help from an AI assistant.</p>
  </div>
  <div class="audience-card">
    <i class="ph ph-chalkboard-teacher audience-card-icon"></i>
    <div class="audience-card-title">Teachers</div>
    <p class="audience-card-desc">Turn any video or playlist into a full course. ViBe splits it into parts, writes a transcript, and drafts quiz questions for you to check. Manage your students, invites, and announcements from one place.</p>
  </div>
</div>

---

## **See It In Action**

A look at the real product – swipe through the screens students and teachers actually use.

<div class="shot-carousel" id="vibe-shot-carousel">
  <div class="shot-carousel-viewport">
  <div class="shot-slide active">
    <img src="{{ site.baseurl }}/assets/images/vibe/vibe-sign-in.png" alt="ViBe sign-in screen">
    <figcaption>Sign in – students and teachers each get their own portal.</figcaption>
  </div>
  <div class="shot-slide">
    <img src="{{ site.baseurl }}/assets/images/vibe/vibe-dashboard.png" alt="ViBe student dashboard">
    <figcaption>Dashboard – courses and progress at a glance.</figcaption>
  </div>
  <div class="shot-slide">
    <img src="{{ site.baseurl }}/assets/images/vibe/vibe-lecture-slide.png" alt="ViBe micro-learning lecture segment">
    <figcaption>Micro-learning – lectures broken into focused segments.</figcaption>
  </div>
  <div class="shot-slide">
    <img src="{{ site.baseurl }}/assets/images/vibe/vibe-course-content.png" alt="ViBe course content sidebar with quiz checkpoints">
    <figcaption>Course content – quiz checkpoints built into the video timeline.</figcaption>
  </div>
  <div class="shot-slide">
    <img src="{{ site.baseurl }}/assets/images/vibe/vibe-ai-exam.png" alt="ViBe AI-generated exam interface">
    <figcaption>AI-built exams – auto-generated questions with timers and difficulty settings.</figcaption>
  </div>
  <div class="shot-slide">
    <img src="{{ site.baseurl }}/assets/images/vibe/vibe-analytics.png" alt="ViBe learning analytics dashboard">
    <figcaption>Learning Analytics – progress and quiz performance, per learner.</figcaption>
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
  var root = document.getElementById('vibe-shot-carousel');
  if (!root) return;
  var slides = root.querySelectorAll('.shot-slide');
  var dots = root.querySelectorAll('.shot-carousel-dot');
  var prevBtn = root.querySelector('.shot-carousel-prev');
  var nextBtn = root.querySelector('.shot-carousel-next');
  var viewport = root.querySelector('.shot-carousel-viewport');
  var current = 0;
  var timer;

  function positionArrows() {
    if (!prevBtn || !viewport) return;
    var img = slides[current].querySelector('img');
    if (!img) return;
    var imgRect = img.getBoundingClientRect();
    var viewportRect = viewport.getBoundingClientRect();
    var centerY = imgRect.top - viewportRect.top + imgRect.height / 2;
    prevBtn.style.top = centerY + 'px';
    nextBtn.style.top = centerY + 'px';
  }

  function goTo(index) {
    slides[current].classList.remove('active');
    dots[current].classList.remove('active');
    current = (index + slides.length) % slides.length;
    slides[current].classList.add('active');
    dots[current].classList.add('active');
    positionArrows();
  }

  function startAuto() {
    timer = setInterval(function() { goTo(current + 1); }, 4000);
  }

  dots.forEach(function(dot, i) {
    dot.addEventListener('click', function() {
      clearInterval(timer);
      goTo(i);
      startAuto();
    });
  });

  if (prevBtn) {
    prevBtn.addEventListener('click', function() {
      clearInterval(timer);
      goTo(current - 1);
      startAuto();
    });
  }

  if (nextBtn) {
    nextBtn.addEventListener('click', function() {
      clearInterval(timer);
      goTo(current + 1);
      startAuto();
    });
  }

  positionArrows();
  window.addEventListener('resize', positionArrows);
  startAuto();
})();
</script>

---

## **The Challenge**

Online courses are easy to access but hard to finish. Most self-paced video courses see only 10 to 15 percent of learners complete them. Most platforms just show the video and hope learning happens. Without a teacher watching, students often let the video play without really following it. The challenge is building a system that keeps learners accountable without making them feel watched or anxious.

---

## **The Platform**

ViBe takes its name from the old tale of Vikram and Betaal, where a wrong answer means going back and trying again. ViBe works the same way: it checks how well you understand something as you go, and asks you to revisit anything you missed.

{% include video-thumb.html id="8ytNdYlK-BU" title="ViBe – Interactive Demo" %}

<div class="audience-grid">
  <div class="audience-card">
    <i class="ph ph-scissors audience-card-icon"></i>
    <div class="audience-card-title">Micro-Learning</div>
    <p class="audience-card-desc">Long lectures are automatically split into short parts, one idea at a time, so you're never overwhelmed.</p>
  </div>
  <div class="audience-card">
    <i class="ph ph-target audience-card-icon"></i>
    <div class="audience-card-title">Smart Assessments</div>
    <p class="audience-card-desc">Quizzes pop up during the video, not after it, so you're tested while it's still fresh, not days later.</p>
  </div>
  <div class="audience-card">
    <i class="ph ph-shield-check audience-card-icon"></i>
    <div class="audience-card-title">Active Verification</div>
    <p class="audience-card-desc">AI watches for signs you've lost focus, like switching tabs or looking away, without making it feel like it's spying on you.</p>
  </div>
</div>

<div class="grid-extra-wrap" id="platform-extra-wrap">
  <div class="audience-grid">
    <div class="audience-card">
      <i class="ph ph-users-three audience-card-icon"></i>
      <div class="audience-card-title">ViBeCrowd</div>
      <p class="audience-card-desc">Learners help write and check quiz questions together, so the question bank keeps getting better.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-magic-wand audience-card-icon"></i>
      <div class="audience-card-title">AI Course Generation</div>
      <p class="audience-card-desc">Give ViBe a video or playlist and it builds a course from it: splitting it into parts, writing a transcript, and drafting quiz questions. The teacher checks and approves each step. Or just share one video and see who watched it.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-trophy audience-card-icon"></i>
      <div class="audience-card-title">Community & Recognition</div>
      <p class="audience-card-desc">Earn points, see how you rank against classmates, ask questions right on the video, and share how you're feeling about each lesson.</p>
    </div>
  </div>
</div>

<div class="grid-view-more">
  <button class="grid-view-more-btn" id="platform-view-more">View more ↓</button>
</div>

<script>
(function() {
  var btn = document.getElementById('platform-view-more');
  var wrap = document.getElementById('platform-extra-wrap');
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

## **The Impact**

ViBe is already used nationwide as part of the Ministry of Education's Malaviya Mission Teacher Training Programme.

<div class="stat-row will-animate" id="impact-stat-row">
  <div class="stat"><span class="stat-number">11,509</span><span class="stat-label">Unique Learners</span></div>
  <div class="stat"><span class="stat-number">5,472</span><span class="stat-label">Active Enrollments</span></div>
  <div class="stat"><span class="stat-number">39</span><span class="stat-label">Courses & Cohorts Live</span></div>
  <div class="stat"><span class="stat-number">~51%</span><span class="stat-label">Completion Rate</span></div>
</div>

<script>
(function() {
  var row = document.getElementById('impact-stat-row');
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

  if (!('IntersectionObserver' in window)) {
    reveal();
    return;
  }

  var observer = new IntersectionObserver(function(entries) {
    entries.forEach(function(entry) {
      if (entry.isIntersecting) {
        reveal();
        observer.unobserve(row);
      }
    });
  }, { threshold: 0.3 });

  observer.observe(row);
})();
</script>

Most self-paced online courses see under 10% of learners finish. ViBe gets roughly 5 times that, with real proctoring, at a very low cost per learner.

<div class="grid-extra-wrap" id="impact-methodology-wrap">
  <ul class="impact-methodology">
    <li><strong>Unique Learners</strong> — distinct users with any student enrollment.</li>
    <li><strong>Active Enrollments</strong> — completed enrollments (5,324) plus enrollments with activity in the last 7 days (148).</li>
    <li><strong>Courses & Cohorts Live</strong> — courses with 20 or more learners.</li>
    <li><strong>Completion Rate</strong> — completed ÷ started (over 1% progress): 5,332 of 10,537 enrollments. At the per-learner level it's 48% (3,525 of 7,292 learners); the figure above is per enrollment.</li>
  </ul>
</div>

<div class="grid-view-more">
  <button class="grid-view-more-btn" id="impact-methodology-toggle">View methodology ↓</button>
</div>

<script>
(function() {
  var btn = document.getElementById('impact-methodology-toggle');
  var wrap = document.getElementById('impact-methodology-wrap');
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
    btn.textContent = expanded ? 'Hide methodology ↑' : 'View methodology ↓';
  });
})();
</script>

---

## **Built to Scale**

For schools and colleges deciding whether to adopt ViBe:

<div class="audience-grid">
  <div class="audience-card">
    <i class="ph ph-lock-open audience-card-icon"></i>
    <div class="audience-card-title">Open-Source, Self-Hostable</div>
    <p class="audience-card-desc">Free to use and free to host yourself. No per-student fees, no lock-in.</p>
  </div>
  <div class="audience-card">
    <i class="ph ph-user-focus audience-card-icon"></i>
    <div class="audience-card-title">Automatic Engagement Enforcement</div>
    <p class="audience-card-desc">If a student stops engaging, ViBe flags and warns them automatically. Students can appeal too, so no manual follow-up is needed.</p>
  </div>
  <div class="audience-card">
    <i class="ph ph-clipboard-text audience-card-icon"></i>
    <div class="audience-card-title">Audit Trail</div>
    <p class="audience-card-desc">Every action taken on the platform is logged, so admins can check what happened and when.</p>
  </div>
</div>

<div class="grid-extra-wrap" id="scale-extra-wrap">
  <div class="audience-grid audience-grid--continued">
    <div class="audience-card">
      <i class="ph ph-user-check audience-card-icon"></i>
      <div class="audience-card-title">Gated Enrollment</div>
      <p class="audience-card-desc">Teachers or admins can approve who joins a course, instead of leaving it open to anyone.</p>
    </div>
    <div class="audience-card">
      <i class="ph ph-flag audience-card-icon"></i>
      <div class="audience-card-title">Proven at National Scale</div>
      <p class="audience-card-desc">Already running as part of a real Ministry of Education programme, not just a test.</p>
    </div>
  </div>
</div>

<div class="grid-view-more">
  <button class="grid-view-more-btn" id="scale-view-more">View more ↓</button>
</div>

<script>
(function() {
  var btn = document.getElementById('scale-view-more');
  var wrap = document.getElementById('scale-extra-wrap');
  if (!btn || !wrap) return;
  var inner = wrap.firstElementChild;
  var expanded = false;

  var firstRowCards = wrap.previousElementSibling.querySelectorAll('.audience-card');
  var extraCards = inner.querySelectorAll('.audience-card');
  var maxCardHeight = 0;
  firstRowCards.forEach(function(c) { maxCardHeight = Math.max(maxCardHeight, c.getBoundingClientRect().height); });
  extraCards.forEach(function(c) { maxCardHeight = Math.max(maxCardHeight, c.getBoundingClientRect().height); });
  if (maxCardHeight) {
    firstRowCards.forEach(function(c) { c.style.minHeight = maxCardHeight + 'px'; });
    extraCards.forEach(function(c) { c.style.minHeight = maxCardHeight + 'px'; });
  }

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

Built at the VLED Lab, IIT Ropar, with support from UGC.

---

## **Learner Feedback**

<div class="split-media">
<p>What does it feel like to learn on ViBe? Here is a glimpse from the platform.</p>

{% include video-thumb.html id="AWuA4b9dUpM" title="ViBe – Learner Feedback" %}
</div>

---

## **Contributors**

ViBe is built and maintained by a community of student and staff contributors.

<div class="contributor-list">
  <span class="contributor-chip">Meenakshi V</span>
  <span class="contributor-chip">Sai Samhith Reddy</span>
  <span class="contributor-chip">Joel Joseph Philip</span>
  <span class="contributor-chip">Jatish Chawla</span>
  <span class="contributor-chip">Tanvish Desai</span>
  <span class="contributor-chip">Aman Sagar</span>
</div>

<a class="contributor-more" href="https://github.com/vicharanashala/vibe/graphs/contributors" target="_blank" rel="noopener">See the full list on GitHub <i class="ph ph-arrow-right"></i></a>

---

Experience the rhythm of learning today at [vibe.vicharanashala.ai](https://vibe.vicharanashala.ai){:target="_blank"}.
