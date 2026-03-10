# Gologin Agent Browser Skill

## Install This Skill

Install the skill with:

```bash
npx skills add GologinLabs/gologin-agent-browser-skill@gologin-agent-browser-skill
```

Standalone repo:

- [GologinLabs/gologin-agent-browser-skill](https://github.com/GologinLabs/gologin-agent-browser-skill)

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

It is built for:

- opening live cloud browser sessions
- capturing page snapshots with refs like `@e1`
- clicking, typing, filling, selecting, and waiting
- semantic `find` flows
- screenshots, PDFs, uploads, and session inspection

It does not cover scraping-only SDK integration. For that, use `gologin-scraping-skill`.

## Capabilities

- Browser sessions with `open`, `sessions`, and `current`
- Snapshot-driven interaction with `snapshot`, `click`, `type`, and `fill`
- Semantic actions with `find`
- Readback helpers with `get`
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
gologin-agent-browser close
```

## When To Use This Skill

Use this skill when:

- the task needs a real browser session
- the agent must click, type, or navigate
- the task should follow the snapshot -> ref -> action model
- uploads, screenshots, or PDFs are required

## References

- [`SKILL.md`](./SKILL.md)
- [`tools.md`](./tools.md)
- [`examples/`](./examples)
- [`workflows/`](./workflows)
