# Hannah's Kitchen — Design Spec

**Live**: https://hannahchoochoo.github.io/kitchen/
**Repo**: https://github.com/hannahchoochoo/kitchen
**Source**: single-file `index.html` (HTML + CSS + JS, no build step)

---

## What it is

A personal Korean + fusion home-cooking recipe book for one person (the owner). 43 recipes, 8 sections (반찬 / 국·찌개 / 단백질 / 덮밥 / 카레 / 면·죽 / 퓨전 / 라이트 나이트). Bilingual KR/EN. Includes a built-in shopping list (FAB → bottom sheet, persists to localStorage) and a "surprise me" recipe picker.

Designed for solo cooking with a Sunday batch-prep workflow — recipes show batch size, fridge life, freeze-friendliness.

Mobile-first, but used on desktop too (the live URL is opened on a laptop ~50% of the time).

---

## Current aesthetic direction

**Quiet** (current default) — minimal Japanese-leaning. Bone-paper background, near-black ink, charcoal accents, hairline borders. Drops the previous gochujang-red accent and emoji-decoration entirely. Inspired by MUJI / Kinfolk / Tartine cookbook.

Three legacy themes still ship as alternates: Editorial (Fraunces serif), Modern (Bricolage Grotesque sans), Cozy (DM Serif Display). The user can flip via a settings sheet (⚙ icon, top-right of header).

---

## Themes — token tables

### Quiet (default)

| Token | Value |
|---|---|
| `--bg` | `#FAFAF7` (bone) |
| `--bg-soft` | `#F2F1ED` |
| `--ink` | `#1A1A1A` |
| `--ink-soft` | `#6B6B68` |
| `--line` | `#E8E6E0` (hairline) |
| `--gochujang` (accent) | `#3A3633` (muted charcoal — was red in other themes) |
| `--tan` | `#8E8B85` |
| `--font-display` | `Cormorant Garamond, Times New Roman, serif` |
| `--font-kr` | `Shippori Mincho, Noto Serif KR, serif` |
| `--font-body` | `Cormorant Garamond, Georgia, serif` |
| Body size / line-height | `1.02rem` / `1.7` |

### Editorial

