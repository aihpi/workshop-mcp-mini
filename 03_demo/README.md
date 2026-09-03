# Live demo — the KISZ inbox assistant (Gmail + Calendar + FAQ)

The worked example for the workshop's live slot (~15–25 min). An agent in **Langflow** helps the KI-Servicezentrum's shared inbox: it **answers questions from the KISZ FAQ** and **drafts appointment replies from the calendar** — then we show how the same setup gets **hijacked by a single incoming email**, and how least privilege fixes it. The demo walks the *same* path the participants walk right afterwards.

> ⚠️ Design docs only — **nothing is built yet**. Server choice is deliberately still open (see `02`/`03`). Verify all server names/scopes and Google facts before building.

## This folder

| File | What it is |
|---|---|
| [`01_use_case.md`](01_use_case.md) | The use case as a worked worksheet (idea → narrowing → why-agentic) |
| [`02_server_search.md`](02_server_search.md) | Our real search walkthrough + candidate shortlist (official Google prioritized) |
| [`03_security_assessment.md`](03_security_assessment.md) | Prüfraster verdicts, Trifecta/Rule-of-Two, the mitigations = the "fix" |
| [`04_build_plan.md`](04_build_plan.md) | The Langflow build (flow, OAuth checklist, system prompt, tool-toggle) |
| [`05_example_emails.md`](05_example_emails.md) | Seed emails + prompts + expected behaviour (incl. the attack) |
| [`faq/`](faq/) | KISZ FAQ markdown the read-only FAQ server serves |
| `fallback/` | Screenshots + recording go here (produced when building) |

## The flow

```
Chat Input ─► Agent (KISZ AI Hub LLM) ─► Chat Output
               ▲ tools
               ├── MCP: Email + Calendar   (read + draft · [send]/[delete] off for the safe config)
               └── MCP: FAQ (filesystem, read-only, scoped to faq/)
```

## Run of show (~10 min)

1. **Idea → narrow (1 min):** "help our shared inbox" → answer FAQ questions + draft appointment replies (`01`).
2. **Search (2 min):** hunt a directory for gmail/calendar; hit the fake-"official" listing, then find the *genuinely* official Google server (`02`). Lesson: "official" is a claim to verify.
3. **Assess (2 min):** run candidates through the Prüfraster live → the whole-workflow Trifecta → the config that makes it acceptable (`03`).
4. **Connect + good run (3 min):** Refresh Tools (discovery, live), then the sichte-Prompt → FAQ-grounded answer + a calendar slot proposal. The value.
5. **Reveal + fix (3 min):** one incoming email (`E6`) hijacks the run — forward of the confidential mail + calendar delete — then **toggle off `send`/`delete`** → re-run → defanged. 🔴→🟡.

## Setup (summary)

Throwaway Google account + Google Cloud OAuth (least-privilege scopes), a Langflow flow with two MCP nodes, the FAQ folder, and a tool-call-tested AI-Hub model. Full steps in [`04_build_plan.md`](04_build_plan.md).

## Fallbacks (build before the dry run)

Screen recording of the good run + the reveal, and screenshots (canvas, tool list, a draft, the caught injection) in `fallback/`. The assessment half (`03`) needs no technology and always works on paper.
