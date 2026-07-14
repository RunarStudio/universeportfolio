# PRD — Readable Experience Web

**Status**: Draft approved decisions · 2026-07-11
**Goal**: Turn the Skills Constellation into a clearly readable showcase of experiences across all areas, backed by a Notion database in Runar Studio ([[🏛️ Hall of Deeds]]) with the same publish behaviour as 🏛️ Miniatures Museum.

**Decisions locked**: Hall of Deeds (DB name) · Expanding star card (page style) · Alegreya (body font) · Manual sync command (Notion → web).

---

## 1. Problem

The constellation is beautiful but hard to *read* and impossible to go *deeper*:

- Node labels ~9px, red-on-dark, letter-spaced Cinzel → illegible; locked nodes nearly invisible.
- Cinzel used for **everything** — decorative fonts fight body reading.
- Large empty dark area under the constellation; info panel gets lost.
- Landing gives zero context (who is this? what do I click?).
- Contact links are placeholders.
- Node descriptions are dead ends — no projects, metrics, dates, or links.
- No URL routing — nothing is shareable.

## 2. Solution overview

Three stages, like turning pages:

1. **Wheel** (exists) — pick an area.
2. **Constellation** (exists, needs readability pass) — pick a star.
3. **Star Card** (new) — the star expands in-place into a readable card: the "page" of that skill, listing its deeds (experiences) pulled from [[🏛️ Hall of Deeds]], cross-linked with `[[wikilinks]]` like an Obsidian note.

Keep all existing animation language (twinkle, wheel rotation, reveal easing).

---

## 3. Pages (Obsidian-style synthesis)

### [[Landing — The Wheel]]
- Add a one-line intro under the title: *"Seven disciplines. Click a realm to open its constellation."*
- Fix contacts: real mailto / LinkedIn / Instagram URLs.
- Fade the intro out on first interaction (keeps the clean look).

### [[Constellation View]]
- Labels: min 12px, Alegreya for labels, `--color-text` (light) with accent only on hover/unlocked ring.
- Locked nodes: raise contrast (visible ghost, not invisible).
- Kill dead space: constellation vertically centered, `preserveAspectRatio="xMidYMid meet"` (no stretch).
- Legend chip: ● unlocked · ◌ planned.
- Hash route: `#/salesforce`.

### [[Star Card]] (new — the core deliverable)
- Click a star → it expands in-place into a card (scale + morph animation, ~400ms, same `--ease`).
- Card content, top to bottom:
  - **Title** (Cinzel) + rank badge.
  - **Description** (Alegreya, 16px, line-height 1.6).
  - **⚔ Deeds** — experience entries from Hall of Deeds tagged with this skill: name, one-line impact metric, date, optional link.
  - **Linked skills** — `[[wikilinks]]` to parent/child nodes; clicking swaps the card (Obsidian navigation feel).
- `Esc` / ✕ / click-outside collapses back to the star.
- Hash route: `#/salesforce/vf-pdf`.

### [[Hall of Deeds — Web Wing]] (optional stage 4, later)
- A gallery page listing all published deeds across areas — the "museum walk" version. Not in v1.

---

## 4. Data — [[🏛️ Hall of Deeds]] (Notion, Runar Studio)

Sibling of 🏛️ Miniatures Museum, same behaviour: **only `Published ✓` rows reach the web**.

| Property | Type | Mirrors Museum |
|---|---|---|
| Name | title | Name |
| Slug | text (auto from Name if empty) | Slug |
| Published | checkbox — gates web visibility | Published |
| Area | select: Salesforce, Integrations, DevOps, Front-End, AI & Tools, Organization, Creative | Room / Wing |
| Skill node | text — node id (e.g. `vf_pdf`) | — |
| Type | select: Project, Role, Certification, Side quest | Game |
| Impact | text — one-line quantified metric ("−80% legacy tool usage") | Notes |
| Story | text — longer lore for the card | Notes |
| Date | date range | Date painted |
| Tech | multi-select | Technique |
| Link | url | — |
| Cover image | file (optional) | Cover image |

### Sync (manual command)
- `npm run sync` (or ask Claude): script queries Hall of Deeds via Notion API → filters `Published` → writes `project/dev/js/deeds.json` → commit + push deploys it.
- Site loads `deeds.json` statically; zero runtime dependency on Notion.
- No secrets in repo: Notion token lives in local `.env` (gitignored).

---

## 5. Readability system (global)

- **Fonts**: Cinzel (titles only) + **Alegreya** 400/700 (all body). One extra Google Fonts request.
- **Contrast**: body text `#e8d8f0` on dark ≥ 7:1; muted text only for hints.
- **Type scale**: body 16px min; labels 12px min; card title `--text-xl`.
- **Motion**: keep everything, but honor `prefers-reduced-motion` (disable twinkle + wheel auto-effects).
- **Mobile**: star card becomes a bottom sheet at ≤768px.

---

## 6. Out of scope (v1)

- Live Notion fetch at page load.
- Hall of Deeds gallery page (stage 4).
- CMS for skill tree structure itself (`data.js` stays hand-edited).

## 7. Success criteria

- Every label legible at arm's length on a laptop.
- A recruiter can land → click → read a quantified experience in ≤ 3 clicks.
- You publish a new deed by ticking a checkbox in Notion + one sync command.
- Any star card is shareable via URL hash.

---

## 8. Build order

1. **Readability pass** — fonts, label sizes, contrast, dead space, real contacts, intro line. *(pure CSS/HTML, ship first)*
2. **Star card** — expand/collapse animation + wikilink navigation + hash routing.
3. **Hall of Deeds** — create Notion DB + seed 5–10 deeds from CV.
4. **Sync script** — Notion → `deeds.json`, wire deeds into star cards.
