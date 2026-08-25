# ⚠️ Security: whom are you trusting?

**A connected server acts with the permissions you gave it — its code, your credentials, your name.**

- **Prompt injection:** the model cannot reliably tell *your* instructions from instructions **hidden in text it reads** — an email, a web page, a tool description *(OWASP LLM01)*
- **The Lethal Trifecta** *(Willison)* — an agent that combines all three can be made to leak:

| 🔒 private data | 📨 content from outsiders | 📤 a channel out |
|---|---|---|
| customer records, mail, internal docs | inbound email, web pages, tickets | can send / post / publish |

<!-- Notes:
Merged from the MCP deck's security slide and the overview deck's security slide (sources: workshop-agentic-workflows/02 slide 06, 01 slides_en 13). Two minutes on the mechanics; the incidents get their own slide next.
The root cause in one sentence, worth saying twice: an LLM cannot reliably distinguish whether an instruction comes from the user or is hidden in the text it is reading — for the model both are the same stream of text. This is why prompt injection is not a bug that gets patched away: OpenAI conceded in Dec 2025 the problem is "probably never fully solvable"; the UK's NCSC says the same. Protection comes from architecture — limiting what a hijacked agent CAN do — which is two slides ahead. (simonwillison.net/2025/Jun/16/the-lethal-trifecta/ · techcrunch.com/2025/12/22/openai-says-ai-browsers-may-always-be-vulnerable-to-prompt-injection-attacks/)
Connect to the previous slide: tool descriptions and tool results are exactly such foreign text. Two named attack patterns to mention because they return in the exercise's checklist: tool poisoning (malicious instructions hidden inside a tool description — invisible in many client UIs) and the rug pull (a server changes its descriptions AFTER you approved it — which is why updates need reviewing).
The Trifecta with the email-triage example from slide 02: it reads inbound customer mail (outsider content) and queries the order database (private data) — so the third leg, sending, stays behind a human click. That was not a UX choice, it was the security architecture.
Broader agent incidents if asked (from the overview deck's notes): EchoLeak (June 2025, CVE-2025-32711 — a zero-click email exfiltrates data via M365 Copilot), the Replit agent deleting a live production database during an explicit code freeze (July 2025, OWASP "Excessive Agency"). The next slide narrows to MCP-specific cases.
-->
