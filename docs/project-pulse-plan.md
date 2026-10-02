# Project Pulse implementation plan

## Goal

Build a lightweight static dashboard that lets Mona's contributors scan project names, owners, status, recent activity, priority/risk, and a short contributor-friendly summary. Follow `.github/project-pulse-brief.md`; keep the app dependency-free and use project data from JSON.

## Responsibilities and file assignments

- **Designer:** Define the card layout, information hierarchy, status/priority treatments, responsive behavior, and accessible color/contrast and focus choices. Share a concise design direction with Coder before styling; do not own implementation files unless explicitly reassigned.
- **Coder:** Implement the dashboard and preview configuration, following the Designer's direction and keeping to the files below.
  - `app/index.html` — semantic page structure, exact “Project Pulse” title, stylesheet and JSON references, and rendering of visible `.project-card` elements with each project's owner, status, recent activity, priority, and summary.
  - `app/styles.css` — polished, responsive card-based UI; include `.dashboard` and `.project-card` hooks, readable spacing and typography, status badges, rounded corners, and subtle shadows. Preserve contrast and keyboard-visible focus.
  - `app/project-data.json` — strict JSON with a top-level `projects` array. Include multiple representative projects; each has `name`, `owner`, `status`, `recentActivity`, `priority`, and a short contributor-friendly `summary`.
  - `.vscode/launch.json` — strict JSON configuration named **Run Project Pulse Dashboard**. Run `python3 -m http.server 5500` with `cwd` set to `${workspaceFolder}/app`; use `serverReadyAction` to open `http://localhost:%s/index.html`, not the server directory root.

## Order, dependencies, and parallel work

1. Coder confirms the data fields and page contract from the brief. Designer can develop the visual direction in parallel with this schema/page-contract setup because the brief fixes the required content fields.
2. Designer hands off layout, responsive, accessibility, and visual decisions. Coder can prepare the JSON and launch configuration in parallel with design; neither depends on the final CSS.
3. Coder implements HTML and CSS against the agreed project-card structure and data fields. HTML rendering depends on the JSON schema; CSS hooks and layout should align with the Designer handoff.
4. Coder integrates all four assigned files, checks references and launch behavior, then reports validation and any remaining assumptions to the Orchestrator.

Do not split HTML and CSS into independent implementation streams: their classes and content layout must agree. The data and launch setup are safe parallel work; integrate and validate the complete set together.

## Validation and handoff

- Confirm all four assigned files exist; `index.html` references `styles.css` and `project-data.json`, and renders project cards with the required fields.
- Parse `app/project-data.json` and `.vscode/launch.json` as JSON. Check the top-level `projects` array and required per-project fields, including `summary`.
- Check `.dashboard`, `.project-card`, `border-radius`, and `box-shadow` styling hooks, plus responsive layout and accessible contrast/focus behavior.
- Run the repository's relevant exercise checks (including the Step 3 workflow expectations where available).
- In VS Code, launch **Run Project Pulse Dashboard** and verify the browser opens `index.html` and displays the dashboard rather than a directory listing; stop the preview server afterward.
- Report files changed, checks run, and any limitations to the Orchestrator. Do not stage, commit, or push as part of implementation.

## Assumptions and open questions

- The brief does not prescribe project names, owners, or statuses; use clearly fictional, representative sample records unless Mona supplies real data.
- A `summary` field is not in the minimum schema but is requested by the brief's contributor-friendly-summary goal, so include and render it.
- Use the brief's Python static-server launch approach and port `5500`; confirm the environment has Python 3 and that the port is available when previewing.
- No existing app files or project-specific visual brand system are present in the repository; the Designer should choose a clear, accessible neutral visual direction.
