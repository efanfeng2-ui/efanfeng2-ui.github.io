# Agent Guidelines — Yifan Feng's academic website

**Read this before editing.** This is a personal academic website built on the
[al-folio](https://github.com/alshedivat/al-folio) v1.x starter, deployed to GitHub Pages at
**https://efanfeng2-ui.github.io**.

The build plan — positioning, page-by-page content specs, English copy drafts, and a list of
facts the site owner still needs to verify — lives in [`WEBSITE_PLAN.md`](WEBSITE_PLAN.md).
**Read it before writing site content.**

## This is a site, not the al-folio repo

`docs/`, and the upstream rules they describe, were written for the **al-folio starter repo
itself**. Three of those rules do not apply here, and following them will cause errors:

| Upstream rule                                      | Here                                                                                                                    |
| -------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| "effective baseurl is `/al-folio`"                 | **`baseurl` is blank.** This is a user site at a root domain. Build with a plain `bundle exec jekyll build`.            |
| "never create `_layouts/`, `_includes/`, `_sass/`" | A user site **may** legally shadow gem-owned files. Prefer config/content first, but overrides are allowed when needed. |
| "run `test/integration_*.sh`"                      | Removed — those test al-folio itself.                                                                                   |

Everything in `docs/` remains a useful **reference** for how the gems work. Just don't treat it
as this repo's contract.

## Rules that do apply

1. **`Gemfile` and `_config.yml` are two lists that must agree.** A plugin present in only one of
   them is inert and fails **silently** — no warning, no error. Repo dirs use hyphens
   (`al-folio-core`); gem ids use underscores (`al_folio_core`).
2. **Runtime lives in gems.** Layouts, includes, Sass, Liquid tags, and feature JS come from the
   versioned `al_*` gems. Upgrade by bumping versions in `Gemfile`, not by editing vendored files.
3. **Features fail silently.** A feature renders only when its gem is loaded _and_ its flag is on
   _and_ the page opts in. If something renders as nothing, check all three.
4. If you do shadow a gem-owned file, run `bundle exec al-folio upgrade overrides audit` and commit
   `.al-folio-overrides.yml`.

## Toolchain

Ruby is pinned by `.ruby-version` and matches the version `deploy.yml` uses in CI.

| Component   | Version | Notes                                                         |
| ----------- | ------- | ------------------------------------------------------------- |
| Ruby        | 3.3.5   | via `rbenv`; shell has no `rbenv init`, so shims need PATH    |
| Bundler     | 4.0.6   | required by `Gemfile.lock`                                    |
| Node        | any     | `npm ci` for prettier + tailwind                              |
| ImageMagick | 7.x     | **required** — al-folio generates responsive `.webp` variants |

`rbenv init` is not configured in this shell. Prefix commands with:

```bash
export PATH="$HOME/.rbenv/shims:$PATH"
```

## Validated command set

Run from the repo root:

```bash
export PATH="$HOME/.rbenv/shims:$PATH"
bundle install
npm ci
bundle exec jekyll build                      # baseurl is blank — do not pass --baseurl
bundle exec jekyll serve                      # http://localhost:4000
npx prettier . --write                        # lint:prettier checks; this fixes
bundle exec al-folio upgrade audit --no-fail  # expect "Blocking: 0"
```

**Never trust a piped exit code.** `bundle install | tail` reports `tail`'s status, not
bundler's — this masked a real failure once already. Redirect to a log and echo `$?` instead.

## What was changed from the stock starter

- **Workflows pruned to 5**: `deploy.yml`, `render-cv.yml`, `update-citations.yml`,
  `upgrade-check.yml`, `broken-links-site.yml`. The other 17 were al-folio's own dev/release CI.
- **Demo content removed**: all 33 `_posts/`, `assets/jupyter/`, `readme_preview/`,
  `lighthouse_results/`, `test/`.
- **`external_sources` emptied** — the stock config fetched al-folio's Medium RSS at build time.
- **Nav** is Research (1) · Publications (2) · CV (3) · Teaching (4) · Toolbox (5). `blog` and
  `projects` are `nav: false` but still build.
- **One local gem override**: `_sass/_themes.scss` shadows `al_folio_core`'s copy to set the
  Virginia Tech maroon palette. Only the four theme/hover color lines differ — keep it that way so
  gem updates stay diffable. It is recorded in `.al-folio-overrides.yml`; after touching it run
  `bundle exec al-folio upgrade overrides audit` and re-accept.

Demo content still present in `_news/`, `_projects/`, `_books/`, `_teachings/`, and
`_bibliography/papers.bib` — replace it rather than leaving it live.

## Content rules for this site

- **Species names are always italic**: _Culex pipiens_, _Aedes aegypti_, _Aedes albopictus_.
  Getting this wrong is a credibility problem with the academic audience.
- **Never present an in-preparation manuscript as published.** Use the `abbr` BibTeX field to mark
  status. See `WEBSITE_PLAN.md` §1.1 — the _Aedes aegypti_ paper **is** published (GBE 2025,
  doi:10.1093/gbe/evaf118); do not revert it to a bioRxiv preprint citation.
- Site copy is **English**. Planning docs and conversation are Chinese.
