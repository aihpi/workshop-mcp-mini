# Your vetting checklist for any MCP server

<style scoped>
table { font-size: 0.68em; }
p { font-size: 0.85em; }
</style>

*(it's on your table — you'll use it in a few minutes)*

| # | Question group | The incident behind it |
|---|---|---|
| 1 | **Who provides it?** first-party · verified · unknown | postmark-mcp (fake vendor) |
| 2 | **What can it do in your name?** read-only vs. irreversible | GitHub (over-broad token) |
| 3 | **Where does your data go?** local code vs. remote cloud | Asana (vendor cloud bug) |
| 4 | **Does the combination become dangerous?** Trifecta / Rule of Two | GitHub (all three legs) |
| 5 | **Could you live with the worst case?** | all of them |

**→ Verdict: 🟢 use it · 🟡 use with mitigations · 🔴 not in this context**

<!-- Notes:
New slide — walks through 02_handouts/pruefraster.md, which participants apply during the exercise. Two minutes. Hold up the physical handout while talking.
Key framing: every question is answerable from a server's directory page or website — no code reading required. If you CANNOT find the answer (who runs this? is the source public?), that is itself the answer: treat missing information as a red flag.
Walk one question group per breath, always tying back to the incident slide: the checklist is not theory, each question exists because the corresponding thing already happened.
Explain the verdict philosophy: 🟡 is the most common and most useful outcome — "yes, with these mitigations" (read-only key, human approval on send, pinned version). A checklist that only produces yes/no gets ignored; one that produces a mitigation list produces a project plan. 🔴 in this context does not mean the server is bad, it means the combination of your data, this server, and this workflow is not defensible — a different use case may be fine.
Also on the back of the handout: the dos-and-don'ts table (the "photograph this" summary).
-->
