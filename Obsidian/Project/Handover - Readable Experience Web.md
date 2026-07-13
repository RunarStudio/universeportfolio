# Handover — Readable Experience Web

**Date**: 2026-07-13 · **Branch**: `docs/prd-readable-experience-web`
**PRD**: [[PRD - Readable Experience Web]]

## Done ✅

1. **Webpage reviewed** — main readability issues: 9px node labels, Cinzel everywhere, dead space under constellation, no landing context, placeholder contact links, no routing, node descriptions are dead ends.
2. **Decisions locked** (via Q&A):
   - DB name: **🏛️ Hall of Deeds**
   - Page style: **Expanding star card** (star morphs into card in-place)
   - Body font: **Alegreya** (Cinzel stays for titles)
   - Sync: **manual command** → static `deeds.json`
3. **PRD written** → `Obsidian/Project/PRD - Readable Experience Web.md`, committed on branch `docs/prd-readable-experience-web`, pushed to remote.
4. **🏛️ Hall of Deeds created in Notion** under Runar Studio (sibling of Miniatures Museum, same `Published ✓` gating):
   - DB: `6cadfad0-b2b4-4847-ae1c-292f5506faf3` — https://app.notion.com/p/6cadfad0b2b44847ae1c292f5506faf3
   - Data source: `collection://d5ac6421-3631-4df2-a983-c394652a0acb`
   - Seeded with **8 draft deeds** (all unpublished), one per area, 2× Salesforce.

## Blocked ⚠️

- **PR creation fails** with "RunarStudio does not have the correct permissions to execute CreatePullRequest" despite ADMIN permission. Likely cause: **unverified primary email** after the account rename `ryuustark` → `RunarStudio`. Fix: verify at https://github.com/settings/emails, or open manually: https://github.com/RunarStudio/universeportfolio/compare/main...docs/prd-readable-experience-web
- Note: repo now lives at `RunarStudio/universeportfolio` (account renamed; old remote URL still redirects).

## Next steps (PRD build order)

1. [ ] **Readability pass** — Alegreya font, label sizes ≥12px, contrast, `preserveAspectRatio="xMidYMid meet"`, dead space, real contact links, intro line, `prefers-reduced-motion`.
2. [ ] **Star card** — expand/collapse morph, `[[wikilink]]` navigation, hash routes (`#/salesforce/vf-pdf`), mobile bottom sheet.
3. [ ] **Review seeded deeds in Notion** — adjust Impact/Story wording, tick `Published` when ready.
4. [ ] **Sync script** — `npm run sync`: Notion API → filter Published → `project/dev/js/deeds.json` (token in gitignored `.env`).

## Key files

- `project/dev/js/data.js` — skill tree model (node ids referenced by Hall of Deeds `Skill node`)
- `project/dev/css/styles.css` — CSS vars in `:root`
- `project/dev/js/tree-renderer.js` — node rendering + info panel (star card will replace `showInfo`)
