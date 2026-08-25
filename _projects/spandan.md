---
layout: default
title: Spandan
parent: Products
order: 2
permalink: /projects/spandan/
quote: "Learning is not a spectator sport."
quote_author: "D. Blocher"
---

<div class="initiative-page-hero product-page-hero">
  <a href="{{ site.baseurl }}/products/" class="initiative-back"><i class="ph ph-arrow-left"></i> Products</a>
  <p class="story-label"><i class="ph ph-pulse"></i> Products</p>
  <h1 class="initiative-page-h">Spandan</h1>
</div>

{% include page-quote.html %}

<div class="product-page-meta">
  <span class="product-page-status">Deployed</span>
  <a href="https://spandan.fun/spandan" target="_blank" rel="noopener" class="product-try-link">Try it now ↗</a>
</div>

<p class="product-page-tagline">Real-time classroom engagement — the lecture is heard, questions are generated, and the teacher decides what students see.</p>

<div class="product-page-section">
  <h2>The Problem</h2>
  <p>In live classrooms — online or physical — there is no reliable way to know if students are following along while teaching is happening. Traditional tools like polls or quizzes break the flow: they need to be prepared in advance, demand extra attention from an instructor already managing an entire room, and fail to adapt to what is actually being taught at that moment.</p>
</div>

<div class="product-page-section">
  <h2>What We Built</h2>
  <p>Spandan listens to the instructor's live speech, transcribes it, and generates questions grounded in exactly what was just said. The teacher sees them first — approving or discarding before anything goes out. Students respond on their phones, and the room sees results and a live leaderboard update in real time, while the class is still in session.</p>

  <div class="sdl-wrap">
    <div class="sdl-bar">
      <span class="sdl-dot"></span>
      <span class="sdl-bar-label">Session Live</span>
      <span class="sdl-bar-status" id="sdl-status">Listening</span>
    </div>
    <div class="sdl-cols">
      <div class="sdl-left">
        <div class="sdl-waveform">
          <span class="sdl-wb"></span><span class="sdl-wb"></span><span class="sdl-wb"></span>
          <span class="sdl-wb"></span><span class="sdl-wb"></span><span class="sdl-wb"></span>
          <span class="sdl-wb"></span>
        </div>
        <div class="sdl-transcript" id="sdl-tx"><span class="sdl-cursor">|</span></div>
      </div>
      <div class="sdl-right">
        <div id="sdl-gen">
          <div class="sdl-shimmer-line"></div>
          <div class="sdl-shimmer-line sdl-sh2"></div>
          <div class="sdl-gen-note">Generating question...</div>
        </div>
        <div id="sdl-q" style="display:none">
          <div class="sdl-q-badge">Question ready</div>
          <div class="sdl-q-text" id="sdl-qtext"></div>
          <div class="sdl-q-btns">
            <button class="sdl-approve" onclick="sdlApprove()"><i class="ph ph-check"></i> Send to class</button>
            <button class="sdl-skip" onclick="sdlSkip()">Skip</button>
          </div>
        </div>
        <div id="sdl-res" style="display:none">
          <div class="sdl-res-note">24 students responded</div>
          <div>
            <div class="sdl-brow"><span class="sdl-opt">A</span><div class="sdl-track"><div class="sdl-fill" id="sdl-f0"></div></div><span class="sdl-pct" id="sdl-p0"></span></div>
            <div class="sdl-brow"><span class="sdl-opt">B</span><div class="sdl-track"><div class="sdl-fill" id="sdl-f1"></div></div><span class="sdl-pct" id="sdl-p1"></span></div>
            <div class="sdl-brow"><span class="sdl-opt">C</span><div class="sdl-track"><div class="sdl-fill" id="sdl-f2"></div></div><span class="sdl-pct" id="sdl-p2"></span></div>
            <div class="sdl-brow"><span class="sdl-opt">D</span><div class="sdl-track"><div class="sdl-fill" id="sdl-f3"></div></div><span class="sdl-pct" id="sdl-p3"></span></div>
          </div>
          <div class="sdl-lb">
            <div class="sdl-lb-title">Leaderboard</div>
            <div class="sdl-lb-row"><span class="sdl-rank">1</span><span class="sdl-name">Rohit Sharma</span><span class="sdl-score" id="sdl-sc0"></span></div>
            <div class="sdl-lb-row"><span class="sdl-rank">2</span><span class="sdl-name">Sakshi Sharma</span><span class="sdl-score" id="sdl-sc1"></span></div>
            <div class="sdl-lb-row"><span class="sdl-rank">3</span><span class="sdl-name">Tanvish Desai</span><span class="sdl-score" id="sdl-sc2"></span></div>
            <div class="sdl-lb-row"><span class="sdl-rank">4</span><span class="sdl-name">Aman Sagar</span><span class="sdl-score" id="sdl-sc3"></span></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<div class="product-page-section">
  <h2>In the Room</h2>
  <p>Spandan works best in large rooms where one person is teaching many — the settings where the gap between teaching and feedback is widest.</p>

  <div class="scenario-tabs">
    <div class="scenario-tab-bar">
      <button class="scenario-tab active" onclick="showScenario('internship', this)">Online Internship</button>
      <button class="scenario-tab" onclick="showScenario('fdp', this)">Faculty Development</button>
      <button class="scenario-tab" onclick="showScenario('workshops', this)">Workshops</button>
    </div>

    <div class="scenario-panel active" id="scenario-internship">
      <div class="scenario-panel-head">
        <i class="ph ph-graduation-cap scenario-icon"></i>
        <span class="scenario-title">Samagama Online Internship</span>
      </div>
      <p>Spandan was used in the Samagama online internship, a cohort of over 2,000 learners attending live sessions remotely. In a fully online setting, the gap between teaching and feedback is even wider. No raised hands, no visible faces, no ambient read of the room.</p>
      <p>Spandan filled that gap. Sessions with live question generation and a real-time leaderboard turned passive watching into active participation, and gave coordinators a clear signal on whether the content was landing while the session was still running.</p>
      <span class="scenario-stat"><i class="ph ph-users"></i> 2,000+ learners across Samagama cohorts</span>
    </div>

    <div class="scenario-panel" id="scenario-fdp">
      <div class="scenario-panel-head">
        <i class="ph ph-chalkboard-teacher scenario-icon"></i>
        <span class="scenario-title">Faculty Development Programmes</span>
      </div>
      <p>FDPs bring together faculty from multiple institutions for intensive, structured learning. The audience is expert, the content is dense, and the stakes of losing the room are high. Spandan lets the facilitator take the temperature of the group without slowing down.</p>
      <p>Questions grounded in what was just said test whether participants are tracking the argument — not general subject knowledge they arrived with.</p>
      <span class="scenario-stat"><i class="ph ph-buildings"></i> Used across CBPAI cohorts</span>
    </div>

    <div class="scenario-panel" id="scenario-workshops">
      <div class="scenario-panel-head">
        <i class="ph ph-lightning scenario-icon"></i>
        <span class="scenario-title">Structured Workshops</span>
      </div>
      <p>Workshops often have mixed audiences — some participants following closely, others less so. Spandan surfaces that spread without singling anyone out. The session record shows which explanations held and which ones didn't, across the whole room.</p>
      <p>Each session builds a record of what was asked, when, and how the room responded. Over time this becomes a picture of the teaching — not a report on individual students.</p>
      <span class="scenario-stat"><i class="ph ph-chart-bar"></i> Session analytics included</span>
    </div>
  </div>
