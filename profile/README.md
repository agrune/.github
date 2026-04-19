<div align="center">

<img src="https://github.com/agrune/agrune/raw/main/packages/devtools/icon-128.png" width="80" height="80" alt="agrune logo" />

# agrune

**Manifest-driven, CDP-only, local-first browser automation for AI agents**

<!-- TODO 2026-04-18: Chrome Web Store 배지는 v1.1 CDP-only 피봇 이후 더 이상 canonical 배포 채널이 아닙니다. 재설치/링크 삭제 판단은 org maintainer 수동 결정. -->
[![Version](https://img.shields.io/npm/v/@agrune/mcp?style=flat-square&label=version&color=cb3837)](https://www.npmjs.com/package/@agrune/mcp)
[![Chrome Web Store](https://img.shields.io/chrome-web-store/v/gchelkphnedibjihiomlbpjhjlajplke?style=flat-square&label=chrome%20web%20store&color=4285F4)](https://chromewebstore.google.com/detail/agrune/gchelkphnedibjihiomlbpjhjlajplke) <!-- deprecated -->
[![Downloads](https://img.shields.io/npm/dm/@agrune/mcp?style=flat-square&label=downloads&color=cb3837)](https://www.npmjs.com/package/@agrune/mcp)
[![License](https://img.shields.io/github/license/agrune/agrune?style=flat-square&color=yellow)](https://github.com/agrune/agrune/blob/main/LICENSE)

</div>

<!-- ============================================================
     HERO DEMO GIF
     Shooting guide: Record an AI agent interacting with a web app
     via a manifest-defined control surface — clicking buttons,
     filling forms, dragging elements. Aurora pointer visible.
     ~800px wide, 10-15 second loop, GIF or WebM. Replace the
     placeholder below once recorded.
     ============================================================ -->

<div align="center">
<img src="https://placehold.co/800x400/1a1a2e/8b949e?text=Demo+GIF+%E2%80%94+Coming+Soon" alt="agrune demo — AI agent automating a web page" width="800" />
</div>

## What is agrune?

**agrune** is an MCP (Model Context Protocol) server that lets AI agents see and control web pages — in a real Chrome instance, driven over the Chrome DevTools Protocol (CDP). The control surface for every interaction is declared in an external **manifest**: one typed `manifest.ts` file, written with `@agrune/manifest` and (for owned apps) a one-line React root-import.

Everything runs **100% locally**. No cloud. No browser add-on. No data leaves your machine.

```ts
// src/manifest.ts
import { defineManifest, defineGroup, defineTarget } from '@agrune/manifest'

export default defineManifest({
  groups: [
    defineGroup({
      groupId: 'login',
      route: '/login',
      targets: [
        defineTarget({
          targetId: 'email_input',
          selector: { role: { name: 'textbox' }, css: 'input[type=email]' },
          actionKinds: ['fill'],
        }),
        defineTarget({
          targetId: 'submit_button',
          selector: { role: { name: 'button' }, text: 'Sign in' },
          actionKinds: ['click'],
        }),
      ],
    }),
  ],
})
```

## Use Cases

| | Use Case | Status | Description |
|---|---|---|---|
| :test_tube: | **Dev QA** | `Coming Soon` | AI agents run E2E tests. No brittle selectors — the manifest tells the agent what each target does. |
| :world_map: | **Site Registry** | `Coming Soon` | Pre-mapped manifests for popular sites. Agents pull them via `agrune maps add <host>`. |
| :zap: | **Platform Automation** | `Coming Soon` | AI autonomously performs tasks on supported sites via manifest + `defineMacro` flows. |

> All use cases are under active development — v0.5 **Manifest Pivot** is the current milestone.

<!-- ============================================================
     MANIFEST GIF
     Shooting guide: Split-view recording — left side shows
     manifest.ts being authored (defineTarget / defineRepeat /
     defineMacro), right side shows the AI agent resolving those
     targets in a live Chrome instance via CDP. ~800px wide,
     10-15 second loop. Replace the placeholder below once recorded.
     ============================================================ -->

<div align="center">
<img src="https://placehold.co/800x400/1a1a2e/8b949e?text=Manifest+%E2%86%92+Control+Split+View+%E2%80%94+Coming+Soon" alt="Manifest to control split view" width="800" />
</div>

## Key Features

| | | |
|:---:|:---:|:---:|
| :dart: **13 MCP Tools** | :lock: **100% Local** | :sparkles: **Live DevTools Webapp** |
| Click, fill, drag, wait, read, focus, `manifest_load`, `macro_run` — full browser control via MCP | Zero cloud. CDP straight to your own Chrome. No browser add-on | Command log, HITL toolbar, session routing, recorder overlay at http://localhost:47654/devtools |
| :label: **Typed Manifests** | :robot: **Agent Agnostic** | :zap: **Self-Healing Sessions** |
| `@agrune/manifest` SDK types `defineTarget` / `defineRepeat` / `defineMacro` at compile time | Works with Claude, GPT, Gemini — any MCP-speaking agent | Auto-reattach on tab crashes, supervisor-driven recovery, `recovered` flag on tool responses |

## Why agrune?

| | agrune | Playwright | BrowserUse | Chrome DevTools |
|---|:---:|:---:|:---:|:---:|
| **AI-native (MCP)** | :white_check_mark: | :x: | :white_check_mark: | :x: |
| **Visual feedback** | :white_check_mark: Aurora cursor | :x: | :warning: Highlight only | :x: |
| **Semantic targeting** | :white_check_mark: Manifest target mapping | CSS / XPath | Vision-based | CSS / XPath |
| **Real browser** | :white_check_mark: | Headless default | :white_check_mark: | :white_check_mark: |
| **Zero cloud** | :white_check_mark: 100% local | :white_check_mark: | :x: Cloud API | :white_check_mark: |
| **Setup** | 1 command + 1 manifest | Config + scripts | API key + config | Manual protocol |

> **The key difference:** Other tools target elements by CSS selectors or screenshots. agrune uses **manifest-defined target mappings** — the AI knows *what* a target does, not just where it is. For owned React apps, a one-line root-import (`<AgruneDevtools />`) gives you component-identity selectors that survive refactors. For external sites, the same manifest falls back to a `role > text > testId > stable attr > css` ladder.

## Architecture

```
┌──────────┐     ┌──────────────────────┐     ┌────────┐     ┌──────────────┐
│ AI Agent │◄───►│ @agrune/mcp (stdio)  │◄───►│ Chrome │◄───►│  Web Page    │
└──────────┘     └──────────────────────┘     └────────┘     └──────────────┘
                  + DevTools webapp :47654     CDP            manifest.ts
                                                              (defineTarget)
```

## Quick Start

**1. Install the MCP server**

```sh
npm install -g @agrune/mcp
```

**2. Launch agrune**

```sh
agrune                     # Chrome launch + DevTools webapp on :47654
agrune --attach ws://...   # attach to an existing Chrome (--remote-debugging-port)
agrune --help              # full flag reference
```

**3. Author a manifest**

```sh
agrune manifest validate src/manifest.ts --url https://your-app.local
agrune manifest dev src/manifest.ts         # DevTools recorder + ts-morph merge watcher
```

**4. Connect your MCP-compatible agent** to the stdio server and start interacting.

See the monorepo [README](https://github.com/agrune/agrune#readme) for a deeper tour, and [`.agents/skills/manifest/SKILL.md`](https://github.com/agrune/agrune/blob/main/.agents/skills/manifest/SKILL.md) for the authoritative AI authoring workflow.

## Current Milestone — v0.5 Manifest Pivot

Active on branch [`feat/v0.5-manifest`](https://github.com/agrune/agrune/tree/feat/v0.5-manifest):

- `@agrune/manifest` — typed authoring SDK (`defineManifest` / `defineTarget` / `defineRepeat` / `defineMacro`)
- `@agrune/react` — one-line root-import (`<AgruneDevtools />`) for component-identity selectors via React fiber
- DevTools recorder overlay + `agrune manifest dev` watcher
- Registry rollout (`github.com/agrune/maps`) planned as Phase 18 REGISTRY

---

<div align="center">

[Documentation](https://github.com/agrune/agrune) · [Chrome Web Store](https://chromewebstore.google.com/detail/agrune/gchelkphnedibjihiomlbpjhjlajplke) <!-- deprecated --> · [npm](https://www.npmjs.com/org/agrune) · [Contributing](https://github.com/agrune/agrune/blob/main/CONTRIBUTING.md)

</div>
