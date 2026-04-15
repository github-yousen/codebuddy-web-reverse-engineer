# Web Reverse Engineer / 网站源码逆向分析技能

[English](#english) | [中文](#chinese)

---

<a id="chinese"></a>

## 📖 简介

一个用于 [CodeBuddy](https://www.codebuddy.ai/) 的技能（Skill），通过抓取 HTML/JS 源码（而非浏览器渲染）逆向分析网站的接口、页面布局、鉴权流程和数据流。

### 核心能力

1. **理解** — 搞清楚网站能做什么，功能结构是什么
2. **操作** — 给定凭证（Cookie / Token），直接通过 API 调用完成具体操作
3. **沉淀** — 产出分析文档，下次直接复用，不用重新分析

### 触发场景

当用户提到以下关键词时触发：
- "分析网站"、"逆向网站"、"网站接口"、"抓接口"
- "网站源码分析"、"逆向工程"、"分析API"
- "爬取接口"、"网站结构分析"、"网站白盒分析"
- 或者直接给一个 URL 说"帮我看看这个网站"

---

## 🚀 快速开始

### 安装

将本项目克隆到 CodeBuddy 的 skills 目录：

```bash
# 克隆到 CodeBuddy skills 目录
git clone https://github.com/github-yousen/codebuddy-web-reverse-engineer.git ~/.codebuddy/skills/web-reverse-engineer
```

### 使用

在 CodeBuddy 中，直接告诉 AI 你想分析哪个网站：

```
帮我分析一下 https://www.example.com 的接口
```

AI 会自动：
1. 抓取目标网站的 HTML 和所有 JS 文件
2. 从 JS 中提取 API 端点
3. 分析鉴权流程（Cookie/CSRF/Token/签名）
4. 产出完整的分析报告

---

## 📁 项目结构

```
web-reverse-engineer/
├── SKILL.md                    # 技能定义文件（中文）
├── SKILL_EN.md                 # 技能定义文件（English）
├── README.md                   # 本文件
├── scripts/
│   ├── web_fetch_source.py     # 一键抓取：HTML → JS → API端点提取
│   └── auth_analyzer.py        # 鉴权深度分析：Cookie/CSRF/Token/签名
└── references/
    └── report_template.md      # 分析报告模板
```

---

## 🔧 脚本说明

### web_fetch_source.py

一键完成网站源码抓取和分析：

```bash
python scripts/web_fetch_source.py https://target-website.com/ output_dir
```

自动完成：
- 抓取 HTML → 提取 JS 列表 → 批量抓取 JS → 提取 API 端点 → 保存分析报告

### auth_analyzer.py

对 JS 文件进行鉴权深度分析：

```bash
python scripts/auth_analyzer.py ./output_dir/js/ auth_report.json
```

提取内容：
- Cookie 操作、CSRF 机制、Token 流程
- 请求拦截器、签名算法、OAuth 流程

---

## ⚠️ 关键注意事项

1. **不要用 `web_fetch` 提取源码** — 它返回 AI 摘要，`<script src>` 标签会丢失
2. **PowerShell 中不要内联 Python** — 引号冲突，应先写 `.py` 文件再执行
3. **主入口 JS 不是全部** — 现代前端做代码分割，需搜索 chunk 引用
4. **HTTP 方法和路径在 JS 中常分离** — 需用正则同时捕获

---

## 📄 License

MIT License

---

<a id="english"></a>

## 📖 Introduction

A [CodeBuddy](https://www.codebuddy.ai/) skill that reverse-engineers websites by fetching HTML/JS source code (not browser rendering) to analyze APIs, page layout, authentication flows, and data flows.

### Core Capabilities

1. **Understand** — Figure out what a website does and its functional structure
2. **Operate** — Given credentials (Cookie / Token), directly call APIs to perform actions
3. **Persist** — Produce analysis documents for reuse, no need to re-analyze

### Trigger Scenarios

Triggered when users mention:
- "analyze website", "reverse engineer website", "website API"
- "scrape endpoints", "website structure analysis"
- "help me look at this website" with a URL

---

## 🚀 Quick Start

### Installation

Clone this project into CodeBuddy's skills directory:

```bash
git clone https://github.com/github-yousen/codebuddy-web-reverse-engineer.git ~/.codebuddy/skills/web-reverse-engineer
```

### Usage

In CodeBuddy, simply tell the AI which website you want to analyze:

```
Help me analyze the APIs of https://www.example.com
```

The AI will automatically:
1. Fetch the target website's HTML and all JS files
2. Extract API endpoints from JS
3. Analyze authentication flows (Cookie/CSRF/Token/Signing)
4. Produce a complete analysis report

---

## 📁 Project Structure

```
web-reverse-engineer/
├── SKILL.md                    # Skill definition (Chinese)
├── SKILL_EN.md                 # Skill definition (English)
├── README.md                   # This file
├── scripts/
│   ├── web_fetch_source.py     # One-click: HTML → JS → API endpoint extraction
│   └── auth_analyzer.py        # Auth deep analysis: Cookie/CSRF/Token/Signing
└── references/
    └── report_template.md      # Analysis report template
```

---

## 🔧 Scripts

### web_fetch_source.py

One-click source code fetching and analysis:

```bash
python scripts/web_fetch_source.py https://target-website.com/ output_dir
```

Automatically:
- Fetch HTML → Extract JS list → Batch fetch JS → Extract API endpoints → Save analysis report

### auth_analyzer.py

Deep authentication analysis on JS files:

```bash
python scripts/auth_analyzer.py ./output_dir/js/ auth_report.json
```

Extracts:
- Cookie operations, CSRF mechanisms, Token flows
- Request interceptors, signing algorithms, OAuth flows

---

## ⚠️ Important Notes

1. **Don't use `web_fetch` for source code** — It returns AI summaries, `<script src>` tags are lost
2. **Don't inline Python in PowerShell** — Quote conflicts occur; write `.py` files first
3. **Main JS isn't everything** — Modern frontends use code splitting; search for chunk references
4. **HTTP methods and paths are often separate in JS** — Use regex to capture both simultaneously

---

## 📄 License

MIT License
