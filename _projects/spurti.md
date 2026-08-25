---
layout: default
title: Spurti
page_title: Spurti - Gamified Engagement Tracking
parent: Products
order: 5
permalink: /projects/spurti/
quote: "We are what we repeatedly do."
quote_author: "Aristotle"
---

<div class="initiative-page-hero product-page-hero">
  <a href="{{ site.baseurl }}/products/" class="initiative-back"><i class="ph ph-arrow-left"></i> Products</a>
  <p class="story-label"><i class="ph ph-stairs"></i> Products</p>
  <h1 class="initiative-page-h">Spurti</h1>
</div>

{% include page-quote.html %}

<div class="product-page-meta">
  <span class="product-page-status">Deployed</span>
</div>

<p class="product-page-tagline">Automated engagement scoring for cohort-based programmes. Tracks participation, rewards consistency, makes effort visible.</p>

<div class="product-page-section">
  <h2>The Problem</h2>
  <p>In any multi-day or multi-week programme — internships, bootcamps, workshops, courses — attendance is the only engagement signal instructors have. Being in the room tells you nothing about who is answering questions, who is helping peers, who is engaging with the material. Instructors have no incentive structure for students to do more than show up.</p>
</div>

<div class="product-page-section">
  <h2>Who It Is For</h2>
  <p>Programme coordinators, instructors, and training leads running cohort-based learning programmes: summer schools, research internships, online courses, corporate training, workshops, and bootcamps. Whether it is a small group of 50 or a national programme with thousands, Spurti works anywhere consistent participation matters more than mere presence.</p>
</div>

<div class="product-page-section">
  <h2>What We Built</h2>
  <p>Spurti converts daily student actions into a transparent, automated point system. Attending sessions, answering polls correctly, teaching peers through structured endorsement workflows, and responding to peer queries: every meaningful contribution earns Spurti Points (SP). A scoring pipeline runs on a schedule, recomputing the entire cohort each time. No manual scoring, no CSV uploads, no instructor intervention.</p>
  <p>Students see their points accumulate, check their rank on live leaderboards, and earn shareable achievement cards for milestones and top placements. The scoring rubric is fully open, so every student can trace their points back to the specific actions that earned them.</p>
  <img src="{{ site.baseurl }}/assets/images/spurti/Dashboard.png" alt="Spurti student dashboard showing SP balance and engagement overview" loading="lazy" style="width:100%; border-radius:6px; margin-top:1rem; display:block;">
</div>

<div class="product-page-section">
  <h2>Key Features</h2>
  <p><strong>Automated Scoring Pipeline.</strong> Points are computed from live session data on a recurring schedule. Handles thousands of students without any manual overhead.</p>
  <p><strong>Band-and-Tier Rubric.</strong> Different actions earn different weights. Attendance is banded by percentage, poll performance is percentile-ranked against the day's top scorer, peer teaching and query answering earn per-action credits. The rubric is fully open and verifiable.</p>
  <img src="{{ site.baseurl }}/assets/images/spurti/SP Bank.png" alt="SP Bank showing point breakdown by category" loading="lazy" style="width:100%; border-radius:6px; margin-top:1rem; margin-bottom:1.5rem; display:block;">
  <p><strong>Live Leaderboards.</strong> Weekly and all-time, per-category (attendance, polls, peer teaching, queries) and overall. Students see the top 50 and their own rank regardless of position. Cohort-scoped boards for onboarding groups.</p>
  <img src="{{ site.baseurl }}/assets/images/spurti/Leaderboard.png" alt="Live leaderboard showing student rankings" loading="lazy" style="width:100%; border-radius:6px; margin-top:1rem; margin-bottom:1.5rem; display:block;">
  <p><strong>Levels and Trophy Leagues.</strong> Students level up based on their highest-ever SP and move through trophy leagues as their current balance changes. Both update automatically on every scoring run.</p>
  <p><strong>Shareable Achievement Cards.</strong> Permanent, verifiable credentials for leaderboard podium placements and milestones (highest-ever SP, Level thresholds, attendance goals). Each card carries a unique code and QR linking to a public verification page. Cards render as PNGs with LinkedIn-optimised metadata.</p>
  <div style="display:flex; gap:2%; margin-top:1rem; margin-bottom:1.5rem; justify-content:center;">
    <img src="{{ site.baseurl }}/assets/images/spurti/achievement-card1.png" alt="Shareable achievement card example" loading="lazy" style="width:40%; border-radius:6px;">
    <img src="{{ site.baseurl }}/assets/images/spurti/achievement-card2.png" alt="Achievement card with verification QR" loading="lazy" style="width:40%; border-radius:6px;">
  </div>
  <p><strong>Certificate Verification.</strong> Every achievement card links to a public page showing the student's name, what was earned, and when. No login required. Designed for sharing on LinkedIn and other platforms.</p>
  <p><strong>SP Trajectory.</strong> Students see their own SP over time compared to their cohort average and onboarding group. Visualises progress, not just current standing.</p>
  <p><strong>Course Commitments.</strong> Students can stake SP on course completion goals. Win or lose the stake based on actual completion, creating skin-in-the-game accountability.</p>
  <p><strong>My Journey.</strong> A phase-by-phase progress tracker where students set personal goals for attendance, peer teaching, and course completion with target dates.</p>
  <img src="{{ site.baseurl }}/assets/images/spurti/journey-and-goals.png" alt="My Journey progress tracker with personal goals" loading="lazy" style="width:100%; border-radius:6px; margin-top:1rem; margin-bottom:1.5rem; display:block;">
  <p><strong>Modular Plugin System.</strong> Teachers choose which modules to enable per course: attendance, assessments, peer queries, peer review, peer teaching, external course completion, exit tickets, leaderboards, rewards. Only the modules relevant to a programme are active, nothing a teacher does not need.</p>
  <p><strong>Programme Announcements.</strong> Targeted or broadcast notices with read-tracking. Instructors see read rates; students see what they have not acknowledged yet.</p>
  <p><strong>Admin Dashboard.</strong> Live stats on student distribution, SP distribution, pipeline health, achievement sharing analytics, and announcement read rates.</p>
