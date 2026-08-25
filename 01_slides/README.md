# Slides: MCP in Practice (15 min + backups)

Marp deck for the first block of the workshop (0–15 min), plus two backup slides for technical Q&A. One Markdown file per slide in [slides/](slides/); only `00_title.md` carries the Marp front matter. Every slide has speaker notes (`<!-- Notes: ... -->`) with the depth that does not belong on the slide — Marp shows them in presenter view.

## Provenance

Slides marked *(source)* were adapted from the decks in `workshop-agentic-workflows/` (not tracked in this repo); the rest are new for this workshop.

| Slide | Source |
|---|---|
| 00 title + agenda | new |
| 01 what is an agent | 01_agentic_systems_overview_FB `slides_en/02` + `03`, merged |
| 02 email triage example | 01 `slides_en/07`, adapted |
| 03 the N×M problem | 02_mcp_DG_PM `slides/01`, nearly as-is |
| 04 how MCP works | 02 `slides/02`, nearly as-is |
| 05 ecosystem + directories | new, distilled from 02 `slides/08` notes |
| 06 descriptions are prompts | 02 `slides/03`, trimmed (JSON-RPC cut) |
| 07 attack surface | 02 `slides/06` + 01 `slides_en/13`, merged |
| 08 real incidents | 02 `slides/06` |
| 09 containment | 01 `slides_en/14` + 02 `slides/07`, merged |
| 10 vetting checklist | new (walks through `../02_handouts/pruefraster.md`) |
| 11 exercise briefing | new |
| 90/91 backups (API comparison, wire format) | 02 `slides/04` + `03` |

Diagrams in [img/](img/) are the license-free self-made SVGs copied from the source decks.

## Build

```bash
cd 01_slides
mkdir -p build
awk 'FNR==1 && NR>1 {print "\n---\n"} {print}' slides/*.md > build/deck.md
npx @marp-team/marp-cli build/deck.md -o DRAFT_deck.pdf --allow-local-files
```

Live preview with presenter view: `npx @marp-team/marp-cli -s .` then open the deck in the browser and press `p`.

## Before the dry run

- Final workshop date on the title slide.
- Fast-moving numbers live in speaker notes only and are marked "verify before the talk" (registry size, benchmark figures).
- Decide whether a German translation of the deck is needed (materials are authored in English by design).
