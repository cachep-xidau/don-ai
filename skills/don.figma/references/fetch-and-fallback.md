# Figma Fetch And Fallback

Use this file after scope confirmation and before any fetch attempt.

## Strategy Priority

```text
1. MCP Scoped Fetch
   ↓ if throttled / 429 / ambiguous result
2. Chrome Remote Debug Fallback
```

## MCP Scoped Fetch

Use `figma-console` MCP server with anti-bloat controls:

- Fetch only the target `node-id`, not the parent frame
- Request `get_figma_data` with `nodeId` and `depth=2`
- If result has more than `500 nodes`, narrow scope and re-fetch with a child node
- If result returns `throttled` or `429`, move to Chrome fallback
- If result shape is ambiguous, wrong-screen, or missing visible text expected by the user, classify as `scope_mismatch` and narrow before retrying

## Chrome Remote Debug Fallback

Use fallback when MCP fails, is ambiguous, or appears gated.

```text
Launch ONCE:
  node connect-chrome.js --launch --port 9222

ALL subsequent calls reconnect via:
  --browser-url http://localhost:9222

Pass browserUrl into getBrowser in:
  screenshot.js | evaluate.js | aria-snapshot.js
```

### Execution Flow

1. Open the exact Figma URL with `?node-id={node-id}`
2. Wait for stabilization, around `12` seconds
3. Validate `accessState` via evaluate text:
   - Must confirm `gated=false`
   - Must not contain login gate text such as `Sign in` or `Log in to view`
4. If screenshot still shows spinner, prioritize `evaluate` result and retry screenshot after stabilization
5. Capture text via `aria-snapshot`
6. Capture layout via screenshot
7. If the loaded frame does not match the requested screen/component, stop and report `scope_mismatch`

## Error Classification

Always classify before retrying.

- `browser_lifecycle`
  - Chrome closed or crashed
  - Relaunch browser and reconnect

- `permission_gate`
  - Login wall detected
  - Need credentials or authorized session

- `render_timing`
  - Spinner still active
  - Wait longer and retry

- `scope_mismatch`
  - Wrong frame or component loaded
  - Need narrower or corrected `node-id`

## Non-Negotiable Rules

- Do not fetch the whole file if the user asked for one screen/component
- Do not trust the data until `gated=false` is confirmed
- Do not paraphrase visible labels during extraction
- Do not continue to downstream artifact drafting if the fetch is `BLOCKED`

## Downstream Routing

After a successful fetch:

- route to `don.artifact` when the user wants to draft Screen Description, User Story, or SRS from the extracted screen context
- route to `don.analysis` when the user wants analysis notes about process, data, or integration implications instead of a design artifact

If fetch is partial, blocked, or mismatched, stop and report the failure class before any downstream handoff.
