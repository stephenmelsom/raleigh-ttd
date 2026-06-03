# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A static, single-page site listing favorite restaurants, coffee shops, bakeries, ice cream, and attractions around Raleigh & Cary, NC — made to share with friends and family. Two hand-edited files (`index.html`, `style.css`), no build step, no framework. The only runtime dependency is Leaflet 1.9.4 (loaded from unpkg CDN) for the interactive map at the top.

- **Live:** https://stephenmelsom.github.io/raleigh-ttd/ (GitHub Pages, source = `main` / root; redeploys automatically on push)

## Develop & preview

Open `index.html` directly in a browser, or serve the folder (needed for the map's geolocation to behave):

```sh
python3 -m http.server   # then visit http://localhost:8000
```

There are no tests, linters, or build commands.

## Architecture

Everything lives in `index.html`: the content cards, plus an inline `<script>` at the bottom that builds the Leaflet map. `style.css` holds all styling (CSS custom properties at `:root` for the theme; deep-teal accent `#0F766E`).

Content is grouped into six sections, each with a sticky-nav anchor: **Short List**, **Restaurants**, **Coffee & Tea**, **Bakeries**, **Ice Cream**, **Attractions**. The Short List re-lists a few favorites whose cards already appear in their category section — so those places exist as **two** `<article class="card">` blocks in the HTML, but only **one** entry on the map.

`raw.txt` is the original source notes — reference only, not used by the site.

## Adding or editing a place — keep two places in sync

A place is defined in two independent spots that must agree:

1. **The card** — an `<article class="card">` in the matching section's `<div class="grid">`. Copy an adjacent card and update: `<h3>` name, a city `<span class="pill">` (e.g. Raleigh / Cary / Durham), an optional modifier pill (`.breakfast`, `.kids`), the `<p>` description, and two `card-links`: a Website link and a Map link of the form
   `https://www.google.com/maps/search/?api=1&query=<URL-encoded "Name, Address">`.

2. **The map marker** — a row in the `places` array inside the inline `<script>`: `['Name', 'category', lat, lng]`. Category must be one of the keys in the `C` color object: `restaurant`, `coffee`, `bakery`, `icecream`, `attraction`. You need real lat/lng coordinates here (the Google Maps query string alone won't place a marker).

When the user asks to add a place, web-search for the official website + street address, build both the card and the map row, and **do not** add Short-List places to the `places` array a second time. Then commit and `git push` — Pages redeploys on its own.
