# Bushnell AI Hub

## Purpose and audience

This site teaches Bushnell staff with little or no AI experience how to safely and confidently use the organization's three approved AI tools — Claude, ChatGPT, and Microsoft Copilot. It is written for novices: no technical background is assumed. The guiding path a first-time visitor should follow is: read the safety rules, choose a work goal, select an approved tool, access it correctly, try a safe fictional prompt, review the result critically, revise once, then consult the full Playbook when deeper guidance is needed.

## The two pages

The site is two **independent, self-contained** HTML documents. Each has its own inline `<style>` and `<script>` block and can be opened directly in a browser with no build step. They are not currently split into shared files on purpose — see "Why no shared files yet" below.

- **`index.html`** — "AI 101: Start Here." The entry point and the beginner's guided journey (8 numbered steps), the three-tool card grid, Rules of the Road, a "Try It Safely" fictional-prompt walkthrough, role-based practice tracks, a short glossary, and an FAQ.
- **`ai-playbook.html`** — "The AI Playbook." The deeper reference: an interactive tool-picker wizard, myth-busting FAQ, the full 14-tool ensemble (3 approved + 11 not-yet-approved), the Prompt Library, the official AI policy, a longer glossary, and Staff Voices.

The two pages cross-link (`index.html` → "Open the AI Playbook", `ai-playbook.html` → "← Start Here") but do not share any files today.

## Repository structure

```
index.html                                    # AI 101 — the beginner entry point
ai-playbook.html                              # The AI Playbook — the full reference
.github/workflows/azure-static-web-apps-*.yml  # CI/CD — deploys main to Azure Static Web Apps
.gitignore                                    # Ignores local *.bak files
README.md                                     # This file
CONTRIBUTING.md                               # Pre-publication review checklist
```

There is no build system, package manager, or dependency file in this repository. Both HTML files load Google Fonts from a CDN `<link>` and are otherwise fully self-contained (no external JS libraries).

A local, untracked `Bushnell_AI_Hub_Claude_Handoff.md` may exist on a contributor's machine as a process document for AI-assisted implementation work. It is excluded from the repository (not tracked by git) and must never be committed — it is not part of the site and has no bearing on what gets deployed.

## Local preview

Because there is no build step, open either file directly:

```bash
# Windows
start index.html
start ai-playbook.html
```

Or serve the folder with any static file server (optional, useful for testing relative links exactly as deployed):

```bash
python -m http.server 8000
# then visit http://localhost:8000/index.html
```

## Deployment (evidence-based)

Deployment is handled by `.github/workflows/azure-static-web-apps-zealous-flower-023093b0f.yml`. What the workflow file itself shows:

- It triggers on pushes to `main` and on pull requests targeting `main`.
- It uses `Azure/static-web-apps-deploy@v1`.
- `app_location` is `"/"`.
- `api_location` and `output_location` are both set to `""` (empty).
- There is no repository-defined package manager, build script, or build configuration anywhere in this repo.

That is the extent of what the repository's evidence supports. It does **not** by itself prove that files are uploaded unmodified or that no build behavior occurs inside the Azure action — that is internal to `Azure/static-web-apps-deploy@v1` and this repository does not document it. Don't state or assume more than the bullet points above.

**Practical consequence: pushing only to `dev` does not trigger this workflow** — it only runs on `main` pushes and PRs targeting `main`. The `dev` branch exists specifically so learner-facing changes can be independently reviewed before they ever reach `main`. Nothing in this repository merges to `main` or deploys without explicit human authorization — no automation in this repo does that on its own.

## Where to maintain content

Everything lives inline in the two HTML files; there is currently no shared data source (see below).

