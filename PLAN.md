# Build Plan: "Welche Tools darf Ihr KI-Agent nutzen? MCP in der Praxis" (1h)

This is the plan for producing the workshop materials. Sources: `WORKSHOP_DESCRIPTION.md` (the contract), `workshop-agentic-workflows/01_agentic_systems_overview_FB` and `02_mcp_DG_PM` (slide material to reuse), `MCP_workflow_ideation/` (worksheet to rework). All materials are authored in English; translation to German happens later if needed.

## 1. Constraints that shape everything

- **60 minutes total**, and the description explicitly asks to compress the front so discussion gets more time.
- **Mixed audience**: programming skills are not *required*, but the room will contain technical people too. The bar is not "avoid technical terms" — it is "every term introduced must be explainable in one sentence and must pay off later" (in the exercise, where directory listings say things like *stdio*, *Streamable HTTP*, *OAuth*, or in the security section). Protocol *internals* that don't pay off (JSON-RPC framing, spec revisions, sampling/elicitation) stay in speaker notes for Q&A.
- **Promised takeaways** (from the abstract): a workflow draft, a security assessment of it, and concrete next steps. The security "Prüfraster" (vetting checklist) is promised explicitly and does not exist yet — it is the biggest new artifact.
- **Paper and pen exercise**: participants search MCP directories (needs phones/laptops or a printed fallback) and fill in a worksheet.

## 2. Proposed agenda (tightened from the description)

| Time | Block | Materials needed |
|---|---|---|
| 0–15 | Intro + slides: agents in 3 slides, MCP in 4, security in 4 | New compact deck (~12 slides) |
| 15–25 | Live example: idea → working agent, security assessment done out loud | Pre-built Langflow flow + filled model worksheet |
| 25–45 | Exercise: participants draft their own use case + vet servers | Worksheet v2 + Prüfraster + curated server menu |
| 45–60 | Peer presentation + discussion | Facilitator prompts, doc-camera or just talking |

The 5 minutes moved from the front (20→15) go to the discussion block (10→15), per the description's wish.

## 3. Slide deck: selection map (~12 slides, 15 min)

New deck, assembled mostly from existing slides. Reuse the Marp workflow from `02_mcp_DG_PM` (per-slide `.md` files, concat + marp build); final PPTX in the AISC template can follow the part-01/02 process later.

| # | Slide | Source | Adaptation |
|---|---|---|---|
| 0 | Title + agenda | template | new |
| 1 | What is an agent (LLM + tools + loop) | 01/`02_from_llm_to_agent` + `03_what_is_an_agent` | merge into one, keep the diagram, drop definitions taxonomy |
| 2 | A concrete example: email triage | 01/`07_ai_workflows_practice` | reuse nearly as-is; it's the mental model for the exercise |
| 3 | The problem: N×M integrations | 02/`01_the_problem` | reuse as-is (already audience-appropriate) |
| 4 | How MCP works (host/client/server; tools, resources, prompts; stdio vs. HTTP) | 02/`02_how_mcp_works` | reuse nearly as-is: the primitives and the two transports stay by name (one sentence each) — participants meet exactly these words on directory pages minutes later |
| 5 | The ecosystem: thousands of servers, where to find them | 02/`08_summary` + worksheet links | new-ish: show the directories (github.com/mcp, PulseMCP, mcpsafe.org) — this primes the exercise |
| 6 | Discovery: the client asks `tools/list`, descriptions are prompts | trimmed from 02/`03_on_the_wire` | keep one real (shortened) tool description on the slide — it's the payoff for the technical crowd AND the mechanism that makes prompt injection / tool poisoning explainable to everyone; cut the JSON-RPC framing around it |
| 7 | Security I — why this is a new attack surface | 02/`06_security` + 01/`13_sicherheit` | merge: server acts with your permissions, foreign text steers the model (prompt injection), Lethal Trifecta |
| 8 | Security II — real incidents | 02/`06_security` notes | the existing arc: GitHub/Invariant demo (May 25) → Asana cross-tenant bug (June 25) → postmark-mcp supply chain (Sept 25); "demonstrated in May, real by September" |
| 9 | Security III — how to contain it | 01/`14_sicherheit_massnahmen` + 02/`07_dos_donts` | least privilege, human-in-the-loop for irreversible actions, Rule of Two, prefer first-party/verified servers |
| 10 | The Prüfraster | **new** | walk through the checklist they're about to use (see §4) |
| 11 | Exercise briefing | **new** | task, timebox, where the links are, what "done" looks like |

Cut from the main deck: 01's three-kinds ladder, multi-agent frameworks, agentic LLMs, open-weight models, comparison tables (out of scope for this workshop, not just too technical). **Backup slides after the end**: 02/`04_just_another_api` and the full 02/`03_on_the_wire` — the two questions technical attendees most reliably ask ("how is this different from a REST API?", "what's actually exchanged?"); having the real slide beats improvising. Speaker notes from the source slides carry over — they're the best part of the existing material (incident details, Q&A ammunition).

## 4. The Prüfraster (new, one page, the core deliverable)

A printed one-pager participants apply to every server they shortlist. Structure — five question groups, each answerable by a non-technical person from a directory listing, ending in a traffic-light verdict:

