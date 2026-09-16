# Contributing / Pre-Publication Checklist

`index.html` and `ai-playbook.html` are independent, self-contained documents — nothing is shared between them yet. That means most items below must be checked **in both files**, not just one. See `README.md` for where each kind of content lives.

Work happens on `dev` first. Nothing merges to `main` or deploys without explicit human authorization — this checklist is what should be satisfied before asking for that authorization.

## Before you publish, confirm:

### Organizational branding (Bushnell / Warner Theatre / HSO)
- [ ] The primary wordmark — "The Bushnell | Warner Theatre | Hartford Symphony Orchestra" over "AI Hub" — matches exactly in both files' `<header>` blocks and is reflected in both `<title>` tags
- [ ] Warner Theatre and Hartford Symphony Orchestra (HSO) are never described as having identical corporate relationships to The Bushnell: Warner is a Bushnell subsidiary; HSO is an independent organization receiving shared services from The Bushnell, never a Bushnell department or subsidiary
- [ ] No HSO-specific account-migration language, transitional account instructions, or personal/public-account approval has been added
- [ ] No HSO (or Warner) authentication, licensing, or tenant details have been invented — the managed-account wording (see "SSO / access wording" below) is deliberately organization-neutral where it needs to be, and stays as-is otherwise unless a confirmed access decision says otherwise
- [ ] Audience/introductory language (hero copy, journey intro, footers) includes all three organizations; approval-status and policy-ownership wording (e.g. "Approved for Bushnell use," "The Bushnell's AI Policy") is left untouched unless a governance decision confirms it should change

### Consistency between the two pages
- [ ] Rules of the Road (Do's and Don'ts) match, word for word, in both files
- [ ] Tool access/note wording matches between `index.html`'s `toolData` and `ai-playbook.html`'s `ensembleToolData` for Claude, ChatGPT, and Copilot
- [ ] Any change made in one file's Rules/FAQ/Myths/access wording has been mirrored in the other

### Approved-tool status
Three states exist, per the AI Approved Tools Addendum — never collapse this to a binary approved/not-approved:
- **Approved** (Claude, ChatGPT, Copilot as the main toolkit/ensemble; Asana in "Also worth knowing") — presented as authorized, no restrictions shown
- **Conditionally Approved** (Canva AI, Beautiful.ai, Suno.ai — all in "Also worth knowing") — labeled "Conditionally Approved" (never plain "Approved," never "Not Approved"), with its condition visible: paid/licensed tier only, public/non-sensitive work only, no non-public organizational information
- **Not Approved** (every other tool in the "Also worth knowing" list) — labeled "Not Approved," requires AI Task Force approval before use

**The "Cast the Right Tool" wizard never recommends a Not Approved tool.** Every `wizardStep2Data` answer path must resolve to Approved, Conditionally Approved, or — if no approved/conditionally-approved tool genuinely fits — a result that names the *closest approved tool* with an honest caveat about the capability gap (never an unapproved tool's name, and never overclaiming a capability the recommended tool doesn't have). `wizardShowResult()` also supports a `noTool:true` state (badge: "No Approved Tool Identified") for cases where recommending any approved tool would be misleading — currently unused in the live data but kept available.

Checklist:
- [ ] Claude, ChatGPT, and Microsoft Copilot remain the only tools in the main Toolkit/Ensemble grid, presented as fully authorized/approved
- [ ] Asana is labeled "Approved" in the "Also worth knowing" list
- [ ] Canva AI, Beautiful.ai, and Suno.ai are labeled "Conditionally Approved" everywhere they appear, with the paid/licensed-tier and non-sensitive-data condition visible alongside the label — not just "approved," and not "not approved"
- [ ] Every other tool in the "Also worth knowing" list is clearly marked "Not Approved" / requiring AI Task Force approval — never shown as already authorized
- [ ] No wizard answer path recommends a tool outside the Approved/Conditionally Approved list — check every option in every `wizardStep2Data` category, not just the ones that changed most recently
- [ ] The wizard's `approved:true/false` flag matches this list; `conditional:true` is set only where the Addendum specifies Conditionally Approved (currently Canva AI); `wizardShowResult()`'s badge logic (approved / conditional / no-tool / not-approved) is not reduced back to a binary
- [ ] Adding any further tool from the Addendum (e.g. the backend security/IT/HR/finance systems) requires the same explicit authorization Asana and Suno.ai received — it is not done by default just because a tool appears in the full Addendum

