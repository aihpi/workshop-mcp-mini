# 🛡️ Contain the damage instead of hoping

- **Least privilege** — the agent gets its **own account**, minimal scopes, short-lived keys — never your admin login
- **Human in the loop** — a person approves everything **irreversible**: send, delete, pay, publish
- **Rule of Two** *(Meta)* — per agent, at most **2 of the 3** Trifecta properties; the third only behind an approval
- **Trust the source** — prefer first-party/verified servers · treat server updates like software updates
- **Keep logs** — when something goes wrong, you want to know what the agent did

**Mindset: assume the agent *can* be hijacked — and make sure that's survivable.**

<!-- Notes:
Merged from the overview deck's hardening slide and the MCP deck's dos-and-don'ts (sources: workshop-agentic-workflows/01 slides_en 14, 02 slide 07). Two minutes. This slide is the bridge into the checklist: every bullet reappears there as a question.
Rule of Two, spelled out (Meta, Oct 2025; Simon Willison calls it "the best practical advice for secure agent systems today"): if the agent reads outsider content AND sees private data, it must not be able to communicate out; if it must communicate out, it doesn't get private data; and so on. Immediately applicable by non-technical people — it is question 4 on the checklist. (ai.meta.com/blog/practical-ai-agent-security/)
For German organizations, the authoritative anchor: BSI and France's ANSSI jointly published Zero Trust design principles for LLM-based systems (Aug 2025) and explicitly reject full autonomy for sensitive use cases. If you need a government reference for internal discussions, that is it. EU AI Act transparency obligations (Art. 50) apply from 2 Aug 2026.
Why "contain instead of hope", one number for discussions: even the most robust models fall for single prompt-injection attempts in a low-single-digit percent of cases on public benchmarks — and attackers get unlimited attempts. Model robustness is a seatbelt, not a guarantee; the architecture limits the crash.
Practical translation for a company without a security team (from the overview deck's notes): (1) own account, minimal rights; (2) API keys with expiry and smallest scope; (3) irreversible actions behind human approval; (4) if a server runs locally, run it isolated where possible; (5) keep the logs.
Also worth one sentence, from the dos-and-don'ts: curate FEW well-described tools per use case. Dozens of tools in one session make the model pick wrong — a quality argument that happens to also shrink the attack surface.
-->
