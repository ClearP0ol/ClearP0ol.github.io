# 谭兆辰的个人学术主页

[English](README.md) | 简体中文

[**访问网站**](https://clearp0ol.github.io/) · [**源码仓库**](https://github.com/ClearP0ol/ClearP0ol.github.io)

这是我的个人学术主页源码仓库，用于展示个人背景、教育经历、研究兴趣、论文、动态、助教经历、兴趣爱好和联系方式。

网站页面使用英文，仓库提供中英文维护文档。网站由 Hugo Extended 和 HugoBlox 根据 Markdown、YAML 生成，使用 Tailwind CSS 编写样式、Pagefind 提供搜索，并通过 GitHub Actions 部署至 GitHub Pages。

## 网站栏目

| 导航名称 | 路径 | 当前内容 |
| --- | --- | --- |
| Bio | `/` | Professional Summary、教育背景及导师、Interests、My Research、精选论文、近期动态和荣誉奖项 |
| Papers | `/publications/` | All Publications，目前显示“No publications yet.” |
| News | `/news/` | All News，与首页共用动态数据 |
| Service | `/service/` | **Teaching Assistant**，Optimization Theory，2025 年秋季 |
| Hobby | `/hobby/` | Counter-Strike 2、VALORANT、钢琴和羽毛球 |
| Contact me | `/contact/` | 邮箱、微信、QQ 和 GitHub 主页链接 |

网站支持明暗切换、固定主题配色、响应式布局、透明背景的联系图标、简历下载，以及显示版权声明和构建日期的页脚。

## 开发环境与本地预览

### 环境要求

| 工具 | 仓库配置 | 用途 |
| --- | --- | --- |
| Hugo Extended | **0.162.1**，由 `hugoblox.yaml` 固定 | 生成网站及处理资源 |
| Node.js | **22**，由 `.github/workflows/build.yml` 指定 | 运行前端构建工具 |
| pnpm | **10.14.0**，由 `package.json` 声明 | 安装依赖及运行构建、搜索命令 |
| Go | 在 `PATH` 中可用 | 解析 `go.mod` 和 `go.sum` 中的 Hugo 模块 |
| Git | 在 `PATH` 中可用 | 克隆及维护仓库 |

JavaScript 依赖包括 Tailwind CSS、其 CLI 和 typography 插件、Pagefind 及 Preact，实际安装版本记录在 `pnpm-lock.yaml` 中。

### 启动预览

```powershell
git clone https://github.com/ClearP0ol/ClearP0ol.github.io.git
cd ClearP0ol.github.io
pnpm install --frozen-lockfile
hugo server
```

已有本地仓库时，在仓库根目录运行最后两条命令即可。浏览器打开 [http://localhost:1313/](http://localhost:1313/)，保持终端运行，修改源文件并保存后即可查看更新。首次构建可能需要下载 Hugo 模块。按 **Ctrl+C** 停止预览，重新运行 `hugo server` 即可再次启动。

如果终端提示无法识别命令，请确认对应程序已加入 `PATH`，并在安装后重新打开终端。

### 可用命令

| 命令 | 作用 |
| --- | --- |
| `hugo server` | 使用 Hugo Fast Render 模式进行本地预览 |
| `pnpm dev` | 执行 `hugo server --disableFastRender`，在预览时进行完整渲染 |
| `pnpm run build` | 执行 `hugo --gc --cleanDestinationDir --minify`，随后生成 Pagefind 索引 |
| `pnpm run pagefind` | 对 `public/` 中已有的 HTML 重新建立索引 |

日常编辑使用 `hugo server` 即可。当预览未反映修改、需要完整渲染时，可使用 `pnpm dev`。Hugo 预览服务器不会自动重建 Pagefind 搜索索引，更新方式见[构建与发布](#构建与发布)。

## 仓库结构

```text
.
├── .github/workflows/       # 构建、部署、论文导入和框架升级
├── .devcontainer/          # 可选的开发容器配置
├── .vscode/                # 编辑器扩展推荐
├── assets/media/           # 头像、网站图标源文件和自定义图标目录
├── config/_default/        # Hugo、模块、语言、导航及网站设置
├── content/
│   ├── _index.md           # 首页模块、荣誉奖项和头像参数
│   ├── authors/_index.md   # 作者归档页面的显示设置
│   ├── publications/       # 全部论文页面及后续论文内容
│   ├── news/               # 全部动态页面
│   ├── service/            # 助教经历页面
│   ├── hobby/              # 兴趣爱好、配图及来源记录
│   └── contact/            # 联系方式、SVG 图标及来源记录
├── data/
│   ├── authors/me.yaml     # 个人资料及教育背景
│   └── news.yaml           # 首页和 News 共用的动态数据
├── layouts/                # HugoBlox 本地模板覆盖及样式钩子
├── static/uploads/cv.pdf   # 可下载的简历
├── hugoblox.yaml            # Hugo 版本及部署目标
├── package.json            # JavaScript 依赖及运行命令
├── pnpm-lock.yaml          # 锁定的 JavaScript 依赖版本
├── .npmrc                  # pnpm 的 hoisted 节点链接器配置
├── go.mod / go.sum         # Hugo 模块依赖
├── netlify.toml            # 可选的 Netlify 构建配置
├── .gitignore              # Git 忽略的生成文件及本地文件
├── LICENSE.md              # 原框架版权及 MIT 许可声明
├── README.md
└── README_CN.md
```

`public/`、`resources/`、`node_modules/`、`.hugo_build.lock` 和 `hugo_stats.json` 均由本地运行生成，已被 Git 忽略。维护网站时修改上述源文件。独立的作者归档页面目前由 `content/authors/_index.md` 禁用。

## 内容维护

大部分内容存放在 YAML 文件，或 Markdown 文件开头的 YAML front matter 中。

| 修改内容 | 对应源文件 |
| --- | --- |
| 姓名、简介、身份、所属单位、社交链接、研究兴趣、教育背景及导师 | [data/authors/me.yaml](data/authors/me.yaml) |
| 首页模块顺序、My Research 文案、精选论文占位文字及简历按钮 | [content/_index.md](content/_index.md) |
| Honors & Awards | [content/_index.md](content/_index.md) 中的 `honors` 模块 |
| 动态条目 | [data/news.yaml](data/news.yaml) |
| All News 页面布局 | [content/news/_index.md](content/news/_index.md) |
| 论文索引及后续论文内容 | [content/publications/](content/publications/) |
| 助教经历 | [content/service/_index.md](content/service/_index.md) |
| 兴趣爱好介绍及卡片配图 | [content/hobby/_index.md](content/hobby/_index.md) 及同目录图片 |
| 联系方式 | [content/contact/_index.md](content/contact/_index.md) |
| 导航名称、目标地址及顺序 | [config/_default/menus.yaml](config/_default/menus.yaml) |
| 网站名称、主题、搜索、版权文字及页脚日期格式 | [config/_default/params.yaml](config/_default/params.yaml) |
| 网站地址及 Hugo 配置 | [config/_default/hugo.yaml](config/_default/hugo.yaml) |
| 语言及模块配置 | [config/_default/languages.yaml](config/_default/languages.yaml)、[config/_default/module.yaml](config/_default/module.yaml) |
| 个人照片、浏览器图标及简历 | [assets/media/authors/me.jpg](assets/media/authors/me.jpg)、[assets/media/icon.jpg](assets/media/icon.jpg)、[static/uploads/cv.pdf](static/uploads/cv.pdf) |

### 个人资料与首页

首页简介模块通过 `username: me` 读取 `data/authors/me.yaml`。教育条目支持使用 `institution_bold` 加粗大学名称，并使用 `supervisor.name` 和 `supervisor.url` 显示带链接的导师信息。

导航栏和页脚使用的网站身份信息另行配置在 `params.yaml` 的 `hugoblox.identity` 中。修改姓名时，需要同时更新个人资料和网站身份信息。

首页荣誉奖项维护在首页的 `honors` 模块中，个人资料中的 `awards` 数组是另一字段。首页各模块的间距和头像参数也在 `content/_index.md` 中设置。

### 动态与荣誉

条目按源文件中的顺序显示，请手动保持时间倒序。动态位于 `data/news.yaml` 的 `items` 中，Recent News 和 All News 共用这份数据；荣誉位于首页 `honors` 模块的 `items` 列表中。每条记录包含加引号的 `date` 和支持 Markdown 的 `text`。

### 论文

首页 Featured Publications 和 All Publications 页面目前均显示“No publications yet.”。有论文后，可创建 `content/publications/<slug>/index.md` 形式的页面内容包，并将相关附件放在同目录。需要在首页展示的论文设置 `featured: true`。

真实条目准备好后，删除 `content/_index.md` 和 `content/publications/_index.md` 中的占位文字。首页精选列表读取 `publications` 目录中标记为 featured 的条目。下文还介绍了可选的 BibTeX 导入工作流。

### 助教、兴趣爱好与联系方式

助教经历直接使用 `content/service/_index.md` 中的 Markdown 正文。兴趣爱好使用 `content/hobby/_index.md` 的 `hobby_cards` front matter，每张卡片包含 `id`、`title`、`image` 和 `items`，各条目还可以单独指定配图。引用的图片应放在该页面同目录，Hugo 会自动为横幅和游戏封面生成 WebP 版本。

联系方式标题通过 `contact-icon` shortcode 引入图标，例如：

```text
{{< contact-icon name="github" >}}
```

支持的名称为 `email`、`wechat`、`qq` 和 `github`，对应本地的 `contact-*.svg` 资源。图标外围背景透明，GitHub 图标使用 `currentColor` 跟随明暗模式下的标题颜色。

### 简历

将新导出的 PDF 替换到 `static/uploads/cv.pdf`，即可更新首页下载的简历。保留文件名和路径，**Download CV** 链接便可继续使用。可编辑的 Word 原稿在本仓库之外单独维护。

从 Word 导出前，将文档属性中的**标题（Title）**设为 `cv`，然后确认 PDF 的文档标题和 XMP 标题也均为 `cv`。浏览器可能使用这些元数据作为标签页标题，简历正文中的可见标题可以保持不变。

## 本地模板与外观

`layouts/` 中的本地模板会覆盖下载的 HugoBlox 模块模板。合并框架升级时，需要同时检查这些覆盖文件。

| 定制内容 | 对应文件 |
| --- | --- |
| 简介布局、首屏间距、头像取景及教育卡片 | [resume-biography-3/block.html](layouts/_partials/hbx/blocks/resume-biography-3/block.html) |
| 读取当前作者资料及处理 JPEG 的 EXIF 方向 | [get_author_profile.html](layouts/_partials/functions/get_author_profile.html) |
| 将个人 JPG 网站图标转换为 PNG 图标 | [get_site_icon.html](layouts/_partials/functions/get_site_icon.html) |
| 动态与荣誉的日期加文字列表 | [dated-list/block.html](layouts/_partials/hbx/blocks/dated-list/block.html)、[news-and-honors.html](layouts/_partials/hooks/head-end/news-and-honors.html) |
| Service、Hobby 和 Contact me 的展示 | [personal/list.html](layouts/personal/list.html)、[personal-pages.html](layouts/_partials/hooks/head-end/personal-pages.html) |
| 内联联系方式 SVG 图标 | [contact-icon.html](layouts/_shortcodes/contact-icon.html) |
| 固定主题配色及独立的明暗切换控制 | [fixed-theme.html](layouts/_partials/hooks/head-end/fixed-theme.html) |
| My Research 模块间距 | [research-spacing.html](layouts/_partials/hooks/head-end/research-spacing.html) |
| 页脚内容及响应式样式 | [site_footer.html](layouts/_partials/site_footer.html)、[academic-footer.html](layouts/_partials/hooks/head-end/academic-footer.html) |

首页第一个模块的 `design.avatar` 可设置以像素为单位的 `width`、`height`，以及 `shape`、`position_x`、`position_y` 和 `zoom`。当前头像框为 **300 × 300**，对齐参数为 **80 / 40**，缩放为 **0.85**。位置参数取值为 0 至 100，缩放为 1 时使用头像框内的原始比例。单独调整图片处理分辨率不会改变可见取景范围。

当前主题配色包为 `default`，初始颜色模式为 `light`，主题选择器已隐藏，明暗切换按钮仍保留。这些选项配置在 `params.yaml` 的 `hugoblox.theme` 和 `hugoblox.header` 中。

页脚显示 `© {year} {name}` 和 **Last updated**。更新时间使用 `Asia/Shanghai` 时区的构建日期，格式为 `Jan 02, 2006`，重新构建时自动更新。当前版权配置不显示 CC 许可链接和图标。

## 构建与发布

### 正式构建与搜索

先按 **Ctrl+C** 停止预览，再运行：

```powershell
pnpm run build
```

该命令会清理未使用的缓存资源和过时的输出文件，将压缩后的站点生成到 `public/`，并为这些 HTML 建立 `public/pagefind/` 搜索索引。之后运行 `hugo server`，即可在本地检查结果。

Pagefind 搜索的是已生成 HTML 的快照。修改内容后，应重新构建以更新搜索结果。`pnpm run pagefind` 只会对已有输出重建索引，不会重新渲染网站本身。

### GitHub Pages

当前网站地址为 `https://clearp0ol.github.io/`。Hugo 的基础地址配置在 `config/_default/hugo.yaml`，`hugoblox.yaml` 通过 `deploy.host: github-pages` 选择部署目标，并固定主要构建工作流使用的 Hugo 版本。

仓库的 Pages 发布来源应设为 **GitHub Actions**，设置方式可参考 [GitHub 自定义工作流文档](https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages)。检查并提交源码修改后，将其推送到 `main` 分支即可触发部署。

部署工作流会检查目标平台，调用可复用的构建工作流，然后部署上传的 `public/` 产物。构建阶段会安装 Node.js 和 pnpm 依赖、指定版本的 Hugo Extended，获取 Pages 基础地址，渲染网站并生成搜索数据；该构建工作流也用于检查目标为 `main` 的拉取请求。

本地修改需要推送源码并成功部署后才会在线上生效。构建和部署状态可在仓库的 **Actions** 页面查看。

## 自动化与可选配置

| 工作流 | 触发方式 | 结果 |
| --- | --- | --- |
| [build.yml](.github/workflows/build.yml) | 目标为 `main` 的拉取请求、其他工作流调用或手动运行 | 构建网站和搜索索引，并上传 Pages 产物 |
| [deploy.yml](.github/workflows/deploy.yml) | 推送到 `main` 或手动运行 | 调用构建工作流，目标为 `github-pages` 时执行部署 |
| [import-publications.yml](.github/workflows/import-publications.yml) | `main` 分支根目录的 `publications.bib` 变更，或手动运行 | 使用 `academic import` 生成论文页面，并创建拉取请求 |
| [upgrade.yml](.github/workflows/upgrade.yml) | 每周定时运行或手动运行 | 执行 HugoBlox 升级命令，并为更新和迁移创建拉取请求 |

需要导入论文时，在仓库根目录添加 `publications.bib`，检查自动生成的拉取请求，并合并需要发布的条目。当前仓库尚未包含该文件。工作流创建拉取请求需要仓库允许相应操作。

可选的 [Netlify 配置](netlify.toml)和[开发容器配置](.devcontainer/devcontainer.json)目前指定 **Hugo 0.162.0**，主要 GitHub Pages 构建使用 **0.162.1**。使用这些环境前，应与 `hugoblox.yaml` 对齐版本，以保持构建一致。仅修改 `deploy.host` 不会自动在其他平台创建托管服务。

[.vscode/extensions.json](.vscode/extensions.json) 推荐 Ownable 编辑扩展，[.npmrc](.npmrc) 配置 pnpm 的 hoisted 节点链接器。网站也可以直接按上述命令行流程维护。

## 致谢与许可记录

网站基于 [HugoBlox](https://github.com/HugoBlox/kit) 的 Academic CV 模板，进行了内容和布局定制。原始的 **Lore Labs 版权及 MIT 许可声明**保留在 [LICENSE.md](LICENSE.md) 中，Hugo 模块的来源及版本记录在 [go.mod](go.mod) 和 [go.sum](go.sum) 中。

素材来源另行记录在：

- [联系方式图标来源及许可信息](content/contact/icon-sources.txt)。
- [兴趣配图、游戏封面及段位图标来源](content/hobby/game-image-sources.txt)。
- [生成兴趣插画所用的提示词](content/hobby/image-prompts.txt)。

页脚的个人版权声明与上述框架、素材来源记录分别维护。注明来源不代表第三方版权转移，也不能替代原有许可条件。维护仓库时应保留许可及素材来源记录。
