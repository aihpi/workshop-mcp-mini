# New aspects from the colleague's brainstorm files

Reviewed `colleague_files/Informationen_mcp.pdf` + `MCP_Workshop_KMU_mit_Grafikbeschreibungen.pdf` against our slides/handouts. Most content overlaps (N×M, roles, primitives, prompt injection, tool poisoning, rug pulls, GitHub demo, least privilege, HITL, logging, "check your vendor first"). Below is only what we **don't** have. Tick what to adopt.

## Worth serious consideration

- [ ] **"Test safely before adopting" step** — try a new server with a test account and fake data before touching production. Genuinely missing from our Prüfraster; would fit as a mitigation line in question 5 or the dos-and-don'ts. *(KMU p.6/11)*
- [ ] **Three risk tiers for actions** instead of our binary read-only/irreversible: low (search/read/summarise) · elevated (create/change) · high (delete, send external, pay, change rights, execute code). Nice refinement for Prüfraster question 2. *(KMU p.11)*
- [ ] **Staged-autonomy closing message**: LESEN → TESTEN → BEGRENZEN → FREIGEBEN → ÜBERWACHEN — expand agent access gradually, never full autonomy on day one. Strong take-away framing; we currently end without a "how to start Monday" ramp. *(KMU p.12)*
- [ ] **"Does this even need MCP/AI?" prompt** on the use-case canvas ("Gibt es eine einfachere Integration? KI oder Mensch?"). Our worksheet asks "why an agent" but not "why MCP at all". One extra line in worksheet §3. *(KMU p.5)*
- [ ] **Vetting tools table**: MCP-Scan, Cisco AI Agent Security Scanner, Snyk/OSV, OpenSSF Scorecard, sandbox+logging — with the caveat "tools give hints, the company decides". We have nothing on tooling; could be one backup slide or a Prüfraster footer. *(KMU p.7)*
- [ ] **Shadow MCP servers + inventory/governance**: unapproved servers running outside inventory, review and logging; keep an MCP inventory, re-approve on updates/scope changes. Our checklist is per-server; the organizational layer (who keeps the list, who approves) is new. Could be one line in "next steps to a pilot". *(Informationen, Risiko-Tabelle + Security-Checkliste)*
- [ ] **Motivation hook**: open a plain chat, ask "book me a meeting Wednesday 1pm" → "no access" — then introduce MCP as the fix. Cheap, effective 30-second opener for slide 1 or the demo. *(Informationen, notes; KMU p.1 "Vom Chat zur Aktion")*

## Maybe (backup slides / speaker notes)

- [ ] **Two separate exercises** instead of our one: (1) use-case canvas, (2) security canvas — mark attack points (INPUT/DATEN/TOOLS/RECHTE/FREIGABE/SERVER) directly on your own workflow sketch. Alternative structure; the "mark risks on your own sketch" move could enrich our worksheet §5/§6 without splitting the exercise. *(KMU p.5+10)*
- [ ] **Build-your-own vs. use-existing decision table** (proprietary system, special compliance → build; else use). One backup slide for the inevitable "our software has no server" question. *(KMU p.8)*
- [ ] **Command injection / RCE risk class** (unvalidated tool parameters reaching shell/processes; OX Security analysis on stdio risks) and **secret exposure** as named classes. Technical; ours subsumes them under "foreign code with your rights". Speaker-note ammunition at most. *(Informationen)*
- [ ] **Memory/context poisoning** — injected instructions persisting in agent memory and steering later decisions. Relevant since our demo features a memory server (mem0); one sentence in the demo's checklist assessment would land well. *(Informationen)*
- [ ] **Layer-wise attack table** (host/client/server each with typical attacks, e.g. confused deputy) + academic reference *"MCP: Landscape, Security Threats, and Future Research Directions"*. Q&A depth only. *(Informationen)*

## Skip (out of scope for this audience/format)

- Builder-side security guidance (TLS, OAuth 2.1 flows, origin checks/DNS rebinding, rate limiting, input validation, timeouts, retries) — for people *operating* servers, not selecting them.
- Protocol extras: Roots, Sampling, Elicitation, composability/MCP-Bridge — too deep; sampling is also deprecated in the 2026-07-28 spec.
- Business-benefits framing (efficiency/scalability/data sovereignty) — covered implicitly; "Datensouveränität" is a nice word to use verbally.
