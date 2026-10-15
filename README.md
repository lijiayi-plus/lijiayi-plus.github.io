# plusone's blog (Hugo)

个人博客，由 Hexo 迁移至 Hugo。站点地址：<https://lijiayi-plus.github.io/>

## 目录结构

```
content/
  _index.md            首页
  posts/               文章（唯一的日常写作目录）
  projects/            项目
  series/_index.md     系列（用 {{< series >}} 短代码聚合）
  gallery/             画廊
layouts/               模板（_default / shortcodes）
static/                css、favicon、og 图
hugo.toml              站点配置
_hexo_backup/          迁移前的 Hexo 全部文件（已 gitignore，仅本地留档）
```

## 本地使用

Hugo 已通过 winget 安装（`Hugo.Hugo.Extended`）。若新开终端找不到 `hugo`，重启终端即可。

```powershell
hugo server          # 本地预览 http://localhost:1313/ （改文件自动刷新）
hugo --gc --minify   # 生成 public/ ，与 CI 一致
```

## 新建文章

```powershell
hugo new content posts/我的新文章.md
```

或在 `content/posts/` 直接新建 `.md`，文件名即 URL slug。Front matter 常用字段：

```yaml
---
title: "标题"
date: 2026-10-15T10:00:00+08:00
slug: "自定义-url"        # 可选，省略则用文件名
cover: "https://..."      # 可选，封面图
series: "一生一芯"         # 可选，归入某个系列
weight: 11                # 系列内排序
tags: ["学习记录"]         # 可选（当前未渲染标签页）
aliases: ["/2026/10/15/旧地址/"]   # 可选，旧链接重定向
---
```

## 数学公式

直接写 `$...$`、`$$...$$`、`\(...\)`、`\[...\]` 均可，模板会自动按需加载 KaTeX。

## 部署

推送到 `main` 分支后，`.github/workflows/hugo.yml` 会自动构建并发布到 GitHub Pages。

需要在仓库 **Settings → Pages → Build and deployment → Source** 选择 **GitHub Actions**（只需设置一次）。

## 旧链接兼容

Hexo 时期的文章地址（`/2026/05/17/13：再看yolov4/` 形式）已通过每篇文章的 `aliases` 生成 301 跳转，旧外链不会失效。

`/archives/`、`/tags/`、`/categories/`、`/flink/`、`/music/` 这些 Hexo 页面未迁移。