# Vox Menthe — Jekyll Site

This repository backs <https://voxmenthe.github.io>. It now uses a small, custom Jekyll theme that keeps the typography and layout close to the clean feel of [mrinalxblog](https://mrinalxblog.com).

## Local development

1. Install a recent Ruby (3.2+ recommended) and Bundler.
   ```bash
   gem install bundler
   ```
2. Install the site dependencies.
   ```bash
   bundle install
   ```
3. Run the development server.
   ```bash
   bundle exec jekyll build
   bundle exec jekyll serve --livereload
   ```

The generated site lives in `_site/` and will rebuild automatically when files change.

## Keeping Jekyll up to date

- Update the gem versions in `Gemfile` when new releases ship. This build currently targets:
  - `jekyll 4.3.x`
  - `jekyll-feed 0.17.x`
  - `jekyll-seo-tag 2.8.x`
  - `jekyll-sitemap 1.4.x`
- Refresh the lockfile after changing versions:
  ```bash
  bundle update
  ```
- If GitHub Pages needs the GitHub Actions build step, add a workflow that runs `bundle exec jekyll build` and deploys the `_site/` folder. (The default Pages builder will also work with this Gemfile.)

## Content

- Posts live in `_posts/` and publish automatically based on the `date` in their front matter.
- `index.md` controls the short introduction on the landing page, while `about.md` powers the About page.
- `assets/css/site.css` holds the complete styling for the site. Keep the design minimal—small changes there ripple site-wide.
