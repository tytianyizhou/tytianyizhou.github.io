# tianyichow-tcs.github.io

Personal academic site + learning log. Built with [Hugo](https://gohugo.io) and the
[PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme (same base as lilianweng.github.io).

## Run locally

```bash
git submodule update --init --recursive   # first time only (fetches the theme)
hugo server -D                            # http://localhost:1313, live reload, shows drafts
```

## Where to edit things

| What | File |
|---|---|
| Name, role, photo, social links, contact | `hugo.yaml` → `params.profile`, `params.socialIcons` |
| Bio paragraph on home page | `content/_index.md` |
| News | `data/news.yaml` |
| Current focus / plans | `data/plans.yaml` |
| Publications (home shows `selected: true`) | `data/publications.yaml` |
| Awards | `data/awards.yaml` |
| Photo / paper thumbnails / CV | `static/images/…`, `static/cv.pdf` |
| Styling | `assets/css/extended/custom.css` |
| Home / publications layouts | `layouts/home.html`, `layouts/publications.html`, `layouts/_partials/pub-item.html` |

## Writing a note

```bash
hugo new content posts/my-topic/index.md   # creates a draft from archetypes/posts.md
```

Put images in the same folder. Set `draft: false` when ready to publish.
Math: `$inline$` and `$$display$$` (rendered at build time with KaTeX; no JS).
Literal dollar signs need escaping: `\$`.

> KaTeX CSS is self-hosted in `static/katex/` and must match the KaTeX version built
> into Hugo. If math looks broken after upgrading Hugo, update it from
> `https://registry.npmjs.org/katex/-/katex-<version>.tgz` (`dist/katex.min.css` + `dist/fonts/`).

## Deploy

Pushing to `main` triggers `.github/workflows/hugo.yml`, which builds and publishes to GitHub Pages.
One-time: repo **Settings → Pages → Source: GitHub Actions**.
