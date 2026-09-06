---
layout: default
title: Research
permalink: /research/
description: Publications and research questions explored by Nilakshan Kunananthaseelan.
---
<header class="page-intro page-intro--wide">
  <p class="eyebrow">Research</p>
  <h1>Intelligence must adapt—<em>without losing what matters</em>.</h1>
  <p class="lede">My research asks how multimodal models can be adapted efficiently, how they can reason over diverse evidence, and how AI agents can act reliably as their tasks and environments change.</p>
</header>

<section class="research-program" aria-labelledby="program-heading">
  <div class="section-heading">
    <p class="eyebrow">Research programme</p>
    <h2 id="program-heading">Questions guiding my work</h2>
  </div>

  <div class="research-question">
    <p class="research-question__index">01</p>
    <div>
      <h3>How can multimodal models adapt efficiently?</h3>
      <p>I develop parameter-efficient and semantically grounded methods that repurpose foundation models for new domains and tasks. This work spans visual prompting, machine unlearning, retrieval-guided adaptation, and lightweight model updates.</p>
    </div>
  </div>
  <div class="research-question">
    <p class="research-question__index">02</p>
    <div>
      <h3>How can multimodal models reason reliably?</h3>
      <p>I study how models combine visual observations, language, and structured knowledge to reach grounded conclusions. This includes document-understanding systems that must trace answers to evidence and reason consistently across related forms.</p>
    </div>
  </div>
  <div class="research-question">
    <p class="research-question__index">03</p>
    <div>
      <h3>How can AI agents earn trust?</h3>
      <p>I investigate agents that learn from interaction, adapt to changing tasks, expose evidence for their decisions, and preserve useful prior capabilities. The goal is dependable behaviour across the full lifetime of an agent.</p>
    </div>
  </div>
</section>

<section class="all-publications" aria-labelledby="publications-heading">
  <div class="section-heading section-heading--split">
    <div>
      <p class="eyebrow">Publications</p>
      <h2 id="publications-heading">Selected papers</h2>
    </div>
    <a class="text-link" href="https://scholar.google.com/citations?user=5YgCHuEAAAAJ&hl=en">Google Scholar ↗</a>
  </div>

  <div class="publication-list">
    {% for publication in site.data.publications %}
      {% include publication.html publication=publication %}
    {% endfor %}
  </div>
</section>

<aside class="collaboration-note">
  <p class="eyebrow">Collaboration</p>
  <p>I welcome collaborations where a clear technical question meets a consequential real-world application, especially projects that connect new learning methods with careful evaluation.</p>
  <a class="text-link" href="mailto:nilakjhc@gmail.com">Start a conversation ↗</a>
</aside>
