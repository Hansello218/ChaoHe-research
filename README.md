# Chao He — Academic Homepage

Personal academic website for **Chao He**, built with Jekyll and the plugin-based
al-folio v1 starter. Canonical URL: <https://hansello218.github.io/ChaoHe-research/>.

## Local preview

This checkout has an isolated Ruby 3.3 / Node 22 toolchain in ignored `.tools/ruby`:

```bash
cd /home/chao/Downloads/workplace/code/Hansello218.github.io
export PATH="$PWD/.tools/ruby/bin:$PATH"
bundle exec jekyll serve --no-watch --host 127.0.0.1 --port 4000
```

Open <http://127.0.0.1:4000/ChaoHe-research/>. Stop and restart after edits (`--no-watch` avoids
upstream agent-skill symlink watcher warnings). On another machine, install Ruby
3.3 and Bundler 4.0.6, then `bundle install` and `npm ci` before previewing.

```bash
JEKYLL_ENV=production bundle exec jekyll build
npm run lint:prettier
bundle exec al-folio upgrade audit
bundle exec al-folio upgrade overrides audit
```

No notebooks are used; an optional `jupyter-nbconvert` warning does not affect
these pages. Build output is `_site/` (ignored). Keep `baseurl: /ChaoHe-research`; do not pass `/al-folio` or an empty baseurl.

## Content and maintenance

See [site maintenance and deployment](docs/SITE_MAINTENANCE.md) for publication
fields, future projects/CV, precise GitHub settings, and validation results.
Read [AGENTS.md](AGENTS.md) and [research notes](RESEARCH_NOTES.md) before substantial
changes. The original framework documentation remains under `docs/`.

The website currently contains exactly three authorized publications: Endo-GSG,
Endo-4SRF, and the accepted ROBIO paper on universal robot kinematic modeling.
No portrait, CV, research teaser, or unconfirmed author metadata is included.
