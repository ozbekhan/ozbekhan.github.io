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

      <div class="post-entry-container">
        {% if post.excerpt %}
          <div class="post-entry">
            {{ post.excerpt | strip_html | truncatewords: 30 }}
            <a href="{{ post.url | relative_url }}" class="post-read-more">[Devamını Oku]</a>
          </div>
        {% endif %}
      </div>
    </article>
    <hr>
  {% endfor %}
</div>
