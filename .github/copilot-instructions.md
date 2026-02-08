<!-- copilot-instructions for AI coding agents -->
# Copilot / AI agent instructions — www.brianbelow.net

Purpose: Give a concise, actionable summary so an AI agent can make safe, high-value edits to this small Jekyll site.

Big picture
- This is a simple Jekyll-powered static blog site. Key runtime pieces are the site config (_config.yml), the primary layout (_layouts/default.html), content pages (e.g. index.html, about.md), and the SCSS source at assets/main.scss which Jekyll processes.
- Posts are expected in the standard Jekyll _posts/ location and surfaced in the home loop: the home template iterates `site.posts` to render entries.

Key files to read before editing
- _config.yml — site-wide settings (markdown engine = kramdown, permalink: /:year/:title/)
- _layouts/default.html — main HTML shell; links the compiled stylesheet at /assets/css/main.css
- index.html — homepage loop; shows which post front-matter fields are used (title, description, image, excerpt)
- about.md — example page using front-matter and `permalink`
- assets/main.scss — single SCSS entry with YAML front-matter (Jekyll will compile this to CSS)

Patterns & conventions (project-specific)
- Liquid templates: prefer using existing page variables (page.title, page.description). Example: the home loop uses `post.title`, `post.description`, and conditionally `post.image`.
- Post front-matter fields expected by templates: `title`, `description`, optional `image`. If no image, the template falls back to rendering an excerpt.
- SCSS entry file contains YAML front-matter (--- ---) so Jekyll will process it; edits to assets/main.scss change the compiled /assets/css/main.css referenced by the layout.
- Permalinks follow the configured pattern from _config.yml; do not change permalinks without updating links and any external references.

Developer workflows / useful commands
- Local preview (if Ruby/Jekyll installed):

  gem install jekyll bundler
  jekyll serve --livereload

  Or, if there is a Gemfile in future, use:
  bundle exec jekyll serve --livereload

- Build output appears in _site/ by default. Verify generated URLs, compiled CSS, and that posts appear under the expected permalinks.

What to change (and what to avoid)
- Safe: small edits to page content (about.md), Liquid templates in _layouts, adding or editing posts in _posts/, and style tweaks in assets/main.scss.
- Cautious: changing _config.yml settings (permalinks, markdown engine) or moving the SCSS path — these affect site URLs and build output; call out these changes prominently in PR descriptions.

Concrete examples from this repo
- Home loop (index.html): iterates `site.posts` and expects `post.title`, `post.description`, `post.image`, and `post.excerpt`.
- Layout ( _layouts/default.html ) links stylesheet at `/assets/css/main.css` — do not change the output path without adjusting the layout.

Edit style for PRs
- Keep edits small and focused. For visual or CSS changes, include before/after screenshots or a quick note how this was validated with `jekyll serve`.
- When adding a new post, include front-matter: `layout`, `title`, `description`, and optional `image`.

If anything here is unclear or you want more examples (e.g., a sample post in _posts/), tell me which area to expand and I will update this file.
