<div align="center">

<img src="img/logo.png" alt="Reina" width="180" />

# Reina

### A desktop AI agent — multi-agent teams, MCP & Skills, bring your own models

**English** · [中文](./README.zh-CN.md)

[![Release](https://img.shields.io/github/v/release/Reina-Agent/Reina?color=blue)](https://github.com/Reina-Agent/Reina/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/Reina-Agent/Reina/total?color=brightgreen)](https://github.com/Reina-Agent/Reina/releases)
[![License: AGPL v3](https://img.shields.io/badge/License-AGPL_v3-blue.svg)](./LICENSE)
[![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20macOS-lightgrey.svg)](#-download--run)
![GitHub stars](https://img.shields.io/github/stars/Reina-Agent/Reina?style=social)

[Download](#-download--run) · [Features](#-features) · [Learn the internals](#-learn-the-internals) · [Build from source](#-build-from-source)

</div>

---

<div align="center">
  <img src="img/demo.gif" alt="Reina reading through a local project and answering" width="90%" />
</div>

---

**Reina is an open-source desktop AI agent.** It holds a continuous conversation around your local workspace — understanding your projects, organizing information, and driving multi-step tasks forward — and when one pair of hands isn't enough, it fans the work out to a coordinated team of sub-agents. Everything runs as a plain desktop app: you bring your own models and API keys, and nothing has to pass through a vendor backend.

> [!NOTE]
> Reina brings its own model layer: you configure your own models and API keys in settings (stored locally in `~/.reina/`) and decide which provider to use. No product HTTP server, no cloud backend.

## ✨ Features

- 🧠 **Workspace-aware sessions** — a continuous conversation organized around your local projects, files, and tasks. Long sessions survive context compaction without forgetting the original goal, and every session persists so you can pause and pick up seamlessly.
- 🤝 **Multi-agent team mode** — a coordinator agent decomposes a goal into a DAG of subtasks and drives worker agents through phase gates until every branch lands — no coordinator stalls, no premature "done".
- 🧩 **MCP & Skills, with a marketplace** — connect MCP servers and install skills from built-in marketplaces; the agent can even search for and install new skills for itself mid-task.
- 🔑 **Bring your own models** — configure any provider you like and switch per session. API keys live in `~/.reina/`, never reach the UI layer, and stay fully under your control.
- 🛡️ **Permissioned & transparent** — side-effecting actions go through approval prompts; every step is visible, pausable, and resumable.
- 🖥️ **Multi-window desktop UX** — chat / workspace / settings in cleanly separated surfaces, hugging your local workflow instead of living in a browser tab. Auto-updates keep you on the latest build.

## 📚 Learn the internals

Curious how a coding agent like this actually works under the hood? Reina's core mechanisms — the agent loop, context compaction, prompt-cache engineering, subagent watchdogs, permission gates, the provider compatibility layer — are taught in **[learn-agent](https://github.com/7-e1even/learn-agent)**: 15 runnable, zero-dependency lessons, each ported and simplified from this codebase. Read the lesson, then come back and find the real implementation here.

## 📦 Download & run

Download the build for your OS from [Releases](https://github.com/Reina-Agent/Reina/releases):

- **Windows** — installer (NSIS) and portable build.
- **macOS** — DMG or ZIP.

Install or unzip and run. First time: pick a workspace → enter your model and API key in settings → type a goal or task.

## 🛠️ Build from source

```bash
git clone https://github.com/Reina-Agent/Reina.git
cd reina
npm install
npm run build:desktop   # builds main process + agent-host + renderer
npm run desktop         # launches the desktop app
```

> [!TIP]
> Requires Node.js >= 22. Architecture at a glance below.

> [!NOTE]
> The chat UI honors your OS **reduce-motion** setting. Transitions like the expandable tool-call cards are intentionally disabled when "reduce motion" is on — turn it off in your system settings (Windows: Settings → Accessibility → Visual effects → Animation effects) to see them.

<details>
<summary>Architecture at a glance</summary>

```text
renderer (React + Tailwind v4: chat / workspace / settings windows)
  → preload bridge
  → Electron main IPC
  → agent-host (Node child process, JSON-line stdio)
  → AgentEngine
  → model providers and local tools
```

Runs entirely as a local desktop app: no product HTTP server, no CLI product entry point.

</details>

## 🤝 Contributing

Issues and PRs welcome! Newcomers can start with [`good first issue`](https://github.com/Reina-Agent/Reina/labels/good%20first%20issue) tickets.

## 🔒 Security

Found a security issue? Please report it privately via [GitHub Security Advisories](https://github.com/Reina-Agent/Reina/security/advisories/new) — **don't** open a public issue.

## 📄 License

Reina is licensed under [AGPL-3.0](./LICENSE).

You may freely use, modify, and distribute it, but **any modified version — including a service offered over a network — must release its complete source under AGPL-3.0**. For use in closed-source / commercial products, contact the author for a commercial license.

---

<div align="center">
<sub>If Reina is useful to you, drop a ⭐ Star — it's the biggest encouragement for a solo developer.</sub>
<br/>
<sub>Copyright © 2026 7-e1even</sub>
</div>
