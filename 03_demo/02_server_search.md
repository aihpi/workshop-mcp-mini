# 02 · Server search — our real walkthrough

We need three capabilities: **email (read + draft)**, **calendar (availability)**, and a **read-only FAQ source**. Here is the actual search, the candidates, and the friction we hit. It ends with a **shortlist, not a final pick** — the pick comes out of `03_security_assessment.md`. Priority per the team: a *genuinely* official Google server if one exists.

> ⚠️ Fast-moving area — **verify every name, transport and scope before building**. Facts below checked Sept 2026.

## Where we searched

`registry.modelcontextprotocol.io` · `github.com/mcp` · `pulsemcp.com` · `mcpservers.org` · `glama.ai` · `mcpsafe.org` — plus a plain web search, which is what surfaced the official Google option.

## What "official" turned out to mean (the first trap)

Searching directories for "gmail", one listing (`pulsemcp.com/servers/google-workspace-gmail`) is badged **"official"** — but PulseMCP's own note says they are *"temporarily managing this server.json until the maintainer publishes it,"* the maintainer shows as a `com.pulsemcp.mirror/...` org, and the URL is truncated. **That badge is a directory placeholder, not proof Google published it.** Lesson for the room: "official" on a catalog is a claim to verify, not a fact — this is exactly the postmark-mcp pattern (imitating a trusted name).

## The genuinely official option (found via Google's own docs)

Google **does** now publish Google-managed Workspace MCP servers (announced at Google Cloud Next '26): Gmail, Calendar, Drive, People, Chat.
- **Docs:** `developers.google.com/workspace/guides/configure-mcp-servers` and `developers.google.com/workspace/calendar/api/guides/configure-mcp-server`; Calendar reference at `calendarmcp.googleapis.com`.
- **Transport:** remote (Google-hosted), **OAuth**. No local code, no token file to babysit.
- **Capabilities (as documented):** read (search emails, list events) and **action via drafts** (create *draft* emails, schedule meetings). Notably draft-oriented — see the tension in `03`.
- **Verify before building:** exact tool names, whether raw `send`/`delete` are exposed, and — critically — **whether Langflow can complete its OAuth handshake** to a remote Google MCP server.

## Candidates by capability

| Capability | Candidate | Provider | Transport | Auth / cost | Notes |
|---|---|---|---|---|---|
| Gmail + Calendar | **Official Google Workspace MCP** | Google (official) | Remote HTTP | OAuth · free | Draft-oriented, scoped, Google-managed. **Priority pick.** |
| Gmail + Calendar (+Drive) | taylorwilsdon/google_workspace_mcp, aaronsb/google-workspace-mcp | Community | Local (stdio) | OAuth (local token) · free | One server for several APIs; broad scope = least-privilege talking point |
| Gmail only | **GongRzhe/Gmail-MCP-Server** | Community | Local (stdio) | OAuth (local) · free | Broad scope: read **+ send + delete**. The cautionary example / danger demo |
| Calendar only | nspady/google-calendar-mcp | Community | Local (stdio) | OAuth (local) · free | Full toolset incl. `delete-event`; note the `...-no-calendar-deletion` variants that drop delete on purpose |
| FAQ (knowledge) | **filesystem MCP** (reference server) | modelcontextprotocol (official ref) | Local (stdio) | none · free | Read-only, scoped to one folder (`03_demo/faq/`). The simplest, lowest-risk server |

## Friction & open questions we hit (the honest log)

1. **"Official" is ambiguous** across catalogs — only Google's own docs settle it. Budget time to verify provenance.
2. **Remote-official vs local-community is a real trade-off**, and it's not "remote = safe": the official remote server is scoped and Google-managed (good), *but* your mail flows through Google's MCP endpoint and Langflow must handle a **remote OAuth flow** (unverified). The local community servers avoid remote OAuth but run **third-party code with a broad Google token** on the machine, and need **Node/npx in Langflow's environment**.
3. **Draft-only official vs send-capable community** changes the demo: the official server may not expose `send`/`delete`, so the dramatic exfil/tamper reveal needs the broad-scope community server. Carried into `03`/`04` as a decision, not silently resolved.
4. **Google OAuth setup** (Cloud project, consent screen, test user, scopes) applies to *any* Google option and is the real setup cost — see `04_build_plan.md`.
5. **FAQ server scope**: the filesystem MCP will happily expose whatever directory you grant — must be pointed at `03_demo/faq/` only, never a home dir.

## Shortlist into `03`

- **Email/Calendar:** official Google Workspace MCP (priority) **vs** a broad-scope community server (GongRzhe / a workspace server) for the danger demo.
- **FAQ:** filesystem MCP (read-only, folder-scoped).

Sources: [Google: configure Workspace MCP servers](https://developers.google.com/workspace/guides/configure-mcp-servers) · [Google Calendar MCP guide](https://developers.google.com/workspace/calendar/api/guides/configure-mcp-server) · [Google Cloud: managed MCP servers for everyone](https://cloud.google.com/blog/products/ai-machine-learning/google-managed-mcp-servers-are-available-for-everyone) · [GongRzhe/Gmail-MCP-Server](https://github.com/GongRzhe/Gmail-MCP-Server) · [nspady/google-calendar-mcp](https://github.com/nspady/google-calendar-mcp) · [PulseMCP "official" listing](https://www.pulsemcp.com/servers/google-workspace-gmail)
