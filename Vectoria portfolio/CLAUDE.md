# Vectoria portfolio — project notes

## Owner
- Designer / brand name: **Victoria Molina de Castro**
- LinkedIn: https://www.linkedin.com/in/mvmdc/

## Pages
- `Home.html` · `Work.html` · `About.html` · `Aventura.html` (case study) · `Kibit.html` (case study)
- Nav order on every page: **Home · Work · About · Linkedin** (active item bold, white pill)

## Design system (locked)
- BG #FFFFFF · text #333333 · text-2 #808080 · border #B3B3B3 · surface #F2F2F2
- Accent red #FF0534 · footer band #333333 white text
- Headings: **Defante** (`fonts/Defante.ttf?v=2`) · body/UI: **Lato**
- Shared tokens: `--page-max:1100–1120px`, `--gutter` fluid clamp, rounded corners, pill buttons/tags
- No drop shadows on elements (user removed them); flat, editorial, generous whitespace

## ⚠️ IMAGES — DO NOT MAKE THE USER RE-UPLOAD
The user drags & drops their own images into `<image-slot>` elements. These persist in
`.image-slots.state.json`, keyed by each slot's `id`. To preserve dropped images across edits:

1. **NEVER change an `<image-slot>`'s `id`.** Keep ids stable when editing/rewriting a page.
2. **NEVER delete or shrink `.image-slots.state.json`.**
3. When restructuring a section, keep the same slot `id`s so the saved image stays attached.
4. Prefer `str_replace_edit` over full `write_file` rewrites on pages with slots, to avoid
   accidentally dropping/renaming slots.
5. Some images are embedded directly as `<img src="assets/…">` (e.g. Home featured cover
   `assets/gamified-portada.png`, About portrait `assets/profile.png`, and ALL Aventura
   case-study images: `assets/av-hero.webp`, `av-showcase.webp`, `av-flows.webp`,
   `av-wires.webp`). Don't remove those files.

### ⚠️ Sidecar size limit
The `.image-slots.state.json` sidecar is ~1.4MB (13 images) and near the host writeFile cap.
Do NOT add more big images to it — new drops can silently fail to persist. For any further
final imagery, extract the data URL and save it as a real file in `assets/`, then reference
it via `<img src>` (that's how the Aventura case-study images were fixed).

### Image handling going forward
Whenever the user drops/loads an image into any template's image-slot, convert it to a
permanent file: extract the data URL, resize to a sane max width (~1600–1800px for
showcases/hero, ~1200px for portraits/assets) and re-encode as webp at ~0.8–0.85 quality
via canvas.convertToBlob before saveFile — don't just dump the raw drop. Keep it as a
reemplazable image-slot with `src="assets/<id>.webp"` pointing at the optimized file.

### Current slot ids (keep stable)
- Home: `proj-mini-left` (Reshaping Kibit), `proj-mini-right` (Humanizing Digital Dating)
- Work: `work-1`…`work-7` (work-7 = Kibit product case study, links to `Kibit.html`)
- About: `about-patagonia`, `about-work`, `about-outdoors`, `about-photography`, `about-boardgames`
- Aventura: now embedded as `assets/av-*.webp` files (no longer slots)

## Case study template
`_Case-Study-Template.html` is the reusable template (forked from Aventura). To make a new
project page: duplicate it, rename (e.g. `Kibit.html`), fill only the `«...»` placeholders,
replace each `.ph-empty` labelled block with `<img src="assets/…">`, and point the matching
Work card (and Home featured card if applicable) at the new file. NEVER change structure/styles
— only content. Role cards and goal cards can be added/removed freely (grids reflow).
Case-study images are clickable → open a fullscreen lightbox (scroll/click to zoom, drag to pan);
this is built into the template, Aventura and Kibit.

## Case-study header pattern (for future case studies)
Full-bleed image at top (navbar floats over it) → left-aligned tag pills → big Defante title → lead paragraph → meta-tag chips. Role cards: no icons. Outcome cards: thin Tabler (`ti ti-*`) icons.
