# efanfeng2-ui.github.io

Personal academic website of **Yifan Feng** — Ph.D. candidate in Entomology at Virginia Tech,
studying chromosomal inversions and genome evolution in mosquitoes.

Live at **https://efanfeng2-ui.github.io**

Built on the [al-folio](https://github.com/alshedivat/al-folio) Jekyll starter, deployed to GitHub
Pages by GitHub Actions on every push to `main`.

## Local development

Requires Ruby 3.3.5 (pinned in `.ruby-version`), Node, and ImageMagick.

```bash
export PATH="$HOME/.rbenv/shims:$PATH"   # this shell has no rbenv init
bundle install
npm ci
bundle exec jekyll serve                  # http://localhost:4000
```

## Where things live

| Path                       | What                                                     |
| -------------------------- | -------------------------------------------------------- |
| `_config.yml`              | Site metadata, feature flags, plugin activation          |
| `_pages/`                  | Top-level pages (about, publications, CV, teaching)      |
| `_bibliography/papers.bib` | Publications — BibTeX drives the publications page       |
| `_data/cv.yml`             | Structured CV; `render-cv.yml` renders it to PDF on push |
| `_news/`                   | Short announcements shown on the homepage                |
| `assets/`                  | Images, PDFs, documents                                  |
| `WEBSITE_PLAN.md`          | Build plan: positioning, page specs, phased roadmap      |
| `AGENTS.md`                | Guidance for coding agents working in this repo          |

## License

Site content © Yifan Feng. The underlying al-folio theme is MIT licensed — see `LICENSE`.