| Token | Value |
|---|---|
| `--font-display` | `Fraunces, serif` |
| `--font-kr` | `Gowun Batang, serif` |
| `--font-body` | `Inter, system-ui, sans-serif` |
| All colors | Same warm-paper palette as Modern (#FAF7F2 bg, gochujang red `#B23A2C`) |

### Modern (original default)

| Token | Value |
|---|---|
| `--font-display` | `Bricolage Grotesque, system-ui, sans-serif` |
| `--font-kr` | `Pretendard, sans-serif` |
| `--font-body` | `Inter, system-ui, sans-serif` |
| `--bg` | `#FAF7F2` (warm cream) |
| `--gochujang` | `#B23A2C` |
| `--gold` | `#C8973F` |
| `--green` | `#6B7E3F` |

### Cozy

| Token | Value |
|---|---|
| `--font-display` | `DM Serif Display, serif` |
| `--font-kr` | `Gowun Dodum, sans-serif` |
| `--font-body` | `DM Sans, system-ui, sans-serif` |

---

## Component inventory

### Header
- Bone background, hairline bottom border
- Quiet theme: left-aligned, asymmetric. Eyebrow `HANNAH'S KITCHEN` (uppercase, 0.7rem, 0.22em tracking) + h1 `한나의 키친` (Shippori Mincho, 500 weight, 2–2.75rem clamp) + italic tagline `Korean + Fusion · Home Cooking`
- Other themes: centered, has `· ❉ ·` ornament in accent color above h1
- ⚙ settings icon: 40px circle, hairline border, top-right absolute

### Filter / Search bar (sticky)
- Search input (rounded pill, hairline border, focus: accent color border)
- Filter chips: All / Quick / Batch / Freezer / Spicy / Veggie (plain text, no emoji as of v2.4)
- "Surprise" button at the end (✨ retained as sole emoji)

### Recipe card
- No background, no shadow. Bottom hairline border separator.
- Hover: shifts 0.4rem to the right
- Layout: `[Korean name (1.2rem) — English subtitle (1rem, italic)]  [time]`
- Description (0.92rem, ink-soft)
- Tags row: hairline-bordered pills, transparent bg, italic, no emoji

### Section header
- Format: `[Korean]   [English]` with a small bullet between
- Tracked uppercase, ink-soft

### Recipe modal
- Right-side slide-in panel, max-width 600px on desktop, full-screen on mobile
- Sticky header with `← Recipe` and `✕` close
- Body: KR + EN title block, `[time · serves · keeps]` meta, ingredients list, method (numbered), `+ Add to list` pill button (turns green ✓ on click for 1.4s)
- "Note" callouts: bg-soft background with accent-color left border

### Shopping FAB + Sheet
- FAB: 56px circle, fixed bottom-right, ink fill, white cart emoji 🛒, accent-color count badge
- Quiet theme: hairline border instead of drop shadow
- Sheet (bottom sheet on mobile, centered card on desktop): handle bar, "Shopping List" header, custom-add input, categorized items grouped by `produce / protein / pantry / other`, checkboxes per item, footer with `Clear checked / Clear list / 📋 Copy`

### Settings sheet
- Same bottom-sheet pattern
- Theme picker: 4 cards, each shows `[Theme name] | 한나의 키친 / Hannah's Kitchen` rendered in that theme's fonts
- Active theme: accent-color border, doubled width

### Toast
- Bottom-center pill, 5.5rem from bottom
- Ink fill, bg-color text, 1.2s show duration
- Used for: shopping list copy/clear actions only (the recipe add-to-list already shows green button feedback, no toast)

---

## Known things to improve / open questions for design

1. **Card hierarchy** — KR + EN currently same row, baseline-aligned. Could try stacked (KR primary, EN secondary smaller), or right-aligned EN, etc. Recipe-book convention TBD.
2. **Section spacing** — sections currently flow continuously with no visual separator beyond the section header. May want more breathing room between sections (currently `padding: 3rem 2rem` on `main` desktop).
3. **Modal pattern** — right-side slide-in feels app-y. Could go full-bleed editorial (modal becomes its own page-styled view with larger photo placeholder, drop cap, etc.). No recipe photos currently — should there be?
4. **Empty states** — `아무것도 없어요 · Nothing matches that` is bland. Could be a moment.
5. **No imagery** — currently 100% type. Open question: should there be Korean ink-wash illustrations (한국화), photography, hand-drawn icons for the section dividers?
6. **Mobile vs desktop** — desktop currently feels like a stretched mobile view. Could lean into desktop with a two-column or sidebar-nav layout.
7. **Print stylesheet** — none currently. A printable recipe card view would be a nice extra (`@media print`).

---

## Constraints

- **Single HTML file**, no build, no framework. Vanilla JS, CSS variables, Google Fonts CDN.
- **No backend**. Shopping list persists via `localStorage` only.
- **Hosted on GitHub Pages** at `hannahchoochoo.github.io/kitchen/`.
- **Personal use** — only one user. No accounts, no analytics, no tracking.
- **Bilingual is non-negotiable** — every recipe shows Korean + English. Korean is primary cultural identity, English is secondary.

---

## Brand voice

Warm but spare. The book opens with `> How to use this book / Each recipe lists batch size, fridge life, and freezer status.` — direct, declarative, no marketing copy. Korean phrases used throughout (잘 먹겠습니다 in footer, section names, dish names). Reads like a personal notebook, not a publication.

---

## Files

- `index.html` — entire app (~1400 lines)
- `recipes.md` — source recipe book (markdown, mirror of in-app data, kept in sync manually)
- `meal_prep_guide.md` — companion shopping/weekly planner
