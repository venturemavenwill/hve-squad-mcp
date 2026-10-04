---
bump: minor
type: Added
---

- **Advisory runs write a report before review.** When no deliverable fan-out
  replaces it, the advisory pipeline now runs a bounded, text-only report stage
  between Plan and Review. It may read project artifacts and write one Markdown
  report under `.copilot-tracking/changes/`, with no shell, network or
  delegation and a fixed tool-call and time budget, so the reviewer no longer
  fails runs for a missing developer artifact.
- **Copilot research can read full pages through curl or a real browser.** The
  Copilot sandbox image now includes pinned Playwright 1.63.0 and Chromium, exposed
  as `squad-browser`. Researchers are told that `web_fetch` may return only a
  summary, and to fall back to `curl` for static text or to `squad-browser`
  for JavaScript-rendered pages and ordinary click, search-field and scroll
  navigation. Each workflow uses a fresh browser context with bounded actions
  and output; requests are limited to public HTTPS hosts (checked after DNS
  resolution) and the optional `SQUAD_MCP_COPILOT_ALLOWED_HOSTS` list, which
  the sidecar now receives as `COPILOT_BROWSER_ALLOWED_HOSTS`. Sign-in,
  passwords, paywalls and CAPTCHAs are out of scope. Browser results are
  recorded as `browser-reported:` evidence with the visited URLs.
- IPv4-mapped IPv6 addresses written in hex (`::ffff:a00:1`) are now treated
  as non-public by the sandbox network policy.
- Files under `host/sandbox/` are pinned to LF, because a CRLF shebang stops the
  launcher from running in the Linux image.
