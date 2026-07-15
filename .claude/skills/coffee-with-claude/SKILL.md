---
name: coffee-with-claude
description: Build a "Café con Claude" thread-notes essay page for a podcast episode, matching the house style of this repo (self-contained Spanish HTML with a side-rail table of contents and "persiana"/accordion sections). Use whenever adding a new Episode NN page to thread-learning-notes from a research report or transcript, or when reusing this reading-room style. Also handles linking the new page into index.html.
---

# Café con Claude — episode essay style

Turns an episode research report (or transcript notes) into a single, self-contained
HTML "reading room" page that matches every other episode in this repo, and links it
from `index.html`.

Each page is a Spanish essay that **re-tells the episode from its center** — a single
thesis stated up front — rather than dumping the report's sections verbatim. The
report is raw material; the page is a rewrite.

## What the style is

- **One self-contained `.html` file per episode.** All CSS and JS are inline. The only
  external dependency is the Google Fonts link (Fraunces for display, Spectral for body).
- **Language:** Spanish (`<html lang="es">`).
- **Layout:** a sticky left **rail** with the brand mark, a subtitle, and a
  table of contents; a main column of collapsible **persianas** (accordion sections).
- **Reading aids:** a top scroll-progress bar, scroll-spy that highlights the active
  TOC entry, click-to-open TOC links, a mobile hamburger menu, and a "← Volver a la sala"
  link back to `index.html`.
- **No font-size / zoom control.** (It was removed from the house style — do not add
  an `A− / A+` control back to the rail.)

## How to build a new page

1. **Copy `template.html`** (in this skill folder) to the repo root as
   `Episode NN - <Title in English>.html`. Keep the apostrophe/dash filename convention
   of the existing files (e.g. `Episode 63 - The Mission of Jesus in Luke's Gospel.html`).
   Filenames use a dash where the title has a colon.
2. **Fill in every `{{PLACEHOLDER}}`.** They are:
   - `{{TITULO_ES}}` — short Spanish title (also used in the tab title and header comment).
   - `{{SUBTITULO_ES}}` — Spanish descriptive subtitle for the `<title>` tag.
   - `{{TEMA}}` / `{{RANGO_BIBLICO}}` — e.g. `La misión de Jesús` / `Lucas 4–8`.
   - `{{TITULO_INICIO}}` + `{{PALABRAS_DESTACADAS}}` — the `<h1>`, where the highlighted
     words sit in `<em>` (rendered in terracotta).
   - `{{SUBTITULO_DESCRIPTIVO}}` — the italic hero subtitle (1–2 sentences of the thesis).
   - `{{FRASE_CENTRAL_DEL_EPISODIO}}` — the amber-barred lede: the single line the whole
     page is built around.
   - Section titles, paragraphs, facet/list content, and the closing `{{PARRAFO_DE_CIERRE}}`.
3. **Add the real sections.** The template ships two example persianas (one prose section
   with a `.lead`, a `.facet`, and a `.refs` block; one with a `.clean` list). Duplicate
   `<section class="persiana">` for every section you need, and **keep three things in sync**:
   - the Roman numeral in `.roman`,
   - the `id="sN"`,
   - and the matching `<a data-target="sN">` entry in the rail `<nav class="toc">`.
   Only the first section should be `data-open="true"`; all others `data-open="false"`
   (and their `.lever` `aria-expanded` must match).
4. **Building blocks available** (all styled by the inline CSS):
   - `<p class="lead">` — a plum, italic opening line for a section.
   - `<div class="facet">` — a bordered callout. Color variants: default (olive),
     `.amber`, `.plum`, `.terra`. Optional `<span class="kicker">` inside the `<h4>`.
   - `<ul class="clean">` — dot-marker list; wrap the lead phrase of each `<li>` in `<strong>`.
   - `<div class="refs">` — scripture references. Link to Bible Gateway, version **DHH**:
     `https://www.biblegateway.com/passage/?search=Lucas+4%3A16-21&version=DHH`
     (use `+` for spaces and `%3A` for the `:` in verse ranges; accented book names are
     URL-encoded, e.g. `Isa%C3%ADas`).
   - `<span class="scripture">` — inline italic/plum for quoted scripture.
   - `<div class="coda">` … `<span class="signoff">` — the closing paragraph + sign-off.
5. **Link it from `index.html`.** Add an `<li>` to the correct section — Mark episodes go
   under **"Marcos & podcast"**, Luke under **"Lucas & podcast"** — in the same shape as
   the neighbors:
   ```html
   <li><a href="Episode NN - <Title>.html">Episode NN - <Title with colon></a><span class="tag">Essay</span></li>
   ```
   The link text may use a colon even though the filename uses a dash.

## Content guidance (writing the essay)

- **State the thesis first** (section I), then let the rest of the page argue and
  illustrate it. Mirror the arc the source report already implies: source → declaration
  → demonstration → implications.
- Common section shapes across episodes: the thesis; the purpose of the walk-through;
  the biblical passages read closely; a "what stays with you" key-insights list; an
  illustrations section (facets); practical applications; and a conclusion with open
  questions. Adapt to the episode — don't force all of them.
- Keep the register warm and essayistic. Use `<strong>` sparingly for anchor ideas and
  `<em>` for nuance, as the existing pages do.

## Verify before committing

- Every `{{...}}` placeholder is gone.
- TOC numerals, section `id`s, and `data-target`s all line up.
- Exactly one section is open by default.
- The `index.html` link points at the exact filename.
