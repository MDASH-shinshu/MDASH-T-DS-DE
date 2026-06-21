---
name: shinshu-mdash-design
description: Use this skill to generate well-branded interfaces and assets for 信州大学 MDASH (Shinshu University's 数理・データサイエンス・AI教育プログラム) — course slides, lecture decks, the course portal, handouts, and Jupyter-notebook-style teaching materials, for production or throwaway prototypes/mocks. Contains essential design guidelines, colors, type, fonts, academic content components, slide layouts, and the course-portal UI kit.
user-invocable: true
---

Read the `README.md` file within this skill first — it holds the brand context, sources,
CONTENT FUNDAMENTALS, VISUAL FOUNDATIONS, and ICONOGRAPHY guidance. Then explore the other files:

- `styles.css` + `tokens/` + `fonts/` — link `styles.css` and design with the CSS variables
  (prefer semantic aliases: `--brand`, `--text-primary`, `--surface-card`, `--border-default`).
- `components/` — React primitives (`Button`, `Badge`, `Card`, `CalloutBox`, `KeywordChip`,
  `FigureFrame`, `CodeCell`); read each `*.prompt.md` for usage.
- `slides/` — six ready 1280×720 lecture-slide layouts (cover, section, objectives, content+figure,
  code, references) sharing `slide-base.css`.
- `ui_kits/course-portal/` — the MDASH course catalogue site recreation.
- `templates/course-slide/` — a copy-to-start branded lecture slide.
- `1-1_data_science_EN.html` — **reference implementation**: a full 24-slide English lecture
  deck (DS section 1-1) built on the system. Use it as the proven "型" (pattern) when localizing
  or building any new course deck — see the workflow below.

## Workflow — localizing / building a course deck (the "型")

Follow the pattern proven in `1-1_data_science_EN.html`:

1. **Get the source.** Read the original course material — a Drive PDF/PPTX (Google Drive MCP:
   `googledrive__search_files` → `download_file_content`), a GitHub repo deck, or the
   `mdash-shinshu.github.io` HTML/PDF. Prefer text-layer PDF/PPTX over screenshots.
2. **Extract structure.** Pull the slide/section order, headings, body copy, figure captions,
   and source credits. Translate to the target language in an academic-neutral register
   (explain, don't sell; no "I"; keep technical terms in English).
3. **Lay out with the system.** Build one 1280×720 `<section>` per slide inside a
   `deck-stage` (copy `english-deck/deck-stage.js` + `image-slot.js`). Reuse the slide chrome
   in `1-1_data_science_EN.html` / `slides/slide-base.css`: cover, section divider,
   objectives+keywords, content+figure, code cell, references. Link `styles.css` for tokens;
   put the logo (`assets/shinshu-vi-logo*.png`) in cover + footers.
4. **Decide figure vs. photo per slide.** If a concept is better shown as a diagram (process
   flow, taxonomy, cyber-physical loop), build it from tokens (see slides 6/7/8/11/12/19/22).
   If a real-world scene helps (factory, city, server room, people), drop an `<image-slot>` and
   fill it with a **free** photo.
5. **Source photos safely (CC0 / Unsplash License only).** Search Unsplash, then **fetch the
   listing page** (e.g. `unsplash.com/s/photos/<theme>`) — the fetched HTML exposes each photo's
   real `images.unsplash.com/photo-…` URL and flags premium ones (`plus.unsplash.com` /
   "For Unsplash+" / lock = NOT free, skip). Pick a `images.unsplash.com` URL, use it as the
   slot `src` at `?w=1600&q=60&auto=format&fit=crop`. People themes skew premium — prefer
   "Centre for Ageing Better" (age-positive, free) and named free photographers.
6. **Record every image** in a `*-IMAGE-CREDITS.md` (slide · subject · license · author · URL).
7. **Ship self-contained.** Add a `<template id="__bundler_thumbnail">` then run the inliner to
   produce a `*.standalone.html` that works offline; for PDF, open and print to PDF.

If creating visual artifacts (slides, mocks, throwaway prototypes), copy the assets and CSS you
need out and produce static HTML files for the user to view. If working on production code, copy
assets and apply the rules here to design as an expert in this brand.

Key brand rules to honor: Japanese-first academic register (explain, don't sell; no "I"; no emoji);
the 《学修項目》/《キーワード》/《参考文献》 section vocabulary; Shinshu school-color deep green
(`#006f48`) as primary with mid (`#008e4c`) and bright-emerald (`#00a050`) accents; clean white paper, hairline borders,
modest radii, restrained motion; ☆/※ glyphs and 《》 brackets are the only native "icons".

> The official Shinshu VI symbol mark is bundled as a transparent PNG `assets/shinshu-vi-logo.png`
> (plus `assets/shinshu-vi-logo-white.png`, a white knockout for dark/brand-green backgrounds).
> Use it directly in slides and screens — no blend-mode tricks needed. Brand greens are sampled
> from it: bright `#00a050`, mid `#008e4c`, deep/school `#006f48`. Ask the user for the horizontal
> logotype lockup if the design needs the wordmark. The horizontal logotype (mark + SHINSHU
> UNIVERSITY) is bundled as `assets/shinshu-vi-logotype.png` (+ `-white.png`) — prefer it on slide
> covers and title screens.

If invoked without other guidance, ask what the user wants to build, ask a few focused questions,
then act as an expert designer who outputs HTML artifacts or production code as the need dictates.
