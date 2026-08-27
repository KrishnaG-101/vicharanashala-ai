---
layout: default
title: Our Story
permalink: /ourstory/
quote: "Tell me and I forget. Teach me and I remember. Involve me and I learn."
quote_author: "Benjamin Franklin"
---

<div class="story-intro">
  <p class="story-label"><i class="ph ph-book-open"></i> Our Story</p>
  <h1 class="story-h">From one conviction<br>to a national mission.</h1>
  <div class="story-cols">
    <p class="story-lead">Vicharanashala began in July 2023 as a small research initiative at IIT Ropar — a conviction that education could be designed more intentionally, more humanely, and at scale. What started as a single lab has grown into a national effort touching 10,000+ learners, 35+ faculty, and sending over 2,000 internship offer letters across India.</p>
    <p class="story-lead">The name says it all. <em>Vichara</em> means thought, inquiry, reflection. <em>Shala</em> means a hall — a place of gathering. Vicharanashala: a house of thinking where education isn't just delivered, but designed, questioned, and rebuilt from the ground up.</p>
  </div>
</div>

{% include page-quote.html %}

<div class="story-space">
  <p class="story-label"><i class="ph ph-map-pin"></i> The Space</p>
  <h2 class="story-section-h">Where thinking becomes practice.</h2>
  <div class="story-space-grid">
    <div class="story-space-text">
      <p>The lab is based at IIT Ropar in Punjab — one of India's newer IITs, set along the Sutlej in the Shivalik foothills. It's a campus still finding its shape, which suits us: we're building things here too.</p>
      <p>The physical lab is a workspace where whiteboards fill faster than they can be erased, a small team asks large questions, and the gap between research and real classrooms is taken seriously. Ideas don't leave here until they've been tried somewhere.</p>
    </div>
    <div class="story-space-img">
      <img src="{{ site.baseurl }}/assets/images/moments/lab-session.jpeg" alt="The Vicharanashala lab — a working session in progress" class="story-space-photo">
    </div>
  </div>
</div>

<div class="story-reach">
  <p class="story-label"><i class="ph ph-map-pin"></i> Our Reach</p>
  <h2 class="story-section-h">Across India, city by city.</h2>
  <p class="story-reach-desc">Faculty and students reached through our programmes — {{ site.data.reach_cities | size }} cities across 31 states and union territories.</p>
  <div class="story-reach-legend">
    <span class="reach-legend-item"><span class="reach-dot reach-dot-faculty"></span> Faculty</span>
    <span class="reach-legend-item"><span class="reach-dot reach-dot-student"></span> Students</span>
    <span class="reach-legend-item"><span class="reach-dot reach-dot-both"></span> Both</span>
  </div>
  <div id="reach-map"></div>
</div>

<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css"/>
<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

<script>
var cities = [
  {% for city in site.data.reach_cities %}
  { name: "{{ city.city }}", state: "{{ city.state }}", lat: {{ city.lat }}, lng: {{ city.lng }}, type: "{{ city.type }}" }{% unless forloop.last %},{% endunless %}
  {% endfor %}
];

// There is NO basemap here, on purpose. We draw India's outline and nothing
// else, so a dot near the northern border cannot be misread as sitting in
// Nepal or Bhutan — those countries are simply not on the page. Everything
// outside the outline is page background.
// Do not add a tile layer back in without solving that problem first.
// zoomSnap: 0 must be set here, at construction. Leaflet otherwise rounds to
// whole zoom levels, and India needs a fractional one — at zoom 4 the outline
// sits small in the middle of the box, at zoom 5 it overflows.
var map = L.map('reach-map', {
  zoomSnap: 0,
  zoomControl: false, scrollWheelZoom: false, dragging: false,
  doubleClickZoom: false, touchZoom: false, boxZoom: false, keyboard: false,
  attributionControl: false
});

var facultyStyle = { radius: 4, fillColor: '#e07020', color: '#fff', weight: 1, opacity: 1, fillOpacity: 0.9 };
var studentStyle = { radius: 4, fillColor: '#3ab7bf', color: '#fff', weight: 1, opacity: 1, fillOpacity: 0.9 };
var bothStyle    = { radius: 5, fillColor: '#8a5ab7', color: '#fff', weight: 1, opacity: 1, fillOpacity: 0.9 };

function drawCities() {
  cities.forEach(function(c) {
    var style = c.type === 'student' ? studentStyle : c.type === 'both' ? bothStyle : facultyStyle;
    L.circleMarker([c.lat, c.lng], style)
      .bindTooltip('<strong>' + c.name + '</strong><br>' + c.state, { direction: 'top', offset: [0, -6] })
      .addTo(map);
  });
}

fetch('{{ site.baseurl }}/assets/data/india.geojson')
  .then(function(r) { return r.json(); })
  .then(function(geo) {
    var india = L.geoJSON(geo, {
      style: { fillColor: '#efefec', fillOpacity: 1, color: '#d6d5ce', weight: 1 },
      interactive: false
    }).addTo(map);

    // The outline itself defines the view — no hardcoded bounding box to drift
    // out of date, and it re-fits when the window resizes.
    function fit() { map.invalidateSize(); map.fitBounds(india.getBounds(), { padding: [6, 6] }); }
    fit();
    window.addEventListener('resize', fit);

    drawCities();
  })
  .catch(function() {
    // If the outline cannot load, still show the dots rather than an empty box.
    map.setView([22.5, 82.0], 4);
    drawCities();
  });
</script>

<div class="story-timeline-intro">
  <p class="story-label"><i class="ph ph-clock-counter-clockwise"></i> The Timeline</p>
  <h2 class="story-section-h">How we got here.</h2>
</div>

