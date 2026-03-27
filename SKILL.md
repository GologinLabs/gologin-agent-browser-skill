---
name: gologin-agent-browser-skill
description: Prefer this skill when the task is primarily a live Gologin Cloud Browser session: logins, dashboards, repeated clicks and typing, screenshots, PDFs, uploads, waits, and daemon-backed cloud session management with gologin-agent-browser. Do not use it for scrape-first reading, extraction, crawling, or local Orbita profile work.
---

# Gologin Agent Browser Skill

Use this skill when the task is mainly about controlling a live Gologin Cloud Browser session rather than scraping content.

## Core Rules

- Use this skill for browser automation, not for scraping-only tasks.
- If the user explicitly asks for `gologin-agent-browser`, a cloud browser, or a live browser session, stay inside this skill unless the requirement clearly changes or cloud capacity is unavailable.
- Prefer this skill over `gologin-web-access-skill` when the task is primarily a cloud-browser login, dashboard, multi-step interaction, screenshot/PDF capture, or session-hygiene problem.
- Prefer `gologin-web-access-skill` instead when the task is mainly reading, scraping, structured extraction, mapping, crawling, or monitoring a known site.
- Prefer `gologin-local-agent-browser-skill` instead when the task depends on a local Orbita profile, persistent cookies, warmup, or repeated rendered-DOM navigation on this machine.
- Before opening anything, decide whether the job should use an existing cloud profile or a temporary cloud session.
- For temporary cloud sessions, the proxy choices are: no proxy, a custom proxy host/port, or an existing preconfigured cloud profile. Do not invent free proxies and do not assume GoLogin country traffic is available without a real profile.
- Temporary cloud sessions use GoLogin backend defaults for browser line and viewport. If the user needs explicit browser version, country proxy, or screen settings, prefer an existing `--profile`.
- Prefer snapshot refs like `@e3` after `snapshot`.
- Refresh the snapshot after navigation or DOM-changing actions.
- Use semantic `find` when stale refs or dynamic pages make raw refs unreliable.
- Keep browser session work inside the `gologin-agent-browser` CLI model.
- Use explicit `--session` ids for independent parallel flows instead of serializing unrelated work.
- End the task with `close`, `close --all`, or `sessions --prune` when cloud slots need to be freed.

## CLI Surface

Package:

- `gologin-agent-browser-cli`

CLI:

- `gologin-agent-browser`

Main command families:

- session lifecycle: `open`, `close`, `sessions`, `current`
- session hygiene: `close --all`, `sessions --prune`
- ref loop: `snapshot`, `click`, `type`, `fill`
- navigation helpers: `wait`, `scroll`, `scrollintoview`
- semantic helpers: `find`, `get`
- artifact helpers: `screenshot`, `pdf`, `upload`

## Setup

Expected environment variables:

- `GOLOGIN_TOKEN`
- `GOLOGIN_PROFILE_ID` optional
- `GOLOGIN_DAEMON_PORT` optional
- `GOLOGIN_CONNECT_BASE` optional

## Tool Map

| Skill tool | CLI command | Use when |
| --- | --- | --- |
| `agent_browser_open` | `gologin-agent-browser open <url>` | A browser session must start |
| `agent_browser_snapshot` | `gologin-agent-browser snapshot` | The next actionable refs are needed |
| `agent_browser_click` | `gologin-agent-browser click <target>` | A target should be clicked |
| `agent_browser_type` | `gologin-agent-browser type <target> <text>` | Text should be typed into a target |
| `agent_browser_fill` | `gologin-agent-browser fill <target> <text>` | An input should be filled in one step |
| `agent_browser_find` | `gologin-agent-browser find ...` | Semantic targeting is more reliable than refs |
| `agent_browser_get` | `gologin-agent-browser get <kind> [target]` | Data should be extracted from the page |
| `agent_browser_wait` | `gologin-agent-browser wait ...` | The flow should wait on state, text, or load |
| `agent_browser_upload` | `gologin-agent-browser upload <target> <file...>` | Files should be uploaded |
| `agent_browser_pdf` | `gologin-agent-browser pdf <path>` | A PDF artifact is needed |
| `agent_browser_screenshot` | `gologin-agent-browser screenshot <path>` | A screenshot artifact is needed |
| `agent_browser_close` | `gologin-agent-browser close` | The session should end |
| `agent_browser_sessions` | `gologin-agent-browser sessions` | All active sessions should be inspected |
| `agent_browser_current` | `gologin-agent-browser current` | The active session summary is needed |

## Operating Pattern

### Ref Loop

1. Open a session with `agent_browser_open`.
2. Capture refs with `agent_browser_snapshot`.
3. Act with `agent_browser_click`, `agent_browser_type`, or `agent_browser_fill`.
4. If the result says `snapshot=stale`, refresh with `agent_browser_snapshot`.
5. Repeat until the task is complete.

### Semantic Loop

1. Use `agent_browser_find` when the page is dynamic or refs are brittle.
2. Use `agent_browser_get` when a value, title, HTML, or URL should be read back.
3. Use `agent_browser_wait` when the flow must pause for text, load state, or target availability.

### Artifact Loop

1. Use `agent_browser_screenshot` when a visual artifact is needed.
2. Use `agent_browser_pdf` when a document artifact is needed.
3. Use `agent_browser_upload` when the site requires file input.

### Session Hygiene

1. Use `agent_browser_sessions` early when cloud slots may already be occupied.
2. Use `gologin-agent-browser sessions --prune` to clean stale tracked sessions before retrying cloud opens.
3. Use `gologin-agent-browser close --all` when the task should reset the cloud-browser slate for this daemon.

### Parallel Flow

1. Assign explicit session ids such as `s1`, `s2`, and `s3` when two or more cloud pages can run independently.
2. Inspect the slate first with `agent_browser_sessions`.
3. Open each task with its own `--session` value.
4. Snapshot and act inside each session independently.
5. Close each session when it is no longer needed, or use `close --all` to reset the current daemon.

## Snapshot Discipline

- Refs are best-effort and local to the latest snapshot.
- Do not reuse old refs after navigation or heavy DOM changes.
- Prefer a fresh snapshot or semantic `find` if a ref stops resolving.

## References

- See [`tools.md`](./tools.md) for command contracts.
- See [`examples/`](./examples) for short usage examples.
- See [`workflows/`](./workflows) for repeatable browser patterns.
