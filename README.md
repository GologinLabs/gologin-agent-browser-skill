# Gologin Agent Browser Skill

## Install This Skill

Install the skill with:

```bash
npx skills add GologinLabs/gologin-agent-browser-skill
```

Standalone repo:

- [GologinLabs/gologin-agent-browser-skill](https://github.com/GologinLabs/gologin-agent-browser-skill)

Monorepo install:

```bash
npx skills add GologinLabs/agent-skills@gologin-agent-browser-skill
```

## Required CLI

This skill is built around the `gologin-agent-browser-cli` package and `gologin-agent-browser` command.

Install the CLI globally:

```bash
npm install -g gologin-agent-browser-cli
```

CLI command:

- `gologin-agent-browser`

CLI repo:

- [GologinLabs/agent-browser](https://github.com/GologinLabs/agent-browser)

## Overview

Gologin Agent Browser Skill is a browser-only skill for AI agents that need live browser sessions, ref-based interaction, semantic find flows, and artifact capture through Gologin Cloud Browser.

## TL;DR

- Use this skill only for live cloud-browser work: login, dashboard interaction, screenshots, uploads, PDFs, tabs, cookies, storage, and session cleanup.
- Do not drift into `gologin-web-access` for scrape-first reading/extraction tasks, and do not drift into `gologin-local-agent-browser` unless the task truly requires a local Orbita profile.
- For temporary cloud sessions, do not invent free proxies and do not assume `--proxy-country` works. Use an existing cloud `--profile` when country traffic, browser version, or viewport must be explicit.
- Use explicit `--session` ids for parallel cloud sessions.
- End by cleaning up with `close`, `close --all`, or `sessions --prune`.

It is built for:

- opening live cloud browser sessions
- capturing page snapshots with refs like `@e1`
- clicking, typing, filling, selecting, and waiting
- semantic `find` flows
- screenshots, PDFs, uploads, and session inspection
- daemon diagnostics with `doctor`
- tabs, cookies, storage export/import, and JavaScript eval
- browser history actions like `back`, `forward`, and `reload`

It does not cover scraping-only SDK integration. For that, use `gologin-scraping-skill`.
It is also not the best default for scrape-first reading, extraction, mapping, or crawling on a known site. For those tasks, prefer `gologin-web-access-skill`. If the work depends on a local Orbita profile or persistent local session reuse, prefer `gologin-local-agent-browser-skill`.

## Capabilities

- Diagnostics with `doctor`
- Browser sessions with `open`, `sessions`, and `current`
- Snapshot-driven interaction with `snapshot`, `click`, `type`, and `fill`
- Semantic actions with `find`
- Readback helpers with `get`
- Tab control with `tabs`, `tabopen`, `tabfocus`, and `tabclose`
- Cookie and storage helpers with `cookies`, `cookies-import`, `storage-export`, `storage-import`, and `eval`
- History helpers with `back`, `forward`, and `reload`
- Upload, screenshot, and PDF artifact generation
- Daemon-backed persistence across commands

## Setup

Set your token:

```bash
export GOLOGIN_TOKEN="your_gologin_token"
export GOLOGIN_PROFILE_ID="optional_profile_id"
```

Optional environment variables:

- `GOLOGIN_DAEMON_PORT`
- `GOLOGIN_CONNECT_BASE`

## Quickstart

```bash
gologin-agent-browser open https://example.com
gologin-agent-browser snapshot -i
gologin-agent-browser click @e3
gologin-agent-browser tabs
gologin-agent-browser cookies --json
gologin-agent-browser close
```

Parallel pattern:

```bash
gologin-agent-browser open https://example.com --session s1
gologin-agent-browser open https://example.org --session s2
gologin-agent-browser sessions
gologin-agent-browser close --all
```

## When To Use This Skill

Use this skill when:

- the task needs a real browser session
- the agent must click, type, or navigate
- the task should follow the snapshot -> ref -> action model
- uploads, screenshots, or PDFs are required
- the task is primarily a live cloud-browser login, dashboard, or session-hygiene flow

Use another GoLogin skill when:

- the task is mostly reading, scraping, mapping, crawling, or structured extraction on a known site -> `gologin-web-access-skill`
- the task depends on a local Orbita profile, persistent cookies, profile preparation, or repeated SPA navigation -> `gologin-local-agent-browser-skill`

## References

- [`SKILL.md`](./SKILL.md)
- [`tools.md`](./tools.md)
- [`examples/`](./examples)
- [`workflows/`](./workflows)
