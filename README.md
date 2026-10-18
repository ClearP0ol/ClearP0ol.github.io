# Zhaochen Tan's Academic Homepage

English | [简体中文](README_CN.md)

[**Website**](https://clearp0ol.github.io/) · [**Source repository**](https://github.com/ClearP0ol/ClearP0ol.github.io)

The source for my personal academic website, presenting my background, education, research interests, publications, news, teaching service, hobbies, and contact information.

The website is written in English. This repository provides English and Chinese maintenance documentation. Pages are generated from Markdown and YAML using Hugo Extended and HugoBlox, with Tailwind CSS for styling, Pagefind for search, and GitHub Actions for deployment to GitHub Pages.

## Site pages

| Navigation | Route | Current contents |
| --- | --- | --- |
| Bio | `/` | Professional Summary, Education and supervisors, Interests, My Research, Featured Publications, Recent News, and Honors & Awards |
| Papers | `/publications/` | All Publications, currently displaying “No publications yet.” |
| News | `/news/` | All News, sharing its entries with the homepage |
| Service | `/service/` | **Teaching Assistant**, Optimization Theory, 2025Fall |
| Hobby | `/hobby/` | Counter-Strike 2 and VALORANT, piano, and badminton |
| Contact me | `/contact/` | Email, WeChat, QQ, and a GitHub profile link |

The site includes a light/dark toggle, a fixed theme pack, responsive layouts, transparent contact icons, a downloadable CV, and a footer with a copyright notice and build date.

## Toolchain and local preview

### Requirements

| Tool | Configuration | Purpose |
| --- | --- | --- |
| Hugo Extended | **0.162.1**, pinned in `hugoblox.yaml` | Site generation and asset processing |
| Node.js | **22**, selected in `.github/workflows/build.yml` | Frontend build tools |
| pnpm | **10.14.0**, declared in `package.json` | Install dependencies and run build/search commands |
| Go | Available on `PATH` | Resolve the Hugo modules in `go.mod` and `go.sum` |
| Git | Available on `PATH` | Clone and maintain the repository |

The JavaScript dependencies include Tailwind CSS, its CLI and typography plugin, Pagefind, and Preact. Exact resolved versions are recorded in `pnpm-lock.yaml`.

### Start the preview

```powershell
git clone https://github.com/ClearP0ol/ClearP0ol.github.io.git
cd ClearP0ol.github.io
pnpm install --frozen-lockfile
hugo server
```

For an existing checkout, run the last two commands from the repository root. Open [http://localhost:1313/](http://localhost:1313/), keep the terminal running, and save source changes to update the preview. The initial build may download Hugo modules. Press **Ctrl+C** to stop the server; run `hugo server` to start it again.

If a command is not recognized, check that its executable is on `PATH` and reopen the terminal after installing it.

### Available commands

| Command | Behavior |
| --- | --- |
| `hugo server` | Local preview using Hugo's Fast Render mode |
| `pnpm dev` | Runs `hugo server --disableFastRender`, with full rendering during preview |
| `pnpm run build` | Runs `hugo --gc --cleanDestinationDir --minify`, then generates the Pagefind index |
| `pnpm run pagefind` | Indexes the HTML already present in `public/` |

Use `hugo server` for everyday editing. `pnpm dev` is useful when changes appear stale and a full render is needed. Hugo's preview server does not regenerate the Pagefind index automatically; see [Build and publish](#build-and-publish).

## Repository structure

```text
.
├── .github/workflows/       # Build, deployment, publication import, and upgrades
├── .devcontainer/          # Optional development container configuration
├── .vscode/                # Editor extension recommendations
├── assets/media/           # Portrait, favicon source, and custom icon directory
├── config/_default/        # Hugo, modules, language, navigation, and site settings
├── content/
│   ├── _index.md           # Homepage sections, honors, and avatar options
│   ├── authors/_index.md   # Author archive visibility settings
│   ├── publications/       # All Publications page and future publication bundles
│   ├── news/               # All News page
│   ├── service/            # Teaching service page
│   ├── hobby/              # Hobby content, images, and source records
│   └── contact/            # Contact content, SVG icons, and source records
├── data/
│   ├── authors/me.yaml     # Personal profile and education
│   └── news.yaml           # Shared news entries
├── layouts/                # Local HugoBlox template overrides and style hooks
├── static/uploads/cv.pdf   # Downloadable CV
├── hugoblox.yaml            # Hugo version and deployment target
├── package.json            # JavaScript dependencies and commands
├── pnpm-lock.yaml          # Locked JavaScript dependency versions
├── .npmrc                  # pnpm uses the hoisted node linker
├── go.mod / go.sum         # Hugo module dependencies
├── netlify.toml            # Optional Netlify build configuration
├── .gitignore              # Generated output and local files excluded from Git
├── LICENSE.md              # Original framework copyright and MIT license notice
├── README.md
└── README_CN.md
```

`public/`, `resources/`, `node_modules/`, `.hugo_build.lock`, and `hugo_stats.json` are generated locally and ignored by Git. Edit the source files above. Standalone author archive pages are currently disabled by `content/authors/_index.md`.

## Content maintenance

Most content lives in YAML files or in the YAML front matter at the beginning of Markdown files.

| What to change | Source |
| --- | --- |
| Display name, biography, role, affiliations, social links, interests, education, and supervisors | [data/authors/me.yaml](data/authors/me.yaml) |
| Homepage section order, My Research text, Featured Publications placeholder, and CV button | [content/_index.md](content/_index.md) |
| Honors & Awards | The `honors` section in [content/_index.md](content/_index.md) |
| News entries | [data/news.yaml](data/news.yaml) |
| All News page layout | [content/news/_index.md](content/news/_index.md) |
| Publications index and future entries | [content/publications/](content/publications/) |
| Teaching service | [content/service/_index.md](content/service/_index.md) |
| Hobby descriptions and card images | [content/hobby/_index.md](content/hobby/_index.md) and neighboring image files |
| Contact details | [content/contact/_index.md](content/contact/_index.md) |
| Navigation labels, destinations, and order | [config/_default/menus.yaml](config/_default/menus.yaml) |
| Site identity, theme, search, copyright notice, and footer date format | [config/_default/params.yaml](config/_default/params.yaml) |
| Base URL and Hugo configuration | [config/_default/hugo.yaml](config/_default/hugo.yaml) |
| Language and module configuration | [config/_default/languages.yaml](config/_default/languages.yaml), [config/_default/module.yaml](config/_default/module.yaml) |
| Portrait, browser icon, and CV | [assets/media/authors/me.jpg](assets/media/authors/me.jpg), [assets/media/icon.jpg](assets/media/icon.jpg), [static/uploads/cv.pdf](static/uploads/cv.pdf) |

### Profile and homepage

The homepage's biography block selects `username: me`, which reads `data/authors/me.yaml`. Education entries support `institution_bold` to emphasize the university name, and `supervisor.name` / `supervisor.url` for linked supervisor information.

The navbar and footer identity are configured separately under `hugoblox.identity` in `params.yaml`. When changing the owner's displayed name, update both the personal profile and site identity.

Homepage honors are maintained in the homepage's `honors` block. The `awards` array in the profile data is a separate field. Homepage section spacing and avatar options are also configured in `content/_index.md`.

### News and honors

Keep entries in reverse chronological order; their display follows the order in the source file. News uses `items` in `data/news.yaml`, read by both Recent News and All News. Honors uses the `items` list in the homepage's `honors` block. Each entry has a quoted `date` and Markdown-enabled `text`.

### Publications

The homepage's Featured Publications section and the All Publications page currently display “No publications yet.” To add publications, create page bundles such as `content/publications/<slug>/index.md`, with related files alongside them. Set `featured: true` on publications that should appear on the homepage.

When real entries are ready, remove the placeholder text from both `content/_index.md` and `content/publications/_index.md`. The homepage collection reads featured entries from the `publications` folder. An optional BibTeX import workflow is described below.

### Service, hobbies, and contact

Service content is Markdown in `content/service/_index.md`. Hobby content uses the `hobby_cards` front matter in `content/hobby/_index.md`; each card has an `id`, `title`, `image`, and `items`, with optional images for individual items. Keep referenced images alongside that page. Hugo automatically creates WebP versions for banners and game covers.

Contact headings use the `contact-icon` shortcode, for example:

```text
{{< contact-icon name="github" >}}
```

The supported names are `email`, `wechat`, `qq`, and `github`, matching the local `contact-*.svg` resources. Their outer backgrounds are transparent; the GitHub icon uses `currentColor` to follow the heading color in light and dark modes.

### CV

Replace `static/uploads/cv.pdf` with the newly exported PDF to update the homepage download. Keep the filename and path so **Download CV** continues to work. The editable Word source is maintained outside this repository.

Before exporting from Word, set its document **Title** property to `cv`, then confirm that the PDF's document title and XMP title are also `cv`. Browsers may use these metadata properties as the tab title; the visible headings inside the CV can remain unchanged.

## Local templates and appearance

Local templates in `layouts/` override the downloaded HugoBlox modules. Review these overrides when merging framework upgrades.

| Customization | Files |
| --- | --- |
| Biography layout, first-screen spacing, avatar framing, and education cards | [resume-biography-3/block.html](layouts/_partials/hbx/blocks/resume-biography-3/block.html) |
| Current author data and JPEG EXIF orientation | [get_author_profile.html](layouts/_partials/functions/get_author_profile.html) |
| Personal JPG favicon converted into PNG icons | [get_site_icon.html](layouts/_partials/functions/get_site_icon.html) |
| Date-and-text rows for news and honors | [dated-list/block.html](layouts/_partials/hbx/blocks/dated-list/block.html), [news-and-honors.html](layouts/_partials/hooks/head-end/news-and-honors.html) |
| Service, Hobby, and Contact me presentation | [personal/list.html](layouts/personal/list.html), [personal-pages.html](layouts/_partials/hooks/head-end/personal-pages.html) |
| Inline contact SVGs | [contact-icon.html](layouts/_shortcodes/contact-icon.html) |
| Fixed theme pack and independent light/dark control | [fixed-theme.html](layouts/_partials/hooks/head-end/fixed-theme.html) |
| My Research spacing | [research-spacing.html](layouts/_partials/hooks/head-end/research-spacing.html) |
| Footer content and responsive styling | [site_footer.html](layouts/_partials/site_footer.html), [academic-footer.html](layouts/_partials/hooks/head-end/academic-footer.html) |

The first homepage block's `design.avatar` settings control `width` and `height` in pixels, `shape`, `position_x`, `position_y`, and `zoom`. The current frame is **300 × 300**, with alignment **80 / 40** and zoom **0.85**. Position values range from 0 to 100; a zoom of 1 uses the original scale within the frame. Changing image-processing resolution alone does not change the visible framing.

The configured theme pack is `default`, the initial color mode is `light`, the theme picker is hidden, and the light/dark toggle remains enabled. These options are under `hugoblox.theme` and `hugoblox.header` in `params.yaml`.

The footer displays `© {year} {name}` and **Last updated**. Its date is generated at build time using `Asia/Shanghai` and the `Jan 02, 2006` format. Rebuilding refreshes that date. The CC license link and icons are omitted by the current copyright configuration.

## Build and publish

### Production build and search

Stop the preview with **Ctrl+C**, then run:

```powershell
pnpm run build
```

The build removes unused cached resources and stale destination files, generates minified site output in `public/`, and indexes that HTML into `public/pagefind/`. Start `hugo server` again to inspect the result locally.

Pagefind searches a generated snapshot of the HTML. After content changes, repeat the build to refresh search results. `pnpm run pagefind` only rebuilds the index from existing output; it does not render the website itself.

### GitHub Pages

The configured public URL is `https://clearp0ol.github.io/`. Hugo's base URL is in `config/_default/hugo.yaml`; `hugoblox.yaml` selects `deploy.host: github-pages` and pins the Hugo version used by the main build workflow.

Configure the repository's Pages publishing source to use **GitHub Actions**, following [GitHub's custom workflow documentation](https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages). Review and commit source changes, then push them to `main` to trigger deployment.

The deployment workflow checks the selected host, calls the reusable build workflow, then deploys the uploaded `public/` artifact. The build installs Node.js and pnpm dependencies, installs the pinned Hugo Extended release, obtains the Pages base URL, renders the site, and generates search data. It can also validate pull requests to `main`.

Local edits become visible online after their source changes are pushed and the deployment succeeds. Build and deployment status can be checked in the repository's **Actions** tab.

## Automation and optional configurations

| Workflow | Trigger | Result |
| --- | --- | --- |
| [build.yml](.github/workflows/build.yml) | Pull requests to `main`, reusable calls, or manual runs | Builds the site and search index, then uploads a Pages artifact |
| [deploy.yml](.github/workflows/deploy.yml) | Pushes to `main` or manual runs | Calls the build workflow and deploys when the selected host is `github-pages` |
| [import-publications.yml](.github/workflows/import-publications.yml) | Changes to root-level `publications.bib` on `main`, or manual runs | Uses `academic import` to generate publication pages and opens a pull request |
| [upgrade.yml](.github/workflows/upgrade.yml) | Weekly schedule or manual runs | Runs the HugoBlox upgrade CLI and opens a pull request for updates and migrations |

To use publication importing, add a root-level `publications.bib`, review the generated pull request, and merge the entries you want to publish. The file is not currently included. Creating workflow pull requests requires the repository to permit that action.

The optional [Netlify configuration](netlify.toml) and [development container](.devcontainer/devcontainer.json) currently specify **Hugo 0.162.0**, while the main GitHub Pages build uses **0.162.1**. Align their versions with `hugoblox.yaml` before using those environments to match the main build. Changing `deploy.host` alone does not provision hosting on another platform.

[.vscode/extensions.json](.vscode/extensions.json) recommends the Ownable editor extension. [.npmrc](.npmrc) configures pnpm's hoisted node linker. The website can be maintained with the command-line workflow above.

## Credits and licensing

This website is based on [HugoBlox](https://github.com/HugoBlox/kit)'s Academic CV template, with local content and layout customizations. The original **Lore Labs copyright and MIT license notice** remain in [LICENSE.md](LICENSE.md). Hugo module origins and versions are recorded in [go.mod](go.mod) and [go.sum](go.sum).

Asset provenance is recorded separately:

- [Contact icon sources and license information](content/contact/icon-sources.txt).
- [Hobby artwork, game covers, and rank badge sources](content/hobby/game-image-sources.txt).
- [Prompts for the generated hobby illustrations](content/hobby/image-prompts.txt).

The footer's personal copyright notice is separate from these framework and asset records. Source acknowledgments do not transfer third-party copyrights or replace the original license terms. Keep the license and provenance records when maintaining the repository.
