---
bump: patch
type: Fixed
---

- **The sandbox browser now works for the agent.** The Copilot runtime starts the
  agent's shell from an allowlisted environment that drops
  `PLAYWRIGHT_BROWSERS_PATH`, so `squad-browser` could not find Chromium; the
  launcher now sets it. A workflow without `steps` no longer crashes.
- **Lazily rendered page content is read.** After its actions, `squad-browser`
  scrolls through the page and extracts visible text including open shadow roots,
  so web components such as MDN's compatibility tables are captured. Output is now
  one short `HVE_BROWSER_RESULT` metadata line followed by plain page text (up to
  30,000 characters) and links, so the server can record the visited pages even
  when long output is truncated. Researchers are told to read the live page with
  the browser when `web_fetch` returns only an app shell, and not to redirect or
  pipe browser output; a redirected run is recorded as
  `browser-output-redirected:` so reviewers know its receipt has no page text.
- **The report stage has room to finish.** Its limits rise to 10 model calls and
  12 tool calls (agentic runtimes spend one model call per tool round trip), and
  a budget failure now names the limit that applied.
- **A declining backlog handoff no longer fails a reviewed run.** When the
  optional backlog-handoff agent stops because the request has nothing to plan
  (for example a research question), the run completes and records the stage as
  skipped. Runtime failures and limits in that stage still halt the run.
