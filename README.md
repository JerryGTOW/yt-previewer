# Thumbnail Previewer — Poker Theory edition

A client-side tool that drops your YouTube thumbnail(s) into a pixel-faithful clone of
the real YouTube interface — surrounded by competing **poker-theory** videos — so you can
judge whether your thumbnail and title actually stand out in a real feed.

Everything runs in the browser. Uploaded images stay in memory (object URLs) — nothing is
sent to a server.

## Run it

```bash
cd thumbnail-previewer
npm install
npm run dev
```

Then open the printed local URL (default http://localhost:5173).

Build a static bundle with `npm run build` (output in `dist/`).

## What's inside

### Three views (switch via the top control bar)
- **Home feed** — responsive YouTube homepage grid; your thumbnails are mixed in among the
  poker placeholders.
- **Watch page** — large player on the left + the **"Up Next" right sidebar** (the side
  banner) where your thumbnails appear as compact recommendation cards.
- **Search** — horizontal one-video-per-row results layout with a live text filter.

### Uploading & editing
- Drag-and-drop zone + **Upload images** button (multiple PNG/JPG/WEBP at once).
- **Try a sample** loads a generated demo poker thumbnail.
- Open the **Studio drawer** (Add thumbnails) any time to add more.
- Per-thumbnail inline editing: title, channel name, channel avatar (optional upload),
  view count, upload age, and duration badge. All edits are live.

### Preview controls
- **Refresh thumbnails**: swaps the competing videos for a different random set of real
  poker videos (from a 31-video pool) while keeping your own uploads in place.
- **Place mine**: Top / Middle / Random (default). In Random mode each upload lands in its
  own segment of the grid, so multiple thumbnails are spread out and never adjacent.
- **Change placement**: re-rolls where your thumbnails sit in the grid (forces Random) — click
  repeatedly to test different placements.
- **Highlight mine**: amber ring + badge so you can spot your thumbnail vs. the competition.
- **Device**: Desktop / Tablet / Mobile — reflows grid columns, sidebar, and the top bar
  the way YouTube does.
- **Theme**: Dark (default) / Light.

### Competing videos (real)
16 **real** poker-theory YouTube videos (Phil Galfond, GTO Wizard, Jonathan Little, The
Poker Bank, etc.) — real thumbnails (served from `i.ytimg.com`), real titles, and real
channel names validated via YouTube's oEmbed endpoint. On the Watch page the selected real
video **plays** via an embedded YouTube player. View counts and upload ages are realistic
approximations for the mock feed. (User-uploaded thumbnails without a video still fall back
to a generated poker placeholder.)

## Component structure

```
src/
  App.jsx                 orchestration + state + Studio drawer
  ControlBar.jsx          tool chrome (views, device, theme, placement, highlight)
  components/
    TopBar.jsx            YouTube top bar (logo, search, right icons)
    LeftSidebar.jsx       collapsible nav rail
    VideoCard.jsx         home-feed grid card
    CompactCard.jsx       watch-page sidebar recommendation card
    SearchRow.jsx         search-results row
    UploadZone.jsx        drag-and-drop + upload + sample
    EditPanel.jsx         inline metadata editor
    Thumb.jsx             16:9 thumbnail (image or generated) + duration/highlight
    Avatar.jsx            channel avatar (image or colored initials)
    PokerThumb.jsx        procedural poker placeholder SVG + sample generator
    icons.jsx             inline SVG icon set
  views/
    HomeFeed.jsx
    WatchPage.jsx
    SearchResults.jsx
  data/pokerVideos.js     placeholder catalog
  utils.js                view/metadata formatting helpers
```

## Tech
React 18 + Vite + Tailwind CSS v4 (class-based dark mode). No backend, no external storage.
