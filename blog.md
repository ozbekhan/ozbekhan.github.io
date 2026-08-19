---
layout: page
title: Blog
subtitle: Tüm blog yazıları
---

<div class="posts-list">
  {% for post in site.posts %}
    <article class="post-preview">
      <a href="{{ post.url | relative_url }}">
        <h2 class="post-title">{{ post.title }}</h2>
        {% if post.subtitle %}
          <h3 class="post-subtitle">{{ post.subtitle }}</h3>
        {% endif %}
      </a>

      <p class="post-meta">
        Yayınlanma tarihi: {{ post.date | date: "%d.%m.%Y" }}
      </p>

      
    </article>
    <hr>
  {% endfor %}
</div>
