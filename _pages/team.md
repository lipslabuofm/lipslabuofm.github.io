---
title: "LIPS Lab - Team"
layout: gridlay
excerpt: "LIPS Lab: Team members"
sitemap: false
permalink: /team/
---

<div markdown="0" class="team-page-root">
  <div class="team-page">
    <header class="team-page__hero">
      <h1 class="team-page__title">Meet Our Team</h1>
      <p class="team-page__subtitle">
        Researchers advancing natural language processing, semantics, and AI for education.
      </p>
      <p class="team-page__lede">
        We work on intelligent tutoring, assessment, question answering, and language technologies collaborating across NLP, machine learning, and human-centered computing.
      </p>
    </header>

    {% assign pi_members = site.data.team_members | where: "category", "pi" %}
    {% assign phd_members = site.data.team_members | where_exp: "m", "m.category != 'pi'" %}

    <section class="team-page__section" aria-labelledby="team-pi-heading">
      <h2 id="team-pi-heading" class="team-page__section-title">Principal Investigator</h2>
      <div class="team-page__section-rule" aria-hidden="true"></div>
      <div class="team-cards team-cards--pi">
        {% for member in pi_members %}
          {% include team-card.html member=member %}
        {% endfor %}
      </div>
    </section>

    <section class="team-page__section" aria-labelledby="team-phd-heading">
      <h2 id="team-phd-heading" class="team-page__section-title">PhD Students</h2>
      <div class="team-page__section-rule" aria-hidden="true"></div>
      <div class="team-cards">
        {% for member in phd_members %}
          {% include team-card.html member=member %}
        {% endfor %}
      </div>
    </section>

    <section class="team-page__section team-page__section--alumni" aria-labelledby="team-alumni-heading">
      <h2 id="team-alumni-heading" class="team-page__section-title">Alumni</h2>
      <div class="team-page__section-rule" aria-hidden="true"></div>
      <p class="team-page__section-note">Former PhD students and postdocs who worked with the lab.</p>
      <div class="team-cards">
        {% for member in site.data.alumni_members %}
          {% include team-card.html member=member alumni=true %}
        {% endfor %}
      </div>
    </section>
  </div>
</div>
