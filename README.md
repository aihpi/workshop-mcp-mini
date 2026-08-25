<div style="background-color: #ffffff; color: #000000; padding: 10px;">
<img src="00_aisc/img/logo_aisc_bmftr.jpg">
<h1> Which Tools May Your AI Agent Use? MCP in Practice
</div>

Materials for a 1-hour workshop for companies planning their own AI agents: how to find suitable use cases and connect them to tools and data via the **Model Context Protocol (MCP)** — safely. No programming skills required. Participants leave with their own workflow draft, a security assessment of it, and concrete next steps. (Full description, in German: [WORKSHOP_DESCRIPTION.md](WORKSHOP_DESCRIPTION.md); content plan: [PLAN.md](PLAN.md).)

## Agenda

| Time | Block |
|---|---|
| 0–15 min | Slides: agents, MCP, and the security risks that come with it |
| 15–25 min | Live example: from idea to a working agent — including its security assessment, done out loud |
| 25–45 min | Exercise in pairs (paper & pen): design your own workflow, find MCP servers, vet them |
| 45–60 min | Pitches and discussion |

## Repository map

| Folder | Contents |
|---|---|
| [01_slides/](01_slides/) | Marp slide deck (12 slides + 2 backups), with build instructions and speaker notes |
| [02_handouts/](02_handouts/) | The three printed handouts: [vetting checklist](02_handouts/pruefraster.md), [worksheet](02_handouts/worksheet.md), [server menu](02_handouts/server_menu.md) |
| [03_demo/](03_demo/) | The live-demo Langflow flow: setup, run of show, [filled model worksheet](03_demo/model_worksheet.md), fallback material |
| [04_facilitation/](04_facilitation/) | [Run of show](04_facilitation/run_of_show.md) for the facilitator |
| `00_aisc/` | AISC logos |

Materials are authored in **English**; translate to German at delivery time if the audience requires it. The source decks this workshop reuses live in `workshop-agentic-workflows/` (a separate repository, not tracked here — see the provenance map in [01_slides/README.md](01_slides/README.md)).

## Building the slides

```bash
cd 01_slides
mkdir -p build
awk 'FNR==1 && NR>1 {print "\n---\n"} {print}' slides/*.md > build/deck.md
npx @marp-team/marp-cli build/deck.md -o DRAFT_deck.pdf --allow-local-files
```

Handouts are plain Markdown; render them to PDF for printing with the same tool or any Markdown-to-PDF converter, and check each fits one A4 sheet (front/back).

## Status

- [x] Slides, handouts, model worksheet, run of show
- [ ] Langflow demo flow built and exported (see the checklist in [03_demo/README.md](03_demo/README.md))
- [ ] Fallback recording/screenshots
- [ ] Dry run, then trim

## Author
- [David Goll](https://hpi.de/kisz)

## License
See [LICENSE](LICENSE).

---

## Acknowledgements
<img src="00_aisc/img/logo_bmftr_de.png" alt="drawing" style="width:170px;"/>

The [AI Service Centre Berlin Brandenburg](http://hpi.de/kisz) is funded by the [Federal Ministry of Research, Technology and Space](https://www.bmbf.de/) under the funding code 16IS22092.
