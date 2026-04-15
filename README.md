# Web Reverse Engineer

[English](#english) | [中文](#chinese)

---

<a id="english"></a>

## What Is This

A reusable skill specification for reverse-engineering websites. Given a URL and a curl command (with cookies/tokens copied from your browser), it automatically:

1. **Understand** — Discover what a website does: its API endpoints, page structure, and data flows
2. **Operate** — Call those APIs directly using your credentials to get things done
3. **Generate** — Produce a dedicated skill for that specific website, so you never have to reverse-engineer it again

The key insight: **reverse engineering is a means, not the end**. Once you've analyzed a site, the output is an actionable skill you can reuse instantly.

### How It Works with Skill Creator

This skill is designed to pair with a [skill-creator](https://docs.anthropic.com/) workflow:

```
User provides:  URL + curl (with auth headers/cookies)
                          ↓
      web-reverse-engineer analyzes the site
                          ↓
      Extracts: APIs, auth flow, data structures
                          ↓
      skill-creator generates a dedicated skill
                          ↓
      Next time: call that skill directly, no re-analysis needed
```

Example: You provide `https://www.yuque.com` + a curl from your browser. This skill reverse-engineers the Yuque API, then skill-creator packages it into a `yuque` skill that can list/read/create/edit documents — permanently.

### Trigger Scenarios

- "Analyze this website" / "Reverse engineer this site"
- "What APIs does this website have?"
- "Help me scrape the endpoints from ..."
- Or simply paste a URL and say "help me look at this website"

---

## Quick Start

### Install

Clone this skill into your AI tool's skills directory:

```bash
git clone https://github.com/github-yousen/codebuddy-web-reverse-engineer.git <your-skills-dir>/web-reverse-engineer
```

### Use

Tell the AI which website to analyze, and provide a curl with your auth info:

```
Analyze https://www.example.com
Here's a curl with my auth:
curl 'https://www.example.com/api/user' -H 'Cookie: session=abc123' -H 'X-CSRF-Token: xyz'
```

The AI will automatically:
1. Fetch the target website's HTML and all JS files
2. Extract API endpoints from JS source code
3. Analyze authentication flows (Cookie / CSRF / Token / Signing)
4. Produce a complete analysis report
5. *(If skill-creator is available)* Generate a dedicated skill for this website

---

## Project Structure

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

## Scripts

### web_fetch_source.py

One-click source code fetching and analysis:

```bash
python scripts/web_fetch_source.py https://target-website.com/ output_dir
```

Automatically: Fetch HTML → Extract JS list → Batch fetch JS → Extract API endpoints → Save analysis report

### auth_analyzer.py

Deep authentication analysis on JS files:

```bash
python scripts/auth_analyzer.py ./output_dir/js/ auth_report.json
```

Extracts: Cookie operations, CSRF mechanisms, Token flows, Request interceptors, Signing algorithms, OAuth flows

---

## Important Notes

1. **Don't use AI-summarized fetchers for source code** — They return readable summaries where `<script src>` tags are lost. Always fetch raw HTML.
2. **Don't inline Python in PowerShell** — Quote conflicts occur; write `.py` files first.
3. **Main JS isn't everything** — Modern frontends use code splitting; search for chunk references.
4. **HTTP methods and paths are often separate in JS** — Use regex to capture both simultaneously.
5. **Provide curl with auth** — Without credentials, you can only analyze the public surface. A curl from your browser unlocks the full API.

---

## License

MIT License

---

<a id="chinese"></a>

## 这是什么

一个通用的网站逆向分析 skill 规范。给定一个 URL 和一条从浏览器复制的 curl 命令（含 Cookie/Token），它能自动：

1. **理解** — 搞清楚网站能做什么：API 端点、页面结构、数据流
2. **操作** — 用你提供的凭证直接调用 API 完成任务
3. **生成** — 为该网站产出专属 skill，下次不用再逆向

核心理念：**逆向只是手段，不是目的**。分析一次之后，输出的是一个可复用的操作 skill。

### 与 Skill Creator 的联动

本 skill 设计为与 skill-creator 工作流配合使用：

```
用户提供：URL + curl（含鉴权头/Cookie）
                    ↓
    web-reverse-engineer 分析网站
                    ↓
    提取：API、鉴权流程、数据结构
                    ↓
    skill-creator 生成该网站的专属 skill
                    ↓
    下次：直接调用该 skill，无需重新分析
```

示例：你提供 `https://www.yuque.com` + 浏览器复制的 curl。本 skill 逆向分析语雀 API，然后 skill-creator 把它打包成一个 `yuque` skill，可以列出/读取/创建/编辑文档 —— 永久可用。

### 触发场景

- "分析网站"、"逆向网站"、"网站接口"、"抓接口"
- "网站源码分析"、"逆向工程"、"分析API"
- "爬取接口"、"网站结构分析"、"网站白盒分析"
- 或者直接给一个 URL 说"帮我看看这个网站"

---

## 快速开始

### 安装

将本 skill 克隆到你的 AI 工具的 skills 目录：

```bash
git clone https://github.com/github-yousen/codebuddy-web-reverse-engineer.git <你的skills目录>/web-reverse-engineer
```

### 使用

告诉 AI 你想分析哪个网站，并提供含鉴权信息的 curl：

```
分析 https://www.example.com
这是我从浏览器复制的 curl：
curl 'https://www.example.com/api/user' -H 'Cookie: session=abc123' -H 'X-CSRF-Token: xyz'
```

AI 会自动：
1. 抓取目标网站的 HTML 和所有 JS 文件
2. 从 JS 源码中提取 API 端点
3. 分析鉴权流程（Cookie/CSRF/Token/签名）
4. 产出完整的分析报告
5. *（如果 skill-creator 可用）* 生成该网站的专属 skill

---

## 项目结构

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

## 脚本说明

### web_fetch_source.py

一键完成网站源码抓取和分析：

```bash
python scripts/web_fetch_source.py https://target-website.com/ output_dir
```

自动完成：抓取 HTML → 提取 JS 列表 → 批量抓取 JS → 提取 API 端点 → 保存分析报告

### auth_analyzer.py

对 JS 文件进行鉴权深度分析：

```bash
python scripts/auth_analyzer.py ./output_dir/js/ auth_report.json
```

提取内容：Cookie 操作、CSRF 机制、Token 流程、请求拦截器、签名算法、OAuth 流程

---

## 关键注意事项

1. **不要用 AI 摘要工具提取源码** — 它们返回可读摘要，`<script src>` 标签会丢失。始终抓取原始 HTML
2. **PowerShell 中不要内联 Python** — 引号冲突，应先写 `.py` 文件再执行
3. **主入口 JS 不是全部** — 现代前端做代码分割，需搜索 chunk 引用
4. **HTTP 方法和路径在 JS 中常分离** — 需用正则同时捕获
5. **提供含鉴权的 curl** — 没有凭证只能分析公开表面，浏览器复制的 curl 能解锁完整 API

---

## 许可证

MIT License
