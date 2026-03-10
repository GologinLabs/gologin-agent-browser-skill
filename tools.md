# Tool Contracts

This skill wraps the `gologin-agent-browser` CLI and its daemon-backed browser model.

## Summary

| Skill tool | CLI command | Requires | Returns |
| --- | --- | --- | --- |
| `agent_browser_open` | `open` | `GOLOGIN_TOKEN` | Session summary |
| `agent_browser_snapshot` | `snapshot` | `GOLOGIN_TOKEN` | Snapshot with refs |
| `agent_browser_click` | `click` | `GOLOGIN_TOKEN` | Action status |
| `agent_browser_type` | `type` | `GOLOGIN_TOKEN` | Action status |
| `agent_browser_fill` | `fill` | `GOLOGIN_TOKEN` | Action status |
| `agent_browser_find` | `find` | `GOLOGIN_TOKEN` | Semantic action result |
| `agent_browser_get` | `get` | `GOLOGIN_TOKEN` | Extracted value |
| `agent_browser_wait` | `wait` | `GOLOGIN_TOKEN` | Wait status |
| `agent_browser_upload` | `upload` | `GOLOGIN_TOKEN` | Upload status |
| `agent_browser_pdf` | `pdf` | `GOLOGIN_TOKEN` | PDF path |
| `agent_browser_screenshot` | `screenshot` | `GOLOGIN_TOKEN` | Screenshot path |
| `agent_browser_close` | `close` | `GOLOGIN_TOKEN` | Close status |
| `agent_browser_sessions` | `sessions` | `GOLOGIN_TOKEN` | Session list |
| `agent_browser_current` | `current` | `GOLOGIN_TOKEN` | Current session summary |

## agent_browser_open

```bash
gologin-agent-browser open "https://example.com"
```

Use when:
A new cloud browser session should begin.

## agent_browser_snapshot

```bash
gologin-agent-browser snapshot -i
```

Typical output:

```text
session=s1 url=https://example.com/
- link "More information..." [ref=@e3]
```

Use when:
The next deterministic ref is needed.

## agent_browser_click

```bash
gologin-agent-browser click @e3
```

Use when:
A ref or selector should be clicked.

## agent_browser_type

```bash
gologin-agent-browser type @e2 "hello world"
```

Use when:
Text should be typed character-for-character into a target.

## agent_browser_fill

```bash
gologin-agent-browser fill "input[name='email']" "test@example.com"
```

Use when:
An input should be set directly in one step.

## agent_browser_find

```bash
gologin-agent-browser find label "Email" fill "test@example.com"
gologin-agent-browser find role button click --name "Submit"
```

Use when:
Semantic target resolution is more reliable than refs.

## agent_browser_get

```bash
gologin-agent-browser get title
gologin-agent-browser get text @e4
```

Use when:
The flow should read back text, value, HTML, title, or URL.

## agent_browser_wait

```bash
gologin-agent-browser wait --text "Welcome"
gologin-agent-browser wait 2000
```

Use when:
The flow must pause until state or content changes.

## agent_browser_upload

```bash
gologin-agent-browser upload "input[type='file']" /absolute/path/to/avatar.png
```

Use when:
The page requires file input.

## agent_browser_pdf

```bash
gologin-agent-browser pdf "/tmp/page.pdf"
```

Use when:
A PDF artifact is required.

## agent_browser_screenshot

```bash
gologin-agent-browser screenshot "/tmp/page.png" --annotate
```

Use when:
A screenshot artifact is required.

## agent_browser_close

```bash
gologin-agent-browser close
```

Use when:
The active session should end.

## agent_browser_sessions

```bash
gologin-agent-browser sessions
```

Use when:
All active sessions must be inspected.

## agent_browser_current

```bash
gologin-agent-browser current
```

Use when:
The active session summary is needed before the next step.
