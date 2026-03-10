# Ref Loop

Use this workflow for deterministic browser actions.

1. Run `agent_browser_open`.
2. Run `agent_browser_snapshot`.
3. Choose the next ref.
4. Act with `agent_browser_click`, `agent_browser_type`, or `agent_browser_fill`.
5. Refresh the snapshot if the page changes.