</div>

<div class="product-page-section">
  <h2>Where It's Going</h2>
  <p>The live demo above is what exists today. Here's what the lab is actively building toward.</p>

  <div class="roadmap">
    <div class="roadmap-item">
      <div class="roadmap-status"><span class="rm-badge rm-live">Live</span></div>
      <div class="roadmap-body">
        <div class="roadmap-title">Live classroom listening and engagement</div>
        <div class="roadmap-desc">Listens to the teacher in a live classroom and generates a variety of questions from the running transcript. Engagement is tested while the session is still going. Teacher approves before anything reaches students.</div>
      </div>
    </div>
    <div class="roadmap-item">
      <div class="roadmap-status"><span class="rm-badge rm-progress">In Progress</span></div>
      <div class="roadmap-body">
        <div class="roadmap-title">Offline classroom experiments</div>
        <div class="roadmap-desc">Running experiments in physical, offline classrooms for initial deployment. Settings without reliable internet need Spandan to work differently at the listening and question generation layer.</div>
      </div>
    </div>
    <div class="roadmap-item">
      <div class="roadmap-status"><span class="rm-badge rm-upcoming">Upcoming</span></div>
      <div class="roadmap-body">
        <div class="roadmap-title">Co-hosting</div>
        <div class="roadmap-desc">Multiple instructors sharing a single session, each contributing to the question pool. Relevant for panel sessions, team-taught courses, and FDPs where more than one expert is in the room.</div>
      </div>
    </div>
    <div class="roadmap-item">
      <div class="roadmap-status"><span class="rm-badge rm-upcoming">Research</span></div>
      <div class="roadmap-body">
        <div class="roadmap-title">Question quality research</div>
        <div class="roadmap-desc">What makes a question genuinely useful in a live classroom — novel enough to reward attention, precise enough to be tied to this session? Every session contributes to the dataset.</div>
      </div>
    </div>
  </div>
</div>

<script src="{{ site.baseurl }}/assets/js/spandan-demo.js"></script>
<script>
function showScenario(id, btn) {
  document.querySelectorAll('.scenario-panel').forEach(function(p) { p.classList.remove('active'); });
  document.querySelectorAll('.scenario-tab').forEach(function(t) { t.classList.remove('active'); });
  document.getElementById('scenario-' + id).classList.add('active');
  btn.classList.add('active');
}
</script>

<a href="https://github.com/vicharanashala/spandan" target="_blank" rel="noopener" class="product-github-card">
  <i class="ph ph-github-logo"></i>
  <span>View source on GitHub ↗</span>
</a>
