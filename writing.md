---
layout: default
title: Writing
permalink: /writing/
description: Essays and research notes by Nilakshan Kunananthaseelan.
published: false
---
<header class="page-intro">
  <p class="eyebrow">Writing</p>
  <h1>Notes from the <em>workbench</em>.</h1>
  <p class="lede">Occasional essays on multimodal learning, research practice, and what experiments reveal when they refuse to match the hypothesis.</p>
</header>

{% assign writing_posts = site.posts | where_exp: "post", "post.categories contains 'writing'" %}
<section class="writing-list" aria-label="Essays">
  {% if writing_posts.size > 0 %}
    {% for post in writing_posts %}
      <article class="writing-item">
        <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: '%Y · %b %d' }}</time>
        <div>
          <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
          {% if post.description %}<p>{{ post.description }}</p>{% endif %}
        </div>
      </article>
    {% endfor %}
  {% else %}
    <div class="empty-state">
      <p class="empty-state__mark" aria-hidden="true">∴</p>
      <h2>The notebook is open.</h2>
      <p>The first long-form note is in progress. In the meantime, my publications contain the finished arguments.</p>
      <a class="text-link" href="{{ '/research/' | relative_url }}">Read the research →</a>
    </div>
  {% endif %}
</section>
