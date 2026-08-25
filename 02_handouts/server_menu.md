# Server Menu — 15 MCP servers to browse offline

> Use this if you'd rather not search the directories (or the Wi-Fi is down). Facts compiled Aug 2026 from the public directory listings — **⚠️ organizers: re-verify every row against the listing before printing.** The last column is deliberately *not* a verdict — that's your job, with the vetting checklist.

| # | Server | What it does | Provider | Runs | Needs | Worth noticing when vetting |
|---|---|---|---|---|---|---|
| 1 | **GitHub** | read/manage repos, issues, PRs | first-party (GitHub) | remote or local | OAuth / access token | token scope decides everything — a broad token was the core of the May 2025 demo attack |
| 2 | **Atlassian** (Jira/Confluence) | search & edit tickets, pages | first-party | remote | OAuth | write access to your project tracker = acts in your name toward colleagues |
| 3 | **Notion** | read/write workspace pages, databases | first-party | remote | OAuth | your internal docs flow through the vendor's cloud endpoint |
| 4 | **Asana** | tasks, projects | first-party | remote | OAuth | the vendor whose own MCP server had the 2025 cross-tenant leak — ask what changed |
| 5 | **HubSpot** | CRM: contacts, deals, notes | first-party | remote | OAuth | customer personal data — GDPR: where is it processed? |
| 6 | **Stripe** | payments: customers, invoices, refunds | first-party | remote or local | API key | money moves = irreversible; restricted keys exist — use them |
| 7 | **Microsoft Learn Docs** | search Microsoft documentation | first-party | remote | none | read-only, public data, no account — what "low stakes" looks like |
| 8 | **Filesystem** (reference server) | read/write files on the machine | open source, maintained with the MCP spec | local | directory allow-list | it sees whatever folder you grant — grant narrowly |
| 9 | **Fetch** (reference server) | fetch a web page into the agent's context | open source, reference | local | none | every fetched page is **outsider content** entering the model — one Trifecta leg by design |
| 10 | **Memory** (reference server) | persistent notes/knowledge graph for the agent | open source, reference | local | none | stored locally; what accumulates in there over months? |
| 11 | **PostgreSQL** (community connectors) | query your database | community (several) | local | DB credentials | give it a **read-only** DB user; check which connector you actually installed |
| 12 | **Tavily** (web search) | web search for agents | first-party (Tavily) | remote | API key (free tier) | search results are outsider content; queries reveal what you're working on |
| 13 | **mem0** | long-term user memory as a service | first-party (mem0.ai) | remote | API key (free tier) | convenient — and your users' profile data lives in a US startup's cloud |
| 14 | **arXiv** (community) | search/read research papers | community (individual author) | local | none | useful and free — but it's an unknown author's code running with your user's rights; pin the version |
| 15 | **WhatsApp** (community) | read/send personal WhatsApp messages | community, unofficial API | local | your WhatsApp session | private messages + can send as you + unofficial API against ToS — a rich checklist exercise |

**Directories for live browsing:** registry.modelcontextprotocol.io · github.com/mcp · pulsemcp.com · mcpservers.org · mcpsafe.org
