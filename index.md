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

<div class="dashboard-controls">
  <div class="search-wrapper">
    <input id="search-input" type="text" placeholder="Search by title, author, asset class…">
  </div>
  <div class="category-filters">
    <button class="filter-button is-active" data-category="all">All</button>
    <button class="filter-button" data-category="equities">Equities</button>
    <button class="filter-button" data-category="fixed-income">Fixed income</button>
    <button class="filter-button" data-category="macro">Macro</button>
    <button class="filter-button" data-category="commodities">Commodities</button>
  </div>
</div>

<section class="dashboard-grid">

  <!-- Left column: latest research -->
  <div class="dashboard-column">
    <h2 class="dashboard-heading">Latest research</h2>

    <div class="posts-grid latest-posts">
      {% for post in site.posts limit:20 %}
        <article class="post-card"
                 data-category="{{ post.category | downcase }}"
                 data-title="{{ post.title | downcase }}"
                 data-author="{{ post.author | downcase }}"
                 data-summary="{% if post.summary %}{{ post.summary | downcase }}{% endif %}">
          <div class="post-meta">
            {{ post.category | upcase }} · {{ post.date | date: "%d %b %Y" }} ·
            {% if post.author_id %}
              <a href="{{ "/authors/" | append: post.author_id | append: ".html" | relative_url }}">
                {{ post.author }}
              </a>
            {% else %}
              {{ post.author }}
            {% endif %}
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
        {% for post in featured_posts limit:8 %}
          <article class="post-card">
            <div class="post-meta">
              {{ post.category | upcase }} · {{ post.date | date: "%d %b %Y" }} ·
              {% if post.author_id %}
                <a href="{{ "/authors/" | append: post.author_id | append: ".html" | relative_url }}">
                  {{ post.author }}
                </a>
              {% else %}
                {{ post.author }}
              {% endif %}
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

<script>
(function() {
  const searchInput = document.getElementById('search-input');
  const filterButtons = Array.from(document.querySelectorAll('.filter-button'));
  const cards = Array.from(document.querySelectorAll('.latest-posts .post-card'));

  let activeCategory = 'all';

  function normalise(str) {
    return (str || '').toLowerCase();
  }

  function applyFilters() {
    const query = normalise(searchInput.value);

    cards.forEach(card => {
      const cardCategory = card.getAttribute('data-category');
      const title = card.getAttribute('data-title');
      const author = card.getAttribute('data-author');
      const summary = card.getAttribute('data-summary');

      const matchesCategory = (activeCategory === 'all') || (cardCategory === activeCategory);
      const haystack = [title, author, summary, cardCategory].join(' ');
      const matchesSearch = haystack.indexOf(query) !== -1;

      if (matchesCategory && matchesSearch) {
        card.style.display = '';
      } else {
        card.style.display = 'none';
      }
    });
  }

  filterButtons.forEach(btn => {
    btn.addEventListener('click', function() {
      filterButtons.forEach(b => b.classList.remove('is-active'));
      this.classList.add('is-active');
      activeCategory = this.getAttribute('data-category');
      applyFilters();
    });
  });

  if (searchInput) {
    searchInput.addEventListener('input', applyFilters);
  }
})();
</script>
