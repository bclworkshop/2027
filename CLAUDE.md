# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository purpose

Static single-page website for the annual **Bellairs Workshop** held at the Bellairs Research Institute (McGill) in Barbados. The 2027 edition is **"Bellairs Workshop on World Models, Causality, and Agents"** (Feb 26 – Mar 5, 2027). Each year gets its own GitHub Pages site under the `bclworkshop` org; this repo's remote is `github.com/bclworkshop/2027` → https://bclworkshop.github.io/2027/.

The current content was rolled forward from the 2025 site (then themed "Causality in the Era of Foundation Models"). The participant list and most of the logistics copy carry over year-to-year; the abstract, topics, dates, program, and jumbotron title/ordinal change each year. The program section currently shows only a "Detailed schedule TBA." placeholder — the per-day card grid (sun/moon-stars SVG icons, see git history) is the template to follow when filling it in.

## No build system

There is no package manager, bundler, linter, or test suite. The site is plain HTML served as-is by GitHub Pages.

- **Preview locally:** open `index.html` directly in a browser, or run `python3 -m http.server` from the repo root and visit http://localhost:8000.
- **Deploy:** `git push origin main` — GitHub Pages serves `main`.
- Bootstrap 4 and jQuery are loaded from CDN; do not vendor them.

## File layout

- `index.html` — the entire site. ~1300 lines, contains all CSS (inline `<style>`), markup, and the program/participant/logistics content. Edits to the site happen here.
- `previous.html` — small standalone index linking to past workshop sites (2022/2023/2024). Update when adding a new edition.
- `people/` — participant headshots (`{firstname}.{jpg,png,jpeg,webp}`). Referenced by `<img src="people/{name}.jpg">` in `index.html`. When adding a participant, add the image here and the `<li>` block in the Participants section.
- `img/` — site chrome (banner, favicon, map, hero backgrounds like `purple_beach.jpg`).
- `documents/logisticsfaq.pdf` — participant-facing FAQ linked from the page.
- `README.md` — currently just a redirect notice for an email mistake; not authoritative.

## index.html structure

The page is organized as anchor-linked sections registered in the top navbar (around `#navbarCollapse`). Each section is wrapped in `<div class="my-3 p-3 bg-white rounded box-shadow">` with an `<h5 class="... anchoritem" id="...">` heading. Section IDs (in order): `abstract`, `attendees`, `goals`, `program`, `logistics`. To add/rename a section, update both the navbar `<ul class="navbar-nav">` and the section's `id`.

### Repeating patterns (keep them consistent)

- **Participant card** (`#attendees` section): one `<li>` per person with a personal-site `<a target="_blank">`, a circular `<img src="people/...">` (width/height 150), the name in `<b>`, and an affiliation line like `<br />(Institution)`. The `*` suffix on a name marks an organizer. Adding a participant = add image to `people/` + insert `<li>` block in alphabetical-ish order.
- **Program day** (`#program` section): a two-column Bootstrap row with morning (sun SVG) and evening (moon-stars SVG) cards. Each day is a `<div class="col-md-6">` containing a `<div class="media">` with a fixed inline SVG icon and a `media-body` listing talks as `<p>Title</p>` + `<p><span class="font-italic">Speaker</span></p>`. The SVG paths are duplicated verbatim across every day — when adding/reorganizing days, copy an existing block and edit only the heading and the talk list. The current file replaces this grid with a "Detailed schedule TBA." placeholder; the previous edition's grid is in git history (see commit `6c605fe` or earlier).
- **Logistics item**: `<div class="media text-muted pt-3">` with a `holder.js` placeholder `<img>`, then `<p class="media-body ...">` containing `<strong class="d-block text-gray-dark">Topic</strong>` and the body text. The `holder.js` reference is decorative — leave it.

## Year-over-year migration checklist

When rolling this site forward to a new edition, the changes are almost entirely textual edits inside `index.html`:

1. Jumbotron heading (`Welcome to the Fifth` ordinal + dates around line ~200–216) — bump the ordinal each year.
2. `<meta name="description">` and `<title>`.
3. Abstract paragraph and topics list.
4. The "This is a sequel to..." line linking previous editions (also add the just-ended edition to `previous.html`).
5. Participants section: replace `<li>` blocks; swap matching images in `people/`.
6. Program section: rewrite each day's talks.
7. Logistics: update venue dates/meal arrangements as needed.
8. Google Analytics `gtag` ID (`G-4QXV9B2MS6`) — confirm with the organizer whether to keep or rotate.
9. Rename the navbar brand (`BCL 2027`) to the new year.
10. Update `README.md` if the redirect URL changes.

## Contact

Organizers listed in the page footer: Alexandre Drouin (alexandre.drouin@servicenow.com) and Perouz Taslakian. Defer to them on content changes.
