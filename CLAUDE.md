# BMIS 235 HTML Module: context for Claude

Read this first in any new session. It holds the decisions, conventions and open work for
Professor John Correia's HTML module (Gonzaga, BMIS 235, business students, no prior coding).

## What this is

- **Live site:** https://gu-27.github.io/html-module/ (GitHub Pages from `main`, `.nojekyll`).
- **This repo (`gu-27/html-module`):** the instructions site and class slide decks.
- **Starter template repos** (students click "Use this template"): `gu-27/bmis235-html-1`,
  `gu-27/bmis235-html-2`, `gu-27/bmis235-html-3` (all public, all template repos).
  HTML-4 has **no** template repo: students copy their own HTML-3 repo.
- `gu-27/bmis235-html-starter` and `gu-27/HTML-test` are older and unused.

## Files

| File | What it is |
|---|---|
| `index.html` | Module home: links to each assignment and each deck |
| `html-1.html` … `html-4.html` | Student instructions, one page per assignment |
| `html-4-blocks.html` | Block library for HTML-4 Path 1 (banner, cards, gallery, table, FAQ, contact), each with an iframe preview and copy buttons; all classes prefixed `blk-` |
| `style.css` | Shared styles for the instructions pages (`.block`, `.why`, `.callout`, `.callout.warn`, `.rubric`, `.btn`, `.pill`) |
| `slides/intro.html`, `slides/html-1..4.html` | Class decks, one self-contained HTML file each |
| `img/` | Before/after screenshots per assignment, `sample-1..3.jpg` placeholders for the block library |

## The four assignments (as built)

1. **HTML-1 · Styling:** Hello World page, publish live, text/colors/fonts.
2. **HTML-2 · Embedding:** "Mind, Body, Craft" podcast page; fix broken images/links/videos, dark-mode button, one business embed.
3. **HTML-3 · Links + CSS:** four-page template (`index`, `page1-3`), `page3` intentionally missing the stylesheet link.
   Students: plan on paper, make menu-button images in Excel (same cell size, centered text, gridlines off, zoom 100%,
   screenshot corner to corner, name after the page), rename pages (e.g. `susie.html`), fix the menu on `index.html`
   first then copy it to every page, `styles.css` as "your brand" (3 styles, one commit each), one outside + one
   mailto link. **Part 7:** paste an AI-built interactive graphic into the empty `<div class="showcase">` on the home
   page using a provided prompt (one block, vanilla JS, every CSS rule prefixed `.showcase`). 10 pts.
4. **HTML-4 · Final, "Your Site, Your Path":** copy the HTML-3 site into a new `bmis235-html-4` repo via
   github.com/new/import, then pick a path:
   - **Path 1 By hand:** 3 blocks from the block library, 4+ pages, 3 new styles.
   - **Path 2 Mix:** 2+ AI pieces (Copilot / Claude / ChatGPT), own-words comment above each.
   - **Path 3 Full build:** Claude Code + GitHub + Cloudflare; must build a *learning tool* that teaches an
     HTML-1–3 concept, built for how the student learns, tested by a Path 1 classmate.
   - Everyone: README with path + "by hand vs by AI". Everyone 3 pts + path 7 pts.
   - Import-error help: Fix 1 (use the real repo address `github.com/user/repo`, not the `github.io` live link;
     replace the capital-letter placeholders), Fix 2 (Download ZIP → upload into a new repo). A failed import leaves a
     broken `bmis235-html-4` that must be deleted first.
   - **John removed the "make HTML-3 a template" fix on purpose: he considers it a cheat. Don't add it back.**

## HTML-4 deck (33 slides) flow

Concepts first, then how sites get built, then the paths:
title → what you know now → what is a website (communicate vs give a tool) → four layers (HTML, GitHub,
JavaScript, Cloudflare; "same code, where it's stored and runs changes") → HTML built-in → what is a repo →
a commit up close → GitHub Pages files in/site out → JavaScript runs on your computer → why JS not Python →
three places data lives (cache / local storage / database) → Cloudflare is everywhere → inside Cloudflare
(front door / building / storage room) → files vs code hosting → click Save: browser ↔ Worker ↔ database →
why Cloudflare → so what can a website do → who's typing → Claude proposes, you approve (branch → PR → main) →
you're in the middle (chat ↔ you ↔ Claude Code → repo → Cloudflare) → the whole loop → three paths → path
slides → README → get started → import error: two fixes → grading → troubleshooting → close.

## John's preferences (apply to everything)

- Students should **read and think**: text steps plus a short gray "What's happening" note (`p.why`) under each
  step. Not graphic-heavy walkthroughs. Make them search for small things themselves (e.g. how to screenshot).
- Hard way first, AI only at the end of each stage. Growth mindset: errors are information.
- Decks: professional, bold large type, big simple blocks, very little text per slide, content fills the frame
  (no big empty space at the bottom). Not dark gray-and-red. Concepts before mechanics.
- Keep replies to John short. He reviews decks in the panel before they go live (see workflow).

## Workflow and gotchas

- **Review flow for decks:** edit, send the file to the panel with `SendUserFile` (display: render), iterate, and only
  merge to `main` when John says push/merge. Use a branch (e.g. `html4-deck-review`) for drafts; Pages only
  publishes `main`. Small student-facing instruction fixes have been pushed straight to `main` when urgent.
- **Check every page with Playwright** before pushing: `chromium.launch(executable_path="/usr/bin/google-chrome")`,
  1600×900 for decks; check for slide overflow with
  `[...document.querySelectorAll('.slide')].map(s => s.scrollHeight > s.clientHeight + 2)` (toggle `.on` first).
- **Deck internals:** slides are `<section class="slide" data-sec="...">`; `data-step` reveals items; `show(i,'end')`
  jumps; diagrams use the in-file `render({w,h,nodes,edges},id)` SVG helper (edge `both:true` = two-way arrow) plus
  `row()` (4 nodes) and `five()` helpers. Insert new CSS **just before `</style>`**: inserting before a selector
  string like `.layers {` once landed inside another rule and broke the layout.
- **Verify deploys** with `gh run list -R gu-27/html-module -L 1` (wait for the HEAD sha to show `completed success`).
  The container cannot fetch `*.github.io` directly. GitHub GraphQL is blocked here; use `gh api` REST.
- Repo visibility changes can't be done via API from here; they need John in the browser (GitHub asks him to verify).

## Open request (not started), from John on 2026-11-19

1. **Restructure HTML-4 paths:** state the choice right at the top; students click a path and see **only that path's
   instructions** (tabs or similar). John said the paths should be "one or two". **Still undecided:** which two.
   Options offered: (a) By hand vs With AI (merge Mix + Full build), (b) By hand vs Full build (drop Mix),
   (c) keep all three as tabs, (d) Mix vs Full build. Ask John before building; update the deck's path slides,
   grading slide and rubric to match.
2. **Make every instructions page easier to read:** short chunks a student can finish one at a time; the extra help
   ("Stuck?", troubleshooting, detailed sub-steps, import errors) collapsed behind click-to-expand (`<details>`), so the
   default view is short. Students already find the pages hard to get through.
3. **Audit all four instructions pages** (`html-1` to `html-4`, plus `html-4-blocks`) and apply the same pattern
   consistently. Keep the `p.why` notes (maybe collapsible), the rubric tables and the before/after images.
