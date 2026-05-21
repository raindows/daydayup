# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概述

DayDayUp（天天向上）是一个面向少儿的中华传统文化启蒙网站，包含 13 个学习模块。纯静态 HTML 页面，内联 CSS/JS，零构建工具，零依赖。

**线上地址：** https://raindows.github.io/daydayup/

## 本地开发

```bash
# 本地预览
python3 -m http.server 8080 -d h5

# 打开指定页面
open h5/shaoer-tonghua.html
```

无需构建、无需 lint、无需测试。所有内容直接写在 HTML 中。

## 部署

推送到 `main` 分支会自动触发 GitHub Pages 部署（`.github/workflows/deploy.yml`），发布整个 `h5/` 目录。

## 架构

所有页面位于 `h5/` 目录，每个文件自包含（HTML + 内联 CSS + 内联 JS）。每个页面统一包含：
- 字体：Google Fonts 的 Noto Serif SC（标题）+ Noto Sans SC（正文）
- CSS 自定义属性做主题色（`--bg`、`--surface`、`--ink`、`--accent` 等）
- 深色模式通过 `[data-theme="dark"]` 属性覆盖变量实现
- 主题偏好通过 `localStorage('daydayup-theme')` 持久化
- 顶部 sticky 导航栏，链接到全部 13 个模块
- IntersectionObserver 实现滚动入场动画
- 响应式断点：960px（平板）、640px（手机）

首页（`h5/index.html`）是入口页，包含 Hero 区域和 12 模块网格。

## 设计系统

CSS 变量定义在每个页面内（非共享样式表）。新增页面时，从现有页面复制 `:root` / `[data-theme="dark"]` 变量块。暖色奶油调色板（`--bg: #FAF7F2`、`--accent: #C9A96E`）需保持一致。

每个内容页有自己的强调色（如诗词用 `--accent`，汉字用 `--gold`）。导航链接使用药丸按钮样式，`.active` 状态为金色填充。

## 内容规范

- 中文内容为硬编码，不从外部加载
- 诗词文本使用 `<span class="line">` 标签包裹每一联
- 历史/文学内容必须事实准确——修改前需对照权威来源核实
