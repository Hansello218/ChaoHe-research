---
layout: academic
title: About
permalink: /
---

<header class="introduction">
  <p class="research-descriptor">Computer Vision &amp; Computer Graphics</p>
  <h1>Chao He</h1>
  <div class="biography">
    <p>I graduated from Soochow University. My research interests lie in computer vision and computer graphics, with a particular focus on 3D/4D reconstruction, Gaussian Splatting, physics-based simulation, and surgical robotics.</p>
    <p>I am interested in developing geometry-aware and physics-informed methods for reconstructing, understanding, and simulating dynamic 3D environments.</p>
  </div>
  <div class="contact-links" aria-label="Contact">
    <a href="mailto:{{ site.data.socials.email }}"><svg viewBox="0 0 24 24" aria-hidden="true"><rect x="3" y="5" width="18" height="14" rx="2"/><path d="m3 6 9 7 9-7"/></svg>Email</a>
    <a href="https://github.com/{{ site.data.socials.github_username }}" target="_blank" rel="noopener noreferrer"><svg viewBox="0 0 24 24" aria-hidden="true"><path d="M9 19c-4 1-4-2-6-2m12 5v-4a3.5 3.5 0 0 0-1-3c3-.3 6-1.5 6-6a5 5 0 0 0-1.4-3.5A4.7 4.7 0 0 0 18.5 2S17.3 1.7 15 3a13 13 0 0 0-6 0C6.7 1.7 5.5 2 5.5 2a4.7 4.7 0 0 0-.1 3.5A5 5 0 0 0 4 9c0 4.5 3 5.7 6 6a3.5 3.5 0 0 0-1 3v4"/></svg>GitHub <span aria-hidden="true">↗</span></a>
  </div>
</header>

<section class="research-interests" aria-labelledby="interests-heading">
  <h2 id="interests-heading">Research Interests</h2>
  <ul><li>3D/4D Reconstruction</li><li>Gaussian Splatting</li><li>Physics-based Simulation</li><li>Surgical Robotics</li></ul>
</section>

<section class="news-section" aria-labelledby="news-heading">
  <h2 id="news-heading">News</h2>
  <ul class="news-list">
    {% for item in site.data.news %}<li><span class="news-year">{{ item.year }}</span><span><a href="{{ item.url }}" target="_blank" rel="noopener noreferrer">{{ item.text }}</a></span></li>{% endfor %}
  </ul>
</section>

<section aria-labelledby="publications-heading">
  <div class="section-heading"><h2 id="publications-heading">Selected Publications</h2><a href="{{ '/publications/' | relative_url }}">All publications <span aria-hidden="true">→</span></a></div>
  {% include publication-list.liquid %}
</section>