### Managed-account access wording
- [ ] Claude and ChatGPT access wording says: **"Use only the Bushnell-managed workspace account provided to you — never a personal or public account."** (not "Bushnell SSO" — that term was retired)
- [ ] Copilot access wording says: **"Use only your organization-issued Microsoft 365 account."** — deliberately organization-neutral; never expand the Claude/ChatGPT "Bushnell-managed workspace" phrasing to Copilot
- [ ] No sentence merges the Claude/ChatGPT and Copilot wording into one undifferentiated access instruction
- [ ] The general-access note — "Access instructions may vary by organization. Contact the AI Task Force if you have not yet received an approved managed account." — is present once on each page (Toolkit intro on `index.html`, Ensemble intro on `ai-playbook.html`) and does not imply every HSO or Warner employee already has a managed account

### Sensitive data
- [ ] No real donor name, gift amount, financial figure, personnel detail, or other confidential Bushnell information appears anywhere in the site, including in examples
- [ ] Every prompt template's bracketed field that could pull in sensitive data (donor name, amount, pasted meeting notes, pasted financial data, etc.) still carries its "fictional placeholder only" / "remove real data first" instruction

### Governance
- [ ] The governing body is named **AI Task Force** everywhere (never "AI Committee" or any other name)
- [ ] The contact address is **ai-taskforce@bushnell.org** in both footers and anywhere else it's referenced

### Fictional / anonymized examples
- [ ] Every example prompt, sample name, and walkthrough (including "Try It Safely") uses clearly fictional or fully anonymized information, explicitly labeled as such where a reader could otherwise mistake it for a real instruction to use real data

### Training links and Staff Voices
- [ ] "Watch & Learn" in `index.html` (inside `id="paths"`) links only to each vendor's own official training catalog (Anthropic Academy, OpenAI Academy, Microsoft Learn/Support) for Claude, ChatGPT, and Copilot — not third-party creators or dated YouTube searches. This is allowed without separate AI Task Force review since it's the vendor's own training, not an outside curator's video
- [ ] Each link's title, approximate duration, and "(free sign-in required)" note (where applicable) still match the live vendor page — vendors reorganize and rename these periodically, so recheck before publishing
- [ ] If a link is ever replaced with a genuinely third-party (non-vendor) training video, it must be reviewed and approved by the AI Task Force first
- [ ] Staff Voices quotes in `ai-playbook.html` are not claimed as verified unless each quote and attribution has actually been confirmed with the named staff member — otherwise the "Illustrative examples... not verified quotes" disclaimer must remain directly above them

### Accessibility and responsive behavior
- [ ] All internal links (`#rules`, `#toolkit`, `#paths`, `#try-it`, `#playbook-cta`, etc.) and cross-page links resolve correctly
- [ ] Every interactive element (tool cards, wizard buttons, copy buttons, modal controls) is operable by keyboard alone — Tab, Shift+Tab, Enter, Space, Escape
- [ ] Both dialogs (tool modal in `index.html`, ensemble modal in `ai-playbook.html`) still: open with focus moved in, trap Tab/Shift+Tab (including from the dialog's initial focus state), close on Escape, restore focus to the exact trigger, and isolate `header`/`main`/`footer`/the skip link via `inert` while open
- [ ] The wizard result and the copy-to-clipboard status each produce exactly one screen-reader announcement — not zero, not two
- [ ] Text and interface-state contrast (including gray text, gold/claude and green/chatgpt tool colors, warning/disclaimer red text, and focus indicators) still meets WCAG AA
- [ ] No horizontal overflow at approximately 320, 375, 768, and 1440 CSS px
- [ ] Browser console is free of errors on load and through primary interactions (opening/closing both dialogs, running the wizard, copying a prompt)
- [ ] Core content (safety rules, tool info, policy text, prompts) is still present and readable if JavaScript fails to run — don't move essential text into a JS-only code path

### Review metadata
- [ ] The content actually reviewed is recorded with a last-reviewed date (see `README.md`'s Last-reviewed section for the convention)
- [ ] A content owner (currently the AI Task Force) has approved the specific change before it's asked to move toward `main`

### Publication
- [ ] Changes are committed and pushed to `origin/dev` first
- [ ] Independent review of `dev` has happened before any request to merge to `main`
- [ ] No merge to `main` and no deployment happens without explicit human authorization — this repository's CI only deploys on push to `main`, so `dev` alone is always safe to iterate on
