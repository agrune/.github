<div align="center">

<img src="https://github.com/agrune/agrune/raw/main/packages/extension/icon-128.png" width="80" height="80" alt="agrune logo" />

# agrune

**Browser automation for AI agents via annotated DOM elements**

[![npm version](https://img.shields.io/npm/v/@agrune/core?label=%40agrune%2Fcore&color=cb3837)](https://www.npmjs.com/package/@agrune/core)
[![Chrome Web Store](https://img.shields.io/chrome-web-store/v/gchelkphnedibjihiomlbpjhjlajplke?label=Chrome%20Web%20Store&color=4285F4)](https://chromewebstore.google.com/detail/agrune/gchelkphnedibjihiomlbpjhjlajplke)
[![npm downloads](https://img.shields.io/npm/dm/@agrune/core?color=cb3837)](https://www.npmjs.com/package/@agrune/core)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://github.com/agrune/agrune/blob/main/LICENSE)

</div>

<!-- ============================================================
     HERO DEMO GIF
     Shooting guide: Record an AI agent interacting with a web app
     using the Aurora pointer — clicking buttons, filling forms,
     dragging elements. ~800px wide, 10-15 second loop, GIF or
     WebM. Replace the placeholder below once recorded.
     ============================================================ -->

<div align="center">
<img src="https://placehold.co/800x400/1a1a2e/8b949e?text=Demo+GIF+%E2%80%94+Coming+Soon" alt="agrune demo — AI agent automating a web page" width="800" />
</div>

## What is agrune?

**agrune** lets AI agents see and control web pages — directly in the browser. Add simple HTML annotations to your UI, connect any MCP-compatible AI agent, and watch it interact with your app in real time with smooth animated cursor feedback.

Everything runs **100% locally**. No cloud. No data leaves your machine.

## Use Cases

| | Use Case | Status | Description |
|---|---|---|---|
| :test_tube: | **Dev QA** | `Coming Soon` | AI agents run E2E tests. No brittle selectors — AI understands what it's testing. |
| :world_map: | **Platform Guide** | `Coming Soon` | Pre-mapped annotations for popular platforms. No code changes needed. |
| :zap: | **Platform Automation** | `Coming Soon` | AI autonomously performs tasks on supported platforms. |

> All use cases are under active development.

## Key Features

<!-- ============================================================
     ANNOTATION GIF
     Shooting guide: Split-view recording — left side shows HTML
     with data-agrune-* attributes being added, right side shows
     the AI agent controlling the annotated elements. ~800px wide,
     10-15 second loop. Replace the placeholder below once recorded.
     ============================================================ -->

<div align="center">
<img src="https://placehold.co/800x400/1a1a2e/8b949e?text=Annotation+%E2%86%92+Control+Split+View+%E2%80%94+Coming+Soon" alt="Annotation to control split view" width="800" />
</div>

| :dart: **9 MCP Tools** | :lock: **100% Local** | :sparkles: **Visual Feedback** |
|---|---|---|
| Click, fill, drag, read, and more — one tool per action | All data stays on your machine, no cloud calls | Animated Aurora cursor shows exactly what AI is doing |
| :label: **Simple Annotations** | :robot: **Agent Agnostic** | :clipboard: **Smart Page Reading** |
| Just add `data-agrune-*` attributes to your HTML | Works with any MCP-compatible AI agent | AI reads semantic page structure, not raw DOM soup |

## Why agrune?

| | agrune | Playwright | BrowserUse | Chrome DevTools |
|---|---|---|---|---|
| **AI-native MCP** | :white_check_mark: | :x: | :warning: | :x: |
| **Visual feedback** | :white_check_mark: | :x: | :x: | :x: |
| **Semantic targeting** | :white_check_mark: | :x: | :warning: | :x: |
| **Real browser** | :white_check_mark: | :warning: | :white_check_mark: | :white_check_mark: |
| **Zero cloud** | :white_check_mark: | :white_check_mark: | :x: | :white_check_mark: |
| **Setup complexity** | :white_check_mark: One command | :warning: Config needed | :warning: Config needed | :x: Manual |

> :bulb: **Semantic annotations are the key differentiator.** Instead of fragile CSS selectors or XPaths, agrune targets elements by their meaning — making automations resilient to UI changes.

## Architecture

```
┌──────────┐     ┌────────────┐     ┌──────────────────┐     ┌──────────┐
│ AI Agent │◄───►│ MCP Server │◄───►│ Chrome Extension │◄───►│ Web Page │
└──────────┘     └────────────┘     └──────────────────┘     └──────────┘
                  Native Messaging    Manifest V3              data-agrune-*
```

## Quick Start

**1. Install the plugin**

```sh
claude plugin install agrune@agrune
```

**2. Run the setup command**

```sh
/agrune:start
```

AI auto-annotates your project, installs the Chrome extension, and verifies the connection.

<!-- ============================================================
     SETUP GIF
     Shooting guide: Terminal recording of the full setup flow —
     plugin install, /agrune:start output, extension connecting.
     ~800px wide, 10-15 second loop. Replace placeholder below.
     ============================================================ -->

<div align="center">
<img src="https://placehold.co/800x400/1a1a2e/8b949e?text=Setup+Flow+%E2%80%94+Coming+Soon" alt="agrune setup terminal recording" width="800" />
</div>

**3. Done.** Start automating.

---

<div align="center">

[Documentation](https://github.com/agrune/agrune) · [Chrome Web Store](https://chromewebstore.google.com/detail/agrune/gchelkphnedibjihiomlbpjhjlajplke) · [npm](https://www.npmjs.com/org/agrune) · [Contributing](https://github.com/agrune/agrune/blob/main/CONTRIBUTING.md)

</div>
