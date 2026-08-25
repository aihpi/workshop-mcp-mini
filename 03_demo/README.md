# Live demo (workshop minutes 15–25)

One pre-built Langflow flow, shown running — then its security assessment done **out loud** with the vetting checklist. The demo deliberately models the exercise the participants do right afterwards; [model_worksheet.md](model_worksheet.md) is the same example on paper.

## The flow

The personalised research assistant: an agent with **two MCP servers** that contrast instructively — one remote first-party (your data leaves the machine) and one local community server (foreign code runs on your machine).

```
Chat Input ─────────────► Agent ─────────► Chat Output
LLM (AISC hub / LiteLLM) ─► Agent
                            ▲ tools
                            ├── MCP: mem0   (remote, Streamable HTTP — user profile memory)
                            ├── MCP: arXiv  (local stdio via uvx — paper search)
                            └── Current Date
```

## One-time setup

1. **Langflow** running (with `uv` installed where Langflow runs, for the stdio server).
2. **mem0 (remote):** API key from app.mem0.ai (free tier). Langflow → Settings → MCP Servers: Streamable HTTP, URL `https://mcp.mem0.ai/mcp`, header `Authorization: Bearer <KEY>`. Then **Refresh Tools** on the node.
3. **arXiv (local stdio):** `command: uvx`, `args: ["arxiv-mcp-server"]` — pin a version. **Refresh Tools** should list ~14 tools.
4. Agent system prompt pins `user_id = workshop_demo_user` for mem0 (store and recall must use the same id, or recall comes back empty).
5. Tool Mode on for both MCP nodes; wire both toolsets + Current Date into the Agent.

## Run of show (10 min)

1. **(2 min)** Show the flow canvas. Point at the two MCP nodes: "these are plugs, not code we wrote." Click **Refresh Tools** on one — the tool list appearing live IS the `tools/list` discovery from the slides.
2. **(3 min)** Run the two prompts from the model worksheet (store profile → ask for papers). Let the tool calls scroll past; narrate which server each call goes to.
3. **(5 min)** The actual point: put the **vetting checklist** under the doc camera (or on a slide) and assess both servers out loud, arriving at 🟡 for each **for different reasons** (mem0: data leaves; arXiv: foreign code runs locally). End on the Trifecta check: "no channel out — the day we give this agent email, we add a human approval."

## Fallbacks (prepare both before the dry run)

- **Recording:** screen recording of steps 1–2 → `fallback/` (plays if Langflow or the venue Wi-Fi dies). Step 3 needs no technology — the checklist works on paper.
- **Screenshots:** flow canvas, tool list after refresh, one answer with visible tool calls → `fallback/`.

## Still to do (needs a live Langflow instance)

- [ ] Build the flow, export the flow JSON into this folder
- [ ] mem0 key for the workshop account (do not demo with a personal key)
- [ ] Record the fallback material
- [ ] Test the AISC-hub model actually tool-calls reliably (10 representative requests)
