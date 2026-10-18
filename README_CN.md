# 谭兆辰的个人学术主页

[English](README.md) | 简体中文

[**访问网站 →**](https://clearp0ol.github.io/)

这是我的个人学术主页源码仓库。我是同济大学软件工程专业本科生，目前正在探索自己的研究兴趣，并准备前往浙江大学继续深造。

网站基于 Hugo Extended、HugoBlox 和 Tailwind CSS 构建，使用 Pagefind 提供站内搜索，通过 GitHub Actions 自动部署至 GitHub Pages。

## 网站栏目

| 栏目 | 内容 |
| --- | --- |
| [Bio](https://clearp0ol.github.io/) | 个人简介、教育背景、导师、研究兴趣、精选论文、近期动态及荣誉奖项 |
| [Papers](https://clearp0ol.github.io/publications/) | 全部论文，目前显示“No publications yet.” |
| [News](https://clearp0ol.github.io/news/) | 学术动态与个人近况 |
| [Service](https://clearp0ol.github.io/service/) | 课程助教经历 |
| [Hobby](https://clearp0ol.github.io/hobby/) | 游戏、钢琴和羽毛球 |
| [Contact me](https://clearp0ol.github.io/contact/) | 邮箱、微信、QQ 和 GitHub |

## 本地预览

### 环境要求

- **Hugo Extended 0.162.1**：与 `hugoblox.yaml` 中指定的版本一致。
- **Go**：用于解析和下载 Hugo 模块。
- **Node.js 22**：与构建工作流中的版本一致。
- **pnpm 10.14.0**：由 `package.json` 中的 `packageManager` 字段指定。

在仓库根目录打开终端并运行：

```powershell
pnpm install
hugo server
```

浏览器打开 [http://localhost:1313/](http://localhost:1313/)。修改文件并保存后，页面会自动更新。预览期间请保持终端运行，按 **Ctrl+C** 停止预览；下次运行 `hugo server` 即可重新启动。

## 内容维护

| 修改内容 | 对应文件或目录 |
| --- | --- |
| 姓名、个人简介、教育背景、导师及研究兴趣 | `data/authors/me.yaml` |
| 首页各模块、荣誉奖项及简历下载按钮 | `content/_index.md` |
| 首页和 News 页面共用的动态列表 | `data/news.yaml` |
| 论文内容 | `content/publications/` |
| 课程助教经历 | `content/service/_index.md` |
| 兴趣爱好介绍及配图 | `content/hobby/` |
| 联系方式及标题图标 | `content/contact/` |
| 导航栏链接 | `config/_default/menus.yaml` |
| 网站名称、主题、搜索及页脚设置 | `config/_default/params.yaml` |
| 网站地址及 Hugo 配置 | `config/_default/hugo.yaml` |
| 个人照片 | `assets/media/authors/me.jpg` |
| 浏览器标签页图标 | `assets/media/icon.jpg` |
| 可下载的简历 | `static/uploads/cv.pdf` |

### 动态与荣誉

在 `data/news.yaml` 中添加动态，首页的 Recent News 和独立的 News 页面会读取同一份列表。荣誉奖项单独维护在 `content/_index.md` 的 `honors` 模块中。两份列表均按时间倒序排列，文字支持 Markdown，可使用**加粗**和链接。

### 论文

有论文后，在 `content/publications/` 中添加对应的论文页面及相关文件。需要在首页展示的论文设置 `featured: true`，并适时删除 `content/_index.md` 和 `content/publications/_index.md` 中的“No publications yet.”占位文字。仓库保留了论文导入工作流，供后续使用。

### 布局与外观

本地模板覆盖文件位于 `layouts/`。个人简介布局和头像显示逻辑定制在 `layouts/_partials/hbx/blocks/resume-biography-3/block.html` 中，头像参数在 `content/_index.md` 中设置。

Service、Hobby 和 Contact me 共用 `layouts/personal/list.html`，相关样式位于 `layouts/_partials/hooks/head-end/personal-pages.html`。联系方式标题通过 `layouts/_shortcodes/contact-icon.html` 显示透明背景的 SVG 图标。

页脚由 `layouts/_partials/site_footer.html` 渲染。**Last updated** 使用 `Asia/Shanghai` 时区的构建日期，每次重新构建网站时自动更新。

## 构建与发布

先停止本地预览，再运行：

```powershell
pnpm run build
```

该命令会清理过时的生成文件，将网站构建到 `public/`，并重新生成 Pagefind 搜索索引。构建完成后，运行 `hugo server` 可在本地检查更新后的搜索结果；预览期间修改内容后，需要再次构建才能同步搜索索引。

将源码修改推送到 `main` 分支后，会触发 `.github/workflows/deploy.yml`。该工作流调用 `.github/workflows/build.yml` 构建网站及搜索索引，然后部署至 GitHub Pages。也可以在 GitHub Actions 中手动触发部署。Hugo 版本和部署目标在 `hugoblox.yaml` 中配置。

`public/`、`resources/` 和 `node_modules/` 分别存放生成的网站、缓存资源及安装的依赖，均已被 Git 忽略。日常维护请修改对应的源文件。

## 致谢与素材来源

网站基于 HugoBlox 的 Academic CV 模板进行本地定制。原框架的版权和许可声明保留在 [LICENSE.md](LICENSE.md) 中。

- 联系方式图标来源：`content/contact/icon-sources.txt`。
- 兴趣爱好配图来源：`content/hobby/game-image-sources.txt`。
- 生成插画所用的提示词：`content/hobby/image-prompts.txt`。

页脚显示的内容许可协议在 `config/_default/params.yaml` 中配置。游戏相关图片和标识的权利归各自所有者所有。
