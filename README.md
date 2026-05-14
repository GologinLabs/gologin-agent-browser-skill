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

This skill is built around the unified `gologin-agent-browser-cli` package and `gologin-agent-browser` command.

Install the CLI globally:

```bash
npm install -g gologin-agent-browser-cli
```

CLI commands:

- `gologin-agent-browser`
- `gologin-local-agent-browser` compatibility alias from `gologin-agent-browser-cli@0.3.0+`

CLI repo:

- [GologinLabs/agent-browser](https://github.com/GologinLabs/agent-browser)

## Overview

Gologin Agent Browser Skill is for AI agents that need live GoLogin browser sessions, ref-based interaction, semantic find flows, artifacts, and profile/session management. The same CLI now has two runtimes:

- `cloud`: remote GoLogin Cloud Browser sessions for parallel automation without local Orbita.
- `local`: local Orbita profile automation for native OS alignment, local profile cookies, warmup, and persistent account workflows.

## TL;DR

- Use this skill for live browser work: login, dashboard interaction, screenshots, uploads, PDFs, tabs, cookies, storage, warmup, and session cleanup.
- Use `--runtime cloud` or no runtime flag for Cloud Browser.
- Use `--runtime local` for local Orbita profile work.
- Do not route local profile work to the deprecated `gologin-local-agent-browser-cli` package. Use `gologin-agent-browser-cli`.
- Do not drift into `gologin-web-access` for scrape-first reading/extraction tasks.
- For temporary cloud sessions, do not invent free proxies and do not assume `--proxy-country` works. Use an existing cloud `--profile` when country traffic, browser version, or viewport must be explicit.
- Use explicit `--session` ids for parallel cloud sessions.
- End by cleaning up with `close`, `close --all`, or `sessions --prune`.

It is built for:

- opening live cloud browser sessions
- opening local Orbita profile sessions
- capturing page snapshots with refs like `@e1`
- clicking, typing, filling, selecting, and waiting
- semantic `find` flows
- screenshots, PDFs, uploads, and session inspection
- daemon diagnostics with `doctor`
- tabs, cookies, storage export/import, and JavaScript eval
- browser history actions like `back`, `forward`, and `reload`
- local profile commands such as `profile-create`, `profile-update`, `run`, `batch`, `jobs`, and `job`

It is not the best default for scrape-first reading, extraction, mapping, or crawling on a known site. For those tasks, prefer `gologin-web-access-skill`.

## Capabilities

- Diagnostics with `doctor`
- Browser sessions with `open`, `sessions`, and `current`
- Runtime selection with `--runtime cloud`, `--runtime local`, `--cloud`, and `--local`
- Snapshot-driven interaction with `snapshot`, `click`, `type`, and `fill`
- Semantic actions with `find`
- Readback helpers with `get`
- Tab control with `tabs`, `tabopen`, `tabfocus`, and `tabclose`
- Cookie and storage helpers with `cookies`, `cookies-import`, `storage-export`, `storage-import`, and `eval`
- History helpers with `back`, `forward`, and `reload`
- Upload, screenshot, and PDF artifact generation
- Local profile management and runbooks through the local runtime
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
- `GOLOGIN_AGENT_BROWSER_RUNTIME`
- `GOLOGIN_EXECUTABLE_PATH`

## Quickstart

Cloud runtime:

```bash
gologin-agent-browser open https://example.com
gologin-agent-browser snapshot -i
gologin-agent-browser click @e3
gologin-agent-browser tabs
gologin-agent-browser cookies --json
gologin-agent-browser close
```

Local runtime:

```bash
gologin-agent-browser --runtime local doctor --json
gologin-agent-browser --runtime local profiles --remote --json
gologin-agent-browser --runtime local open https://example.com --profile your_profile_id
gologin-agent-browser --runtime local snapshot -i
gologin-agent-browser --runtime local close
```

Parallel cloud pattern:

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
- the task is a live cloud-browser login, dashboard, or session-hygiene flow
- the task depends on a local Orbita profile, persistent cookies, profile preparation, or repeated SPA navigation

Use another GoLogin skill when:

- the task is mostly reading, scraping, mapping, crawling, or structured extraction on a known site -> `gologin-web-access-skill`

## References

- [`SKILL.md`](./SKILL.md)
- [`tools.md`](./tools.md)
- [`examples/`](./examples)
- [`workflows/`](./workflows)