| What | Where |
|---|---|
| Approved-tool status, card copy, "Best for" lists, access notes | `index.html`: `const toolData = {...}` (Claude/ChatGPT/Copilot objects). `ai-playbook.html`: `const ensembleToolData = {...}` |
| Tool-picker wizard branches and approval flags (`approved:true/false`) | `ai-playbook.html`: `const wizardStep2Data = {...}` |
| Safety rules ("Rules of the Road") | Both files, `id="rules"` section — currently duplicated by design; keep both copies in sync |
| Access/SSO wording (Claude & ChatGPT via Bushnell SSO; Copilot via Bushnell Microsoft 365 account — never mix these up) | Both files, wherever Claude/ChatGPT/Copilot access is mentioned (tool notes, FAQ, Myths, Rules) |
| Prompt Library templates | `ai-playbook.html`, `<!-- PROMPT LIBRARY -->` section |
| Training-video placeholders ("Training resource coming soon") | `index.html`, "Watch & learn" block — carries an inline `TODO(AI Task Force)` comment; replace only with links the AI Task Force has actually reviewed and approved |
| Staff Voices and its illustrative-example disclaimer | `ai-playbook.html`, `<!-- STAFF VOICES -->` section — the disclaimer directly above the quotes must stay unless every quote and attribution has been individually verified with the named staff member |
| Official AI policy text | `ai-playbook.html`, `<!-- POLICY -->` section |
| Last-reviewed date | A visible "Last reviewed: YYYY-MM-DD" line in the footer of both `index.html` and `ai-playbook.html`, directly below the AI Task Force contact line. Update the date in both files together whenever a content review is completed, and record it in `CONTRIBUTING.md`'s checklist history |

### Why no shared files yet

Prompt 4 of this project's implementation process deliberately did not extract shared CSS/JS or a shared content source — that consolidation is scoped to a later phase. Until then, **any change to safety rules, tool status, or access wording must be made in both files** to keep them consistent. `CONTRIBUTING.md`'s checklist exists specifically to catch drift between the two pages before publication.

## Governance and contact

The **AI Task Force** owns this content and the underlying AI policy. Questions, tool-approval requests, and content corrections go to **ai-taskforce@bushnell.org** (both pages' footers link here). Do not invent a different governing-body name or contact address — "AI Task Force" and this address are the only confirmed values.

## Test-data requirements

Every example, prompt, and screenshot-worthy sample in this site must use **fictional or fully anonymized information** — never a real donor name, gift amount, financial figure, personnel detail, or other confidential Bushnell data. The Prompt Library and "Try It Safely" sections already model this; preserve that pattern in any new content.

## Accessibility expectations

Both pages are built to a working accessibility baseline that any change must preserve:

- Semantic `header`/`nav`/`main`/`footer` landmarks and a visible-on-focus skip link
- All interactive cards are real `<button>`/`<a>` elements (never a clickable `<div>`) with clear accessible names
- Both modals (`index.html`'s tool modal, `ai-playbook.html`'s ensemble modal) implement full dialog semantics: `role="dialog"`, `aria-modal`, `aria-labelledby`, initial focus into the dialog, a Tab/Shift+Tab focus trap (including the dialog's own initial `tabindex="-1"` focus state), Escape-to-close, exact focus restoration to the triggering control, and background isolation (`header`/`main`/`footer`/skip-link all set `inert` while a dialog is open)
- The wizard result and copy-to-clipboard status each use exactly one `aria-live` announcement mechanism — never both a live-updating visible region and a duplicate hidden announcement for the same event
- `:focus-visible` styling, `prefers-reduced-motion` support, and `rel="noopener noreferrer"` on external links
- No responsive layout should reintroduce horizontal overflow; test at approximately 320/375/768/1440 CSS px

See `CONTRIBUTING.md` for the full pre-publication checklist that verifies these.

## Workflow: dev-first, independently validated

This repository uses a `dev`-first workflow for learner-facing changes:

1. Changes are made and committed on `dev`.
2. `dev` is pushed to `origin/dev` for **independent review** before anything is considered accepted.
3. Only after that review confirms the change is correct does it get merged to `main` — and **that merge, and any deployment, requires explicit human authorization.** No process in this repository merges to `main` or deploys on its own.

## Last-reviewed

This maintenance documentation (`README.md` and `CONTRIBUTING.md`) was written and last reviewed **2026-08-06**. This date reflects when this documentation was authored, not a review of the learner-facing content's accuracy — record actual content review dates using the checklist in `CONTRIBUTING.md`.