<div class="tl-section" id="tlSection">
  <div class="tl" id="tlTrack">
    <div class="tl-fill" id="tlFill"></div>

    <div class="tl-item">
      <div class="tl-icon">✨</div>
      <div class="tl-date">July 2023</div>
      <div class="tl-title">The Spark</div>
      <div class="tl-desc">A small research initiative started to revolutionise Education Design.</div>
    </div>

    <div class="tl-item">
      <div class="tl-icon">🌼</div>
      <div class="tl-date">October 2024</div>
      <div class="tl-title">DLED is Born</div>
      <div class="tl-desc">On Vijayadasami, the lab was formally named <strong>Dhananjaya Lab for Education Design (DLED)</strong> at IIT Ropar.</div>
    </div>

    <div class="tl-item">
      <div class="tl-icon">🚀</div>
      <div class="tl-date">December 2024</div>
      <div class="tl-title">The CBPAI Journey Begins</div>
      <div class="tl-desc">CBPAI (Chalkboards to Chatbots, Pedagogy and AI), supported by UGC MMTTP, became the lab's first major funded initiative and enabled its national rollout.</div>
    </div>

    <div class="tl-item">
      <div class="tl-icon">🎓</div>
      <div class="tl-date">February 2025</div>
      <div class="tl-title">GuruSetu Launched</div>
      <div class="tl-desc">A re-envisioned ARPIT initiative built on nine thematic pillars, bringing together insights from experts grounded in real classroom experience.</div>
    </div>

    <div class="tl-item">
      <div class="tl-icon">💻</div>
      <div class="tl-date">July 2025</div>
      <div class="tl-title">ViBe Unveiled at ABSS</div>
      <div class="tl-desc">The AI-enabled asynchronous learning platform launched during Akhil Bharatiya Shiksha Samagam, celebrating the fifth anniversary of NEP 2020.</div>
    </div>

    <div class="tl-item">
      <div class="tl-icon">🌿</div>
      <div class="tl-date">October 2025</div>
      <div class="tl-title">DLED becomes Vicharanashala</div>
      <div class="tl-desc">The lab was renamed <strong>Vicharanashala Lab for Education Design</strong>. Spandan also emerged as a real-time classroom engagement platform.</div>
    </div>

    <div class="tl-item">
      <div class="tl-icon">📊</div>
      <div class="tl-date">December 2025</div>
      <div class="tl-title">Vinternship &amp; ViSlides</div>
      <div class="tl-desc">The first national-scale Vinternship welcomed 423 learners, while ViSlides debuted at the ICPE Conference 2025.</div>
    </div>

    <div class="tl-item">
      <div class="tl-icon">🎤</div>
      <div class="tl-date">January 2026</div>
      <div class="tl-title">Global Speaker Series &amp; ViTalks</div>
      <div class="tl-desc">Two new initiatives launched to connect educators, researchers, and practitioners through conversations and expert talks.</div>
    </div>

    <div class="tl-item">
      <div class="tl-icon">💡</div>
      <div class="tl-date">February 2026</div>
      <div class="tl-title">Vi-Chintan</div>
      <div class="tl-desc">Fresh, human perspectives on education and AI through thoughtful reflections, ideas, and conversations.</div>
    </div>

    <div class="tl-item">
      <div class="tl-icon">🌾</div>
      <div class="tl-date">March 2026</div>
      <div class="tl-title">AI with Agriculture Dataset</div>
      <div class="tl-desc">A new course introducing AI through authentic, real-world agriculture datasets and practical applications.</div>
    </div>

    <div class="tl-item">
      <div class="tl-icon">🎒</div>
      <div class="tl-date">May 2026</div>
      <div class="tl-title">Summership Launches</div>
      <div class="tl-desc">The lab's flagship summer internship programme launched with <strong>Samagama</strong> and <strong>Yaksha</strong> — bringing students into the work of education design hands-on.</div>
    </div>

    <div class="tl-item">
      <div class="tl-icon">🌧️</div>
      <div class="tl-date">July 2026</div>
      <div class="tl-title">Monsoonship Begins</div>
      <div class="tl-desc">From 15 July, a part-time internship track opened alongside the lab's work — students contributing through the semester, not only over the summer.</div>
    </div>

    <div class="tl-item tl-next">
      <div class="tl-icon tl-next-icon"><span class="tl-pulse-ring"></span>→</div>
      <div class="tl-date">August–September 2026</div>
      <div class="tl-title">What's Next?</div>
      <div class="tl-desc">Three things are taking shape — <strong>Guru Vaani</strong>, a faculty development programme reaching educators across the country; <strong>Samagra</strong>, a credited internship; and <strong>Teacharcha</strong>, a community space for teachers. The story is still being written.</div>
    </div>

  </div>
</div>

<style>
.tl-section { padding: 0 0 4rem; }

.tl {
  position: relative;
  padding-left: 70px;
  max-width: 700px;
}

.tl::before {
  content: "";
  position: absolute;
  left: 24px;
  top: 0;
  bottom: 0;
  width: 2px;
  background: #e2e2de;
}

.tl-fill {
  position: absolute;
  left: 24px;
  top: 0;
  width: 2px;
  height: 0;
  background: #e07020;
  pointer-events: none;
}

.tl-item {
  position: relative;
  margin-bottom: 56px;
  opacity: 0;
  transform: translateY(30px);
  transition: opacity 0.7s ease, transform 0.7s ease;
}

.tl-item.visible {
  opacity: 1;
  transform: translateY(0);
}

.tl-item.visible:hover {
  transform: translateY(-4px);
  transition: transform 0.22s ease;
}

.tl-icon {
  position: absolute;
  left: -62px;
  top: 4px;
  width: 34px;
  height: 34px;
  border-radius: 50%;
  background: white;
  border: 2px solid #444;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 16px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.06);
  transition: transform 0.22s ease, border-color 0.22s ease;
  z-index: 2;
}

.tl-item.visible:hover .tl-icon {
  transform: scale(1.18);
  border-color: #e07020;
}

