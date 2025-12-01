---
layout: default
title: Cordoba Capital Research
---

<section class="hero">
  <div class="hero-eyebrow">Cordoba Capital</div>
  <h1 class="hero-title">Research Library</h1>
  <p class="hero-subtitle">
    A home for Cordoba analysts and Visiting Research Analysts to publish
    notes across macro, equities, fixed income, commodities, and credit.
  </p>
</section>

<section class="posts-section">
  <div class="posts-heading">Latest from the Desk</div>

  <div class="posts-grid">
    {% for post in site.posts %}
      <article class="post-card">
        <div class="post-meta">
          {{ post.category | upcase }} · {{ post.date | date: "%d %b %Y" }} · {{ post.author }}
        </div>
        <h2 class="post-card-title">
          <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
        </h2>
        {% if post.summary %}
          <p class="post-card-summary">{{ post.summary }}</p>
        {% endif %}
      </article>
    {% endfor %}
  </div>
</section>
          <p class="post-card-summary">{{ post.summary }}</p>
        {% endif %}
      </article>
    {% endfor %}
  </div>
</section>
