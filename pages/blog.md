---
layout: page
title: Blog
description: Thoughts on AI, Agents, RL, ML, and Data Science
---

<div class="page-hero">
  <h1>Blog</h1>
  <p class="subtitle">Thoughts on AI, Agents, RL, ML, and Data Science</p>
</div>

<section>
  <div class="section-container">
    <div class="blog-list">
      {% for post in site.posts %}
      <article class="blog-card reveal">
        <div class="blog-card-meta">
          <time>{{ post.date | date: "%B %d, %Y" }}</time>
        </div>
        <h3><a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></h3>
        {% if post.description %}
        <p>{{ post.description }}</p>
        {% endif %}
        {% if post.tags.size > 0 %}
        <div class="blog-card-tags">
          {% for tag in post.tags %}
          <span>{{ tag }}</span>
          {% endfor %}
        </div>
        {% endif %}
        <a href="{{ BASE_PATH }}{{ post.url }}" class="blog-read-more">Read more &rarr;</a>
      </article>
      {% endfor %}
    </div>
  </div>
</section>