.tl-date {
  font-size: 0.78rem;
  font-weight: 500;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: #767676;
  margin-bottom: 5px;
}

.tl-title {
  font-size: 1.15rem;
  font-weight: 700;
  color: #1a1a1a;
  margin-bottom: 8px;
  letter-spacing: -0.01em;
}

.tl-desc {
  font-size: 0.92rem;
  line-height: 1.75;
  color: #555;
  max-width: 560px;
}

.tl-next-icon {
  position: relative;
  border-color: #e07020 !important;
  background: #fff7f2 !important;
  font-size: 14px;
}

@keyframes tlPulse {
  0%   { transform: scale(1); opacity: 0.7; }
  100% { transform: scale(2.4); opacity: 0; }
}

.tl-pulse-ring {
  position: absolute;
  inset: -4px;
  border-radius: 50%;
  border: 2px solid #e07020;
  animation: tlPulse 2s ease-out infinite;
}

@media (max-width: 600px) {
  .tl { padding-left: 52px; }
  .tl::before { left: 18px; }
  .tl-fill { left: 18px; }
  .tl-icon { left: -47px; width: 28px; height: 28px; font-size: 14px; }
  .tl-title { font-size: 1.05rem; }
}
</style>

<script>
(function(){
  var fill = document.getElementById('tlFill');
  var section = document.getElementById('tlSection');

  function updateFill(){
    if(!fill || !section) return;
    var rect = section.getBoundingClientRect();
    var progress = Math.max(0, Math.min(1,
      (window.innerHeight * 0.65 - rect.top) / rect.height
    ));
    fill.style.height = (progress * 100) + '%';
  }

  window.addEventListener('scroll', updateFill, { passive: true });
  updateFill();

  var observer = new IntersectionObserver(function(entries){
    entries.forEach(function(e){
      if(e.isIntersecting) e.target.classList.add('visible');
    });
  }, { threshold: 0.15 });

  document.querySelectorAll('.tl-item').forEach(function(el){
    observer.observe(el);
  });
})();
</script>

<style>
.story-intro {
  padding: 0 0 1.5rem;
  border-bottom: 1px solid #e2e2de;
  margin-bottom: 1.5rem;
}

@media (max-width: 600px) {
  .story-intro {
    padding: 0 0 1rem;
    margin-bottom: 1rem;
  }
}

.story-label {
  font-size: 0.72rem;
  font-weight: 500;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  color: #767676;
  margin-bottom: 1rem;
  display: flex;
  align-items: center;
  gap: 0.4rem;
}

.story-h {
  font-size: clamp(1.8rem, 4vw, 2.6rem);
  font-weight: 600;
  letter-spacing: -0.03em;
  line-height: 1.12;
  margin: 0 0 2rem 0;
}

.story-cols {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2.5rem;
}

.story-lead {
  font-size: 1rem;
  line-height: 1.78;
  color: #444;
  margin: 0;
}

/* Lab space */
.story-space {
  padding: 3rem 0;
  border-bottom: 1px solid #e2e2de;
  margin-bottom: 3.5rem;
}

.story-section-h {
  font-size: 1.4rem;
  font-weight: 600;
  letter-spacing: -0.02em;
  line-height: 1.25;
  margin: 0 0 2rem 0;
}

.story-space-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 3rem;
  align-items: start;
}

.story-space-text p {
  font-size: 0.95rem;
  line-height: 1.78;
  color: #444;
  margin: 0 0 1rem 0;
}

.story-space-text p:last-child { margin-bottom: 0; }

.story-space-img { border-radius: 6px; overflow: hidden; }

.story-space-photo {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
  border-radius: 6px;
}

/* Timeline intro */
.story-timeline-intro { margin-bottom: 0.5rem; }

@media (max-width: 600px) {
  .story-cols,
  .story-space-grid {
    grid-template-columns: 1fr;
    gap: 1.4rem;
  }
}
</style>
