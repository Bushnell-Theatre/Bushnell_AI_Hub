# Contributing / Pre-Publication Checklist

`index.html` and `ai-playbook.html` are independent, self-contained documents — nothing is shared between them yet. That means most items below must be checked **in both files**, not just one. See `README.md` for where each kind of content lives.

Work happens on `dev` first. Nothing merges to `main` or deploys without explicit human authorization — this checklist is what should be satisfied before asking for that authorization.

## Before you publish, confirm:

### Consistency between the two pages
- [ ] Rules of the Road (Do's and Don'ts) match, word for word, in both files
- [ ] Tool access/note wording matches between `index.html`'s `toolData` and `ai-playbook.html`'s `ensembleToolData` for Claude, ChatGPT, and Copilot
- [ ] Any change made in one file's Rules/FAQ/Myths/access wording has been mirrored in the other

### Approved-tool status
- [ ] Only Claude, ChatGPT, and Microsoft Copilot are ever presented as authorized/approved
- [ ] Every other tool (in `ai-playbook.html`'s "Also worth knowing" list and the wizard's `wizardStep2Data`) is clearly marked as requiring AI Task Force approval before use — never shown as already authorized
- [ ] The wizard's `approved:true/false` flag on every option matches this list

### SSO / access wording
- [ ] Claude and ChatGPT access wording says **Bushnell SSO** through a Bushnell-managed workspace — never a personal or public account
- [ ] Copilot access wording says it is tied to the user's **Bushnell Microsoft 365 account** — never expand the Bushnell SSO phrasing to Copilot; that is a different, unconfirmed policy
- [ ] No sentence generalizes "sign in with Bushnell SSO" across all three tools when Copilot is included in that sentence

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
