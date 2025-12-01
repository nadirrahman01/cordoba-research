---
layout: default
title: Cordoba Capital Research
---

<div class="dashboard-header">
  <div>
    <div class="hero-eyebrow">Cordoba Capital</div>
    <h1 class="hero-title">Research Dashboard</h1>
    <p class="hero-subtitle">
      Internal hub for Cordoba analysts and Visiting Research Analysts to publish and access notes
      across macro, equities, fixed income, commodities, and credit.
    </p>
  </div>

  <div class="publish-wrapper">
    <a class="publish-button"
       href="https://github.com/nadirrahman01/cordoba-research/new/main/_posts"
       target="_blank" rel="noopener">
      + Publish research
    </a>
  </div>
</div>

<section class="dashboard-grid">

  <!-- Left column: latest research -->
  <div class="dashboard-column">
    <h2 class="dashboard-heading">Latest research</h2>

    <div class="posts-grid">
      {% for post in site.posts limit:8 %}
        <article class="post-card">
          <div class="post-meta">
            {{ post.category | upcase }} · {{ post.date | date: "%d %b %Y" }} · {{ post.author }}
          </div>
          <h3 class="post-card-title">
            <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
          </h3>
          {% if post.summary %}
            <p class="post-card-summary">{{ post.summary }}</p>
          {% endif %}
        </article>
      {% endfor %}
    </div>
  </div>

  <!-- Right column: trending / featured research -->
  <div class="dashboard-column dashboard-column-right">
    <h2 class="dashboard-heading">Trending research</h2>

    <div class="posts-grid">
      {% assign featured_posts = site.posts | where_exp:"post", "post.featured == true" %}
      {% if featured_posts.size > 0 %}
        {% for post in featured_posts limit:5 %}
          <article class="post-card">
            <div class="post-meta">
              {{ post.category | upcase }} · {{ post.date | date: "%d %b %Y" }} · {{ post.author }}
            </div>
            <h3 class="post-card-title">
              <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
            </h3>
            {% if post.summary %}
              <p class="post-card-summary">{{ post.summary }}</p>
            {% endif %}
          </article>
        {% endfor %}
      {% else %}
        <p class="no-featured">
          No featured pieces yet. Mark a note with <code>featured: true</code> in the front matter to show it here.
        </p>
      {% endif %}
    </div>
  </div>

</section>
          <p class="post-card-summary">{{ post.summary }}</p>
        {% endif %}
      </article>
    {% endfor %}
  </div>
</section>
