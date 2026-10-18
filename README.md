# Zhaochen Tan's Academic Homepage

English | [简体中文](README_CN.md)

[**Visit the website →**](https://clearp0ol.github.io/)

The source code for my personal academic website. I am a Software Engineering undergraduate at Tongji University, exploring my research interests and preparing for further study at Zhejiang University.

Built with Hugo Extended, HugoBlox, and Tailwind CSS, with Pagefind for site search and GitHub Actions for deployment to GitHub Pages.

## Website pages

| Page | Contents |
| --- | --- |
| [Bio](https://clearp0ol.github.io/) | Professional summary, education, supervisors, research interests, featured publications, recent news, and honors |
| [Papers](https://clearp0ol.github.io/publications/) | All publications; currently displays “No publications yet.” |
| [News](https://clearp0ol.github.io/news/) | Academic news and updates |
| [Service](https://clearp0ol.github.io/service/) | Teaching assistant experience |
| [Hobby](https://clearp0ol.github.io/hobby/) | Gaming, piano, and badminton |
| [Contact me](https://clearp0ol.github.io/contact/) | Email, WeChat, QQ, and GitHub |

## Run locally

### Requirements

- **Hugo Extended 0.162.1**, matching the version in `hugoblox.yaml`.
- **Go**, for resolving Hugo modules.
- **Node.js 22**, matching the build workflow.
- **pnpm 10.14.0**, specified by `packageManager` in `package.json`.

Run these commands from the repository root:

```powershell
pnpm install
hugo server
```

Open [http://localhost:1313/](http://localhost:1313/). Save changes to preview them automatically. Keep the terminal running during preview, and press **Ctrl+C** to stop it. Start it again with `hugo server`.

## Maintain the website

| What to update | Source file or directory |
| --- | --- |
| Name, biography, education, supervisors, and interests | `data/authors/me.yaml` |
| Homepage sections, awards, and CV button | `content/_index.md` |
| News entries shared by the homepage and News page | `data/news.yaml` |
| Publications | `content/publications/` |
| Teaching service | `content/service/_index.md` |
| Hobby descriptions and images | `content/hobby/` |
| Contact details and heading icons | `content/contact/` |
| Navigation links | `config/_default/menus.yaml` |
| Branding, theme, search, and footer settings | `config/_default/params.yaml` |
| Website URL and Hugo settings | `config/_default/hugo.yaml` |
| Portrait | `assets/media/authors/me.jpg` |
| Browser tab icon | `assets/media/icon.jpg` |
| Downloadable CV | `static/uploads/cv.pdf` |

### News and honors

Add news to `data/news.yaml`; both news sections read the same list. Honors are maintained separately in the `honors` section of `content/_index.md`. Keep both lists in reverse chronological order. Their text supports Markdown, including **bold text** and links.

### Publications

Add real publication bundles under `content/publications/`. Set `featured: true` on entries that should appear on the homepage, and remove the “No publications yet.” placeholders from both `content/_index.md` and `content/publications/_index.md` when appropriate. The publication import workflow is retained for future use.

### Layout and appearance

Local template overrides live in `layouts/`. The profile layout and avatar framing are customized in `layouts/_partials/hbx/blocks/resume-biography-3/block.html`; the avatar options are configured in `content/_index.md`.

Service, Hobby, and Contact me use `layouts/personal/list.html`, with styling in `layouts/_partials/hooks/head-end/personal-pages.html`. Contact headings use transparent SVG icons through `layouts/_shortcodes/contact-icon.html`.

The footer is rendered by `layouts/_partials/site_footer.html`. **Last updated** is generated automatically at build time using the `Asia/Shanghai` timezone; rebuilding the site refreshes the date.

## Build and publish

Stop the local preview before building:

```powershell
pnpm run build
```

This clears stale generated output, builds the site into `public/`, and regenerates its Pagefind search index. To check the refreshed search locally, start `hugo server` again after the build. Content edits during preview require another build to refresh that index.

Pushing source changes to `main` triggers `.github/workflows/deploy.yml`, which calls `.github/workflows/build.yml` to build the website and search index, then deploys the result to GitHub Pages. Deployment can also be started manually from GitHub Actions. The Hugo version and deployment target are configured in `hugoblox.yaml`.

`public/`, `resources/`, and `node_modules/` are generated output, cached assets, and installed dependencies. They are ignored by Git; maintain the source files instead.

## Credits and asset sources

The website uses HugoBlox's Academic CV template with local customizations. The original framework copyright and license notice are retained in [LICENSE.md](LICENSE.md).

- Contact icon sources: `content/contact/icon-sources.txt`.
- Hobby image sources: `content/hobby/game-image-sources.txt`.
- Generated illustration prompts: `content/hobby/image-prompts.txt`.

The content license displayed in the footer is configured in `config/_default/params.yaml`. Game artwork and logos retain their respective owners' rights.
