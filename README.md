# The Twilight Zone Catalogue

A complete interactive catalogue of the classic original series. Browse, search, filter, and track all 156 episodes across five seasons from 1959 to 1964.

**Live site:** [tz.scheiber.dev](https://tz.scheiber.dev/)

---

## Overview

The Twilight Zone Catalogue is a single-file vanilla HTML/CSS/JS web app. It fetches episode data from a [Railway-hosted REST API](https://twilight-zone-api-production.up.railway.app/episodes) and renders a responsive, filterable grid of episode cards. No build tools, no frameworks, no external dependencies other than Google Fonts.

---

## AI Disclaimer

This project was created and developed by a human, but an AI assistant ([Claude Code](https://claude.ai)) was used for brainstorming, code generation, design, and debugging purposes. The final implementation and design decisions were made solely by the author, and all generated code, content, and logic were reviewed, tested, and validated by the author prior to inclusion. Any errors, bugs, or issues in the final product are the responsibility of the author. The AI was a tool to assist in the creative and development process, but the vision, implementation, and final product are entirely the work of the author.

---

## Features

### Browsing and Search

- **Full-text search** across episode title, plot summary, cast, writer, director, and theme tags, with a debounced input and a one-click clear button.
- **Season filter bar** to jump between All, Seasons 1 through 5, or any personal collection (Favorites, Watchlist, Viewed).
- **Sort options** for air date (default), title A-Z, or season order, with articles ("The", "A", "An") stripped for accurate alphabetical sorting.
- **Random Episode** button that opens a randomly selected episode modal instantly.
- **Live episode count** that updates to reflect the current filtered view.

### Episode Cards

- Photo or stylized placeholder for each episode, with graceful runtime fallback if an image URL returns a 404.
- **Must Watch** badge (star icon) on curated standout episodes.
- **Viewed** badge and subtle image dimming on episodes marked as watched, so unwatched entries visually stand out.
- Clicking any card opens the full episode detail modal.

### Episode Modal

- Full episode detail including season and episode number, air date, writer, director, runtime, and plot summary.
- **Cast list** rendered as clickable chips: tapping an actor's name closes the modal and runs a search for all their appearances.
- **Theme tags** rendered as clickable chips: tapping a theme filters the grid to episodes sharing that theme.
- **Collection action buttons** to toggle Favorites, Watchlist, and Viewed status directly from the modal.
- **Previous / Next navigation** buttons (and a mobile bottom bar) that step through the currently filtered and sorted episode list.
- **Swipe navigation** on touch devices: swipe left or right to move between episodes.
- Keyboard support: arrow keys navigate between episodes, Escape closes the modal.

### Personal Collections

All three collections (Favorites, Watchlist, Viewed) are stored in `localStorage` and persist across sessions. Each collection is accessible as a filter in the season bar. The stats panel tracks collection progress.

### Stats Panel

An expandable drawer with at-a-glance statistics for the full episode catalogue:

- Top writers and directors (by episode count), each clickable to run a search.
- Top theme tags by frequency, each clickable to filter by that theme.
- Top cast members by appearance count, each clickable to run a search.
- Season-by-season episode counts, each clickable to switch to that season.
- Viewing progress: total episodes watched, percentage complete, and a per-season breakdown.
- Collection counts for Favorites and Watchlist, each clickable to switch to that collection view.

### Themes and Visual Design

- **Dark mode** (default): deep navy background, film-grain overlay, subtle scanline texture, and a procedurally generated animated starfield in three twinkling layers.
- **Light mode**: vintage newsprint palette with warm paper tones and a heavier grain overlay.
- Theme preference persists in `localStorage` and is restored before first paint (no flash of wrong theme).

### URL State and Deep Linking

The current view (season filter, sort order, search query, and open episode) is serialized into the URL hash (e.g., `#season=2&sort=title&q=serling&ep=51`). This means any filtered view or open episode can be shared as a direct link. Browser back/forward navigation restores state correctly.

### Accessibility and UX Details

- Masthead click resets all filters and scrolls to the top (a global "go home" shortcut).
- Back-to-top button appears after scrolling past the hero.
- Mobile-optimized layout with a fixed bottom navigation bar for episode modal browsing.

---

## Architecture

| Concern     | Approach                                                      |
| ----------- | ------------------------------------------------------------- |
| Data source | Railway-hosted REST API (`/episodes`)                         |
| Rendering   | Vanilla JS DOM manipulation, no framework                     |
| State       | In-memory JS variables, synced to URL hash and `localStorage` |
| Styling     | Pure CSS custom properties, two themes, no preprocessor       |
| Fonts       | Playfair Display (headings) and Inter (body) via Google Fonts |

---

## Local Development

No build step required. Clone the repo and open `index.html` in a browser, or serve it with any static file server:

```bash
npx serve .
# or
python3 -m http.server
```

To point at a local API instance, swap the `API` constant near the top of the script block:

```js
// const API = "https://twilight-zone-api-production.up.railway.app/episodes";
const API = "http://localhost:3000/episodes";
```