</div>

<div class="product-page-section">
  <h2>Architecture</h2>
  <p>React single-page application with an Express.js API, backed by MongoDB. Authenticated through the parent platform's session, no separate sign-up required. The scoring pipeline runs as a separate cron-driven process that mirrors operational data and computes points from scratch on every run. Fully open source.</p>
</div>

<div class="product-page-section">
  <h2>In the Room</h2>
  <p>Spurti runs inside the platforms learners are already using. No separate app, no extra login. The experience changes from inside.</p>

  <div class="scenario-tabs">
    <div class="scenario-tab-bar">
      <button class="scenario-tab active" onclick="showScenario('learners', this)">Learners</button>
      <button class="scenario-tab" onclick="showScenario('instructors', this)">Instructors</button>
      <button class="scenario-tab" onclick="showScenario('coordinators', this)">Programme Coordinators</button>
    </div>

    <div class="scenario-panel active" id="scenario-learners">
      <div class="scenario-panel-head">
        <i class="ph ph-student scenario-icon"></i>
        <span class="scenario-title">Learners</span>
      </div>
      <p>Self-paced learning is easy to start and easy to abandon. Spurti changes the daily experience: learners see their SP balance, know which actions earned points, and can feel the cost of falling behind before it gets hard to recover.</p>
      <p>Students who can see their own engagement patterns are more likely to fix them before the deadline, not after it.</p>
      <span class="scenario-stat"><i class="ph ph-trend-up"></i> Engagement tracked through the course, not just at the end</span>
    </div>

    <div class="scenario-panel" id="scenario-instructors">
      <div class="scenario-panel-head">
        <i class="ph ph-chalkboard-teacher scenario-icon"></i>
        <span class="scenario-title">Instructors</span>
      </div>
      <p>An instructor running a course can see which students are keeping up and which have gone quiet, without waiting for an assignment due date to find out.</p>
      <p>SP trends show early disengagement. A student losing points steadily over two weeks looks different from one who dips and bounces back. Spurti makes that visible while there is still time to do something about it.</p>
      <span class="scenario-stat"><i class="ph ph-bell-ringing"></i> Early signals before mid-course dropout</span>
    </div>

    <div class="scenario-panel" id="scenario-coordinators">
      <div class="scenario-panel-head">
        <i class="ph ph-chart-bar scenario-icon"></i>
        <span class="scenario-title">Programme Coordinators</span>
      </div>
      <p>At the programme level, Spurti aggregates engagement data across entire cohorts. Coordinators can see which modules are holding attention and which are losing learners while the programme is still running, not after it wraps up.</p>
      <p>That kind of signal shapes what gets taught next, not just what gets reported.</p>
      <span class="scenario-stat"><i class="ph ph-buildings"></i> Cohort-level analytics during the programme</span>
    </div>
  </div>
</div>

<div class="product-page-section">
  <h2>Where It's Going</h2>
  <p>An integration API that lets organisations push their own data straight into the scoring engine through per-course keys, so any platform can feed Spurti without custom work.</p>

  <div class="roadmap">
    <div class="roadmap-item">
      <div class="roadmap-status"><span class="rm-badge rm-live">Live</span></div>
      <div class="roadmap-body">
        <div class="roadmap-title">Automated SP system with full analytics</div>
        <div class="roadmap-desc">Spurti Points assigned for attendance, polls, peer teaching, and queries. Live leaderboards, achievement cards, and an admin dashboard, all computed automatically on every scoring run.</div>
      </div>
    </div>
    <div class="roadmap-item">
      <div class="roadmap-status"><span class="rm-badge rm-progress">In Progress</span></div>
      <div class="roadmap-body">
        <div class="roadmap-title">LTI 1.3 integration</div>
        <div class="roadmap-desc">Single sign-on, roster sync, and grade passback built and tested against a live LMS. Deep linking is next, after which Spurti embeds directly into any LTI-compatible platform.</div>
      </div>
    </div>
    <div class="roadmap-item">
      <div class="roadmap-status"><span class="rm-badge rm-upcoming">Upcoming</span></div>
      <div class="roadmap-body">
        <div class="roadmap-title">Integration API for third-party platforms</div>
        <div class="roadmap-desc">Per-course API keys that let any platform push engagement data into the Spurti scoring engine without custom integration work on either side.</div>
      </div>
    </div>
    <div class="roadmap-item">
      <div class="roadmap-status"><span class="rm-badge rm-upcoming">Research</span></div>
      <div class="roadmap-body">
        <div class="roadmap-title">What effort signals actually predict</div>
        <div class="roadmap-desc">Every Spurti cohort generates data on which engagement patterns correlate with learning outcomes. The research question: what does consistent SP accumulation actually predict, and which actions matter most?</div>
      </div>
    </div>
  </div>
</div>

<script>
function showScenario(id, btn) {
  document.querySelectorAll('.scenario-panel').forEach(function(p) { p.classList.remove('active'); });
  document.querySelectorAll('.scenario-tab').forEach(function(t) { t.classList.remove('active'); });
  document.getElementById('scenario-' + id).classList.add('active');
  btn.classList.add('active');
}
</script>

<a href="https://github.com/vicharanashala/spurti" target="_blank" rel="noopener" class="product-github-card">
  <i class="ph ph-github-logo"></i>
  <span>View source on GitHub ↗</span>
</a>
