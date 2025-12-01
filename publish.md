---
layout: default
title: Publish research
---

<section class="publish-section">
  <header class="publish-header">
    <h1 class="article-title">Publish new research</h1>
    <p class="publish-subtitle">
      Use this form to draft a note. We’ll generate the markdown front matter for you — then you can
      paste it into the repository so it appears on the dashboard and gets a Word document.
    </p>
  </header>

  <div class="publish-grid">
    <form class="publish-form" onsubmit="return false;">
      <div class="field">
        <label for="pub-title">Title</label>
        <input id="pub-title" type="text" placeholder="Saudi Banks: NIM Risk in 2026">
      </div>

      <div class="field field-row">
        <div class="field">
          <label for="pub-author">Author name</label>
          <input id="pub-author" type="text" placeholder="Nadir Rahman">
        </div>
        <div class="field">
          <label for="pub-author-id">Author ID (short code)</label>
          <input id="pub-author-id" type="text" placeholder="nadir">
        </div>
      </div>

      <div class="field field-row">
        <div class="field">
          <label for="pub-category">Asset class</label>
          <select id="pub-category">
            <option value="equities">Equities</option>
            <option value="fixed-income">Fixed income</option>
            <option value="macro">Macro</option>
            <option value="commodities">Commodities</option>
          </select>
        </div>
        <div class="field">
          <label>
            <input id="pub-featured" type="checkbox">
            Show in “Trending research”
          </label>
        </div>
      </div>

      <div class="field">
        <label for="pub-summary">Short summary (1–3 lines)</label>
        <textarea id="pub-summary" rows="3"
          placeholder="We look at how higher-for-longer rates and funding mix shifts may pressure NIMs in 2026."></textarea>
      </div>

      <div class="field">
        <label for="pub-body">Main body (Markdown)</label>
        <textarea id="pub-body" rows="10"
          placeholder="# Investment thesis&#10;&#10;Write your note here in markdown..."></textarea>
      </div>

      <button type="button" class="hero-btn" onclick="generateMarkdown()">
        Generate markdown
      </button>
    </form>

    <div class="publish-preview">
      <h2 class="dashboard-heading">Generated markdown</h2>
      <p class="publish-help">
        Step 2: copy all of this into a new file in <code>_posts</code> on GitHub
        (e.g. <code>2025-12-05-slug-here.md</code>) and commit.
      </p>
      <textarea id="pub-output" readonly></textarea>
      <p class="publish-help">
        Tip: file names must be <code>YYYY-MM-DD-your-slug.md</code> for Jekyll to pick them up.
      </p>
    </div>
  </div>
</section>

<script>
function slugify(str) {
  return (str || "")
    .toLowerCase()
    .trim()
    .replace(/[^a-z0-9]+/g, "-")
    .replace(/^-+|-+$/g, "");
}

function generateMarkdown() {
  const title = document.getElementById('pub-title').value.trim();
  const author = document.getElementById('pub-author').value.trim();
  const authorId = document.getElementById('pub-author-id').value.trim();
  const category = document.getElementById('pub-category').value;
  const featured = document.getElementById('pub-featured').checked;
  const summary = document.getElementById('pub-summary').value.trim();
  const body = document.getElementById('pub-body').value.trim();

  let frontMatter = "---\n";
  frontMatter += "layout: post\n";
  if (title) frontMatter += `title: "${title.replace(/"/g, '\\"')}"\n`;
  if (author) frontMatter += `author: "${author.replace(/"/g, '\\"')}"\n`;
  if (authorId) frontMatter += `author_id: "${authorId}"\n`;
  frontMatter += `category: "${category}"\n`;
  if (summary) frontMatter += `summary: "${summary.replace(/"/g, '\\"')}"\n`;
  frontMatter += `featured: ${featured ? "true" : "false"}\n`;
  frontMatter += "---\n\n";

  const output = frontMatter + (body || "# Investment thesis\n\nWrite your note here…\n");
  document.getElementById('pub-output').value = output;
}
</script>
