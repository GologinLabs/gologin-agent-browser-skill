# Quick Session

Goal:
Open a browser session, capture a snapshot, click a ref, and close the session.

```bash
export GOLOGIN_TOKEN="your_gologin_token"

gologin-agent-browser open https://example.com
gologin-agent-browser snapshot -i
gologin-agent-browser click @e3
gologin-agent-browser close
```
