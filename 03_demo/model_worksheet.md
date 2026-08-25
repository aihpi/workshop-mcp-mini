# Model Worksheet — Personalized Research Assistant (filled example)

> This is the worked example shown in the live demo, filled into the same worksheet the participants use. Print a few copies as the "what good looks like" reference during the exercise. (Adapted from the earlier ideation sheet for the arXiv + mem0 flow.)

## 1. The idea, in one sentence

A research assistant that **remembers who I am and what I work on**, then **finds and summarises recent papers** tailored to those interests.

## 2. Goal & example prompts

- **Goal:** personalised (not generic) literature monitoring, without re-explaining my interests every time.
- **Example requests:**
  1. *"I'm an AI engineer at the AI Service Center, interested in reinforcement learning for control."* (the agent stores the profile)
  2. *"Show me notable papers on RL in control from the past month and summarise them."* (the agent recalls the profile, searches, summarises)

## 3. Why does this need an agent?

The model runs a multi-step plan and picks tools as needed: recall my profile → resolve "past month" to real dates → search papers → read the promising ones → rank & summarise → optionally store a new preference. Nothing is hardcoded; it decides which of ~25 available tools to call and when it has enough to answer.

## 4. The MCP servers

| Field | Server 1: **mem0** (memory) | Server 2: **arXiv** (research) |
|---|---|---|
| Name / provider | mem0.ai — first-party hosted | community (individual author) |
| What it does | store/search my long-term profile | search, read, analyse arXiv papers |
| Runs | ☑ remote | ☑ local |
| Auth & cost | API key, free tier | none, free |
| Tools it offers | add_memory, search_memories, … (11) | search_papers, read_paper, … (14) |

## 5. Sketch the workflow

```
Me ──► Agent ──► answer
        ▲ tools
        ├── mem0   (remote: my profile)          ← private-ish data
        ├── arXiv  (local: paper search/read)    ← content from OUTSIDERS (paper text!)
        └── current date
Leaves the company: my interest profile → mem0's cloud. Nothing else goes out.
```

## 6. Security assessment

| Server | Verdict | Reasoning / required mitigations |
|---|---|---|
| mem0 | 🟡 | First-party and authenticated — but my profile data lives in the provider's cloud. OK for research interests; would be 🔴 for customer data. Mitigation: store nothing sensitive, use a dedicated account. |
| arXiv | 🟡 | Free and useful — but an unknown author's code running locally with my rights. Mitigations: pin the version, glance at the source, or run it isolated. Paper text is outsider content entering the model. |

**Trifecta check:** private data ☑ (my profile) · outside content ☑ (paper text) · channel out ☐ (the agent can't send/post anything) → **two of three: acceptable without an approval step.** The moment we add an email tool, this needs a human approval.

## 7. Next steps to a pilot

1. **Owner:** me.
2. **Access needed:** a mem0 account (self-service); arXiv is open.
3. **Approval:** none for public papers + my own profile; revisit if colleagues' data enters the memory.

## 8. Expected difficulty & open questions

- **Difficulty:** ⭐⭐⭐ — two servers plus memory working together.
- **Open questions:** memory quality over months; "notable" is hard to judge for very recent papers (citations lag — the agent should say so).
