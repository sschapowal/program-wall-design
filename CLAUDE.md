# MoMA Lobby Screens — R4

Local prototype of MoMA's four adjacent 1080×1920 portrait lobby monitors. This is iteration R4, built for rapid design iteration using handwritten code edits and the Figma MCP.

Live screens (network-accessible): `https://www.moma.org/screens/{welcome,collections,exhibitions,directory}`

---

## File Structure

```
R4/
├── CLAUDE.md                      ← this file
├── screen-1-welcome.html          ← Screen 1: date/time, today's events
├── screen-2-collections.html      ← Screen 2: floor-by-floor collection guide
├── screen-3-exhibitions.html      ← Screen 3: now-open exhibitions
├── screen-4-directory.html        ← Screen 4: full floor directory
├── .vscode/
│   └── mcp.json                   ← Figma Desktop MCP (127.0.0.1:3845)
└── shared/
    ├── styles.css                 ← all design tokens, reset, and shared components
    └── fonts/                     ← reserved for local font files if needed
```

Each HTML file is self-contained and opens directly in a browser. All share `shared/styles.css`.

---

## Design System

### Typography
- **Font**: `"MoMA Sans", Helvetica, Arial, sans-serif`
- **Source**: Loaded via `@font-face` from `moma.org` CDN — requires internet connection to render correctly. Falls back to Helvetica.
- **Base size**: `html { font-size: 62.5% }` → `1rem = 10px`
- **Weights**: 300 (light), 400 (regular), 700 (bold), 900 (black)

### Color Palette
| Token | Value | Usage |
|---|---|---|
| `--color-bg` | `#222222` | Default screen background |
| `--color-bg-dark` | `#000000` | Dark section backgrounds |
| `--color-bg-mid` | `#444444` | Dividers, mid-tone areas |
| `--color-bg-light` | `#1a1a1a` | Artwork placeholders |
| `--color-text` | `#ffffff` | Primary text |
| `--color-text-muted` | `#aaaaaa` | Secondary text |
| `--color-text-dim` | `#999999` | Tertiary/label text |
| `--color-divider` | `#444444` | Horizontal rules |
| `--color-accent-teal` | `#4dd8c0` | Featured exhibition highlight |

### Spacing & Layout Variables
```css
--header-height:      16rem   /* top header band */
--floor-height:       23.6rem /* standard floor row height */
--floor-gap:          0.4rem  /* gap between floor rows */
--margin-side:        4rem    /* horizontal page margins */
--margin-top:         4rem    /* section top padding */
--floor-padding:      3rem    /* floor cell padding */
--floor-v-padding:    3.2rem  /* floor vertical padding */
--highlighted-height: 28rem   /* featured exhibition info panel */
--events-gap:         4rem    /* gap between event columns */
```

### Animation Timing
```css
--transition-timing:  500ms  /* fades */
--translate-timing:   1200ms /* slide transitions */
--transition-curve:   linear
```

---

## Screen Dimensions

| Property | Value |
|---|---|
| Width | 1080px |
| Height | 1920px |
| Orientation | Portrait |
| Environment | Physical lobby monitors |

**To preview locally at correct size:**
1. Open any HTML file in Chrome
2. Open DevTools (⌥⌘I) → device toolbar (⇧⌘M)
3. Set custom size: `1080 × 1920`

---

## Artwork Placeholders

No raster images are used. All artwork areas use the `.artwork-placeholder` class:
```css
.artwork-placeholder {
  background-color: var(--color-bg-light); /* #1a1a1a */
}
```

Replace with `<img>` tags or `background-image` CSS when connecting to real CMS data.

---

## Content Notes

All content is static placeholder text matching the live screens as of **March 27, 2026**. Update by editing the HTML directly.

### Screen 1 — Welcome
- Header shows date/time (static)
- Events section: 3-column grid, 2 pages (pagination dots)
- Promo: "Shop Good Design" — Floors 1, 2, and 6
- Footer: multilingual welcome text

### Screen 2 — Collections
- "On View" header
- Floors 5, 4, 3, 2 — each with era label, artist list, artwork placeholder
- Artwork fills right 50% of each floor row

### Screen 3 — Exhibitions
- "Now Open" header
- Exhibition cards stack vertically: artwork placeholder (top) + info panel (bottom)
- Featured card uses `--color-accent-teal` background (`exhibition-card__info--accent`)
- Current exhibitions: Wifredo Lam, Rose B. Simpson, Frida and Diego, Ideas of Africa

### Screen 4 — Directory
- "Directory" header
- Floors 6 → 1, each row: floor number + show list + amenity labels
- Floor 6: no gallery access (dimmed text)
- Amenities: Terrace Café (6), Café 2 (2), Store (2), Museum Store (1), Art Lab (1)

---

## Figma MCP

`.vscode/mcp.json` connects VS Code to the local Figma Desktop MCP server:
```json
{ "servers": { "figma": { "url": "http://127.0.0.1:3845/mcp" } } }
```

Requires Figma Desktop app to be running. Enables Claude to read frames from Figma and translate them directly into code edits.

---

## Production Reference

The live screens use two stylesheets:
- `moma.org/dist/sol.[hash].css` — global MoMA styles
- `moma.org/dist/screens-2019.[hash].css` — screens-specific styles

The production class naming system uses design-token-style utility classes (e.g. `$color/background:gray:222`, `$typography/size:80pt`). The local R4 prototype uses semantic BEM-style classes defined in `shared/styles.css` instead.
