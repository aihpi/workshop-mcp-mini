# 03 · Security assessment — running the shortlist through the Prüfraster

We apply `02_handouts/pruefraster.md` to the shortlist from `02`. This is the security heart of the demo: the assessment *produces* the server recommendation (not the other way round).

## Candidate A — Official Google Workspace MCP (Gmail + Calendar)

| # | Question | Finding |
|---|---|---|
| 1 | **Who provides it?** | Google itself (verified via Google's own docs, not just a catalog badge). 🟢 |
| 2 | **What can it do in your name?** | Read + **draft** (draft-oriented); verify whether raw `send`/`delete` are exposed. Draft-only = no irreversible action. 🟢/🟡 |
| 3 | **Where does data go?** | Remote — your mail is processed via Google's MCP endpoint under OAuth. You already trust Google with this mailbox, so low marginal exposure. 🟢 |
| 4 | **Dangerous combination?** | Still reads untrusted inbound mail; but draft-only removes the outbound-auto leg → Trifecta not completed by the server itself. 🟢 |
| 5 | **Worst case?** | A malicious inbound mail can still *influence a draft*, but a human reads it before sending. Limited blast radius. 🟢 |

**Verdict: 🟢 / 🟡 — the recommended real-world choice**, provided we confirm scopes and that Langflow can drive its remote OAuth.

## Candidate B — Broad-scope community server (e.g. GongRzhe Gmail)

| # | Question | Finding |
|---|---|---|
| 1 | **Who provides it?** | A community developer. Popular, but read the source / pin the version. 🟡 |
| 2 | **What can it do?** | Read **+ send + delete + modify** — everything, including irreversible actions. 🔴 |
| 3 | **Where does data go?** | Runs locally, but holds a **broad Google OAuth token**; it's third-party code with your rights on the machine. 🟡 |
| 4 | **Dangerous combination?** | Untrusted inbox + private data + **send** = **all three Trifecta legs from one server**. 🔴 |
| 5 | **Worst case?** | A crafted inbound mail makes it exfiltrate an internal mail and delete calendar entries — automatically. 🔴 |

**Verdict: 🔴 as-is** for real use; usable only with heavy mitigations (below). **We keep it in the demo precisely to show the danger.**

## Candidate C — Filesystem MCP for the FAQ

| # | Question | Finding |
|---|---|---|
| 1 | Who? | Official reference server. 🟢 |
| 2 | What can it do? | Read files — **if scoped to `03_demo/faq/` only**. Never grant a home dir. 🟢 (🔴 if over-scoped) |
| 3 | Data? | Local, read-only. 🟢 |
| 4/5 | Combination / worst case? | No outbound, no private personal data, no writes → negligible. 🟢 |

**Verdict: 🟢** — the low-risk foil, and a clean least-privilege lesson (scope = one folder).

## Whole-workflow Trifecta / Rule of Two

The **workflow as a whole** touches all three legs:
- 🔒 **private data** — internal KISZ mails, participant lists, calendar
- 📨 **untrusted content** — the shared inbox (anyone can email it)
- 📤 **channel out** — the ability to send

**Rule of Two:** allow at most two without a human gate. We keep *private data* + *untrusted content* and **remove auto-send**: the third leg (send) sits **behind human approval**. That single decision defuses the injection.

## Mitigations we apply (the "fix")

1. **Draft-only / human-in-the-loop** — the agent may `draft`, never `send`; a person approves and sends. (Native to the official server; enforced by tool-toggle on a community server.)
2. **Least privilege** — no `delete` tool at all (calendar or mail); narrowest scopes; the agent's own throwaway account, not an admin login.
3. **Scope the FAQ server** to `03_demo/faq/` only.
4. **Throwaway account + fake data** for the demo — no real KISZ data on stage.
5. **Logging** — keep a record of tool calls.

## Recommendation (still an open team decision)

- **For a real KISZ deployment:** the **official Google Workspace MCP** (draft-only, scoped, Google-managed) + human approval → **🟡→🟢**.
- **For the workshop's danger reveal:** deliberately use a **broad-scope community server** so `send`/`delete` exist to be abused, then **toggle them off** live to show the fix. See the staging options in `04_build_plan.md`.

**The teaching line:** the assessment didn't just pick a server — it produced a *configuration* (draft-only, no delete, human approval, scoped FAQ). That configuration is the deliverable, and it's what makes an otherwise-🔴 email agent 🟡-acceptable.