1. **Who provides it?** First-party vendor / verified namespace / community-unknown. Is the source public? Actively maintained? (Red flag: name imitating a known vendor — the postmark-mcp pattern.)
2. **What can it do in your name?** Read-only vs. write/send/delete/pay. Anything irreversible? What credentials does it need, and can they be scoped down?
3. **Where does it run, where does the data go?** On your machine / your infrastructure / the provider's cloud. Does sensitive company data leave your control? (The Asana lesson: even honest vendors get multi-tenant isolation wrong — ask.)
4. **Does the combination become dangerous?** The Trifecta check across the *whole workflow*, not just one server: private data + content from outsiders + a channel to the outside. Rule of Two: at most two of the three without a human approval step.
5. **Could you live with the worst case?** If this server were malicious or compromised tomorrow: what's the maximum damage? What logs/approvals would limit it?

Verdict: 🟢 use it / 🟡 use with the named mitigations / 🔴 not in this context — plus one line of reasoning. The dos-and-don'ts table from 02/`07_dos_donts` goes on the back of the page as the "photograph this" summary.

Content sources: 02/`06_security` + `07_dos_donts` notes, 01/`13`+`14` notes, the trust-check row of the existing worksheet. Nothing needs new research; it's a re-formatting job into questions a business user can answer.

## 5. Worksheet v2 (rework of `MCP_workflow_ideation/00_TEMPLATE.md`)

Keep the skeleton, swap the Langflow-specific build sections for the security assessment:

- **Keep**: §1 idea in one sentence, §2 goal + example prompts, §3 "why is this agentic?", §4 MCP server table (with the directory links — add a QR code).
- **Replace §5–8** (Langflow components, flow sketch with MCPTools nodes, setup steps, success test) with: a generic boxes-and-arrows sketch (user → agent → which tools/data), the **Prüfraster verdict per shortlisted server** (reference the one-pager, record verdict + reasoning here), and **"next steps to a pilot"** (who owns it, what data access is needed, what approval is required) — this fulfils the "konkrete nächste Schritte" promise.
- **Keep §9** simplified: expected difficulty + open questions.

Must fit on one A4 sheet (front/back), fillable by pen in 20 minutes.

## 6. The live example (15–25 min slot): decision needed

The 02 demo (weather server + MCP Inspector) is unbuilt and too technical for this audience. Recommendation: **Option A**.

- **Option A (recommended): pre-built Langflow flow, shown live, plus the model worksheet.** Reuse the documented arXiv + mem0 flow from `MCP_workflow_ideation/01_arxiv_markitdown_research.md` — it already exists as a written spec, and it's *deliberately* a good security teaching case: one remote first-party server where your data leaves your machine (mem0) and one community server that runs foreign code on your machine (arXiv). Show: the flow running (2 prompts), then "Refresh Tools" to show tool discovery, then — the key move — **fill in the Prüfraster live for both servers**, out loud, arriving at 🟡 for each with different reasons. That is exactly the exercise they do next, modelled once. Bring a filled worksheet as handout/model answer.
- **Option B: simpler single-server flow** (e.g. a search or weather MCP in Langflow) if the two-server flow feels too heavy or mem0 auth is a hassle. Same structure, less to go wrong, less interesting security contrast.
- **Fallback either way (mandatory)**: screenshots or a 3-min screen recording of the flow running, checked into the repo. Venue Wi-Fi is the usual killer; mem0 also needs a live API key.

## 7. Exercise logistics (25–45)

- Participants work in **pairs** (better discussion, halves the number of presentations).
- Directory browsing on their own phones/laptops via QR codes on the worksheet. **Printed fallback: a curated "server menu"** — one page, ~15 real MCP servers across domains (CRM, e-mail, docs, DB, calendar, industry tools), each with provider, one-line function, and the raw facts needed for the Prüfraster (provider type, local/remote, permissions). This de-risks Wi-Fi, speeds up the exercise, and guarantees the menu contains instructive risk contrasts (include at least one deliberately 🔴-ish entry).
- Facilitators circulate; the model worksheet from the demo is the reference for "what good looks like".

## 8. Discussion block (45–60)

2–3 pairs present (2 min each): the idea, the chosen server(s), and **the traffic-light verdict with reasoning** — the verdict framing keeps presentations short and comparable. Facilitator closes with: common patterns seen, the one-slide summary, and pointers (directory links, this repo / handouts as PDF).

## 9. Build list (ordered)

| # | Artifact | Effort | Notes |
|---|---|---|---|
| 1 | Repo structure: `slides/`, `handouts/`, `demo/` at root | XS | mirror the 02 folder conventions |
| 2 | Prüfraster one-pager (`handouts/pruefraster.md` → PDF) | M | do first — slides 7–10 and the worksheet reference it |
| 3 | Worksheet v2 (`handouts/worksheet.md` → PDF) | S | rework of the existing template |
| 4 | Slide deck (~12 slides, Marp, per §3 map) | M | mostly copy + trim from 01/02; 4 genuinely new/merged slides |
| 5 | Curated server menu handout | M | the only research-heavy item; verify each entry's facts against directories |
| 6 | Langflow demo flow + filled model worksheet + recording/screenshot fallback | M | flow spec already exists; needs mem0 key + Langflow instance + dry run |
| 7 | Facilitator run-of-show (1 page: timings, transitions, discussion prompts) | S | last, once everything else is fixed |
| 8 | Dry run, then trim | — | 15 min of slides is tight; cut on evidence |

## 10. Open decisions

1. **Demo option A or B** (§6) — and which Langflow instance/model endpoint (AISC hub as in the existing spec?).
2. **Print budget**: 3 handouts per pair (worksheet, Prüfraster, server menu) — confirm printing is available at the venue.
3. Whether the final deck needs the **AISC PPTX template** treatment (like parts 01/02) or Marp PDF is enough for this format.
4. Incident freshness: the 2025 cases are solid, but check the speaker notes' "verify before the talk" items (registry size, any 2026 incident worth adding — the notes already mention SmartLoader/Oura, Feb 2026).
