<div align="center">

# Agrune

**A CDP-based MCP server for local AI agents**

[![npm](https://img.shields.io/npm/v/agrune?style=flat-square&label=npm&color=cb3837)](https://www.npmjs.com/package/agrune)
[![downloads](https://img.shields.io/npm/dm/agrune?style=flat-square&label=downloads&color=cb3837)](https://www.npmjs.com/package/agrune)
[![license](https://img.shields.io/github/license/agrune/agrune?style=flat-square&color=yellow)](https://github.com/agrune/agrune/blob/main/LICENSE)

</div>

Agrune lets MCP-compatible agents control a real Chrome session through Chrome DevTools Protocol. The agent talks to public MCP tools such as `browser_open_tab`, `browser_get_targets`, `browser_click`, and `browser_fill`; the page supplies the optimized control manifest at `window.__agrune_manifest__`.

The current product scope is intentionally focused: a local MCP server, a managed or attached Chrome instance, compact page-owned targets, and browser-control tools for agents. It is distributed as the `agrune` npm package and runs with `npx agrune@latest`.

## Quick Start

Add Agrune to your MCP host config:

```json
{
  "mcpServers": {
    "agrune": {
      "command": "npx",
      "args": ["-y", "agrune@latest"]
    }
  }
}
```

Agrune starts over stdio and launches Chrome lazily on the first browser-control tool call.

You can also run the server directly:

```sh
npx agrune@latest
npx agrune@latest --headless
npx agrune@latest --isolated
npx agrune@latest --attach http://127.0.0.1:9222
```

## How It Works

1. An MCP host starts Agrune before the agent session.
2. Agrune launches Chrome or attaches to an existing CDP endpoint.
3. The agent opens a page with `browser_open_tab`.
4. The page exposes its manifest through `window.__agrune_manifest__`.
5. The agent reads compact targets with `browser_get_targets` and acts with `browser_*` tools.

Agents should not need to read manifest files, load manifests manually, use CSS selectors directly, or know CDP details.

## Public Tool Surface

Agrune exposes browser-focused MCP tools for tab control, target discovery, clicking, filling, dragging, pointer input, waiting, reading visible content, and runtime configuration. Current tools include:

`browser_list_tabs`, `browser_open_tab`, `browser_focus_tab`, `browser_get_targets`, `browser_click`, `browser_double_click`, `browser_right_click`, `browser_hover`, `browser_long_press`, `browser_fill`, `browser_drag`, `browser_pointer`, `browser_wait_for`, `browser_read`, and `browser_update_config`.

## Packages

The public npm package is [`agrune`](https://www.npmjs.com/package/agrune). Internal packages in the monorepo provide the MCP server, CDP browser driver, runtime injector, shared contracts, manifest schema, and tests.

## Links

[Repository](https://github.com/agrune/agrune) · [npm package](https://www.npmjs.com/package/agrune)
