# 01 · Use case — the KISZ inbox assistant (worked worksheet)

This is our own worked answer to `02_handouts/worksheet.md` — the model the participants compare against. We deliberately walk the same steps they will.

## Broad idea → narrowing

- **Broad:** "We get too much email. Can AI help?"
- **Narrow once:** the KISZ shared inbox (`info@` / the address on hpi.de/kisz) is always behind — the same kinds of mail arrive daily.
- **Narrow again (the task):** *an assistant that reads each new mail and **drafts a reply** — answering general questions from our FAQ, and for booking requests proposing a free slot from our calendar. A human just checks and sends.*

## Goal & example prompts

- **Goal:** cut the time-to-first-draft for routine inbox mail to near zero, without anyone typing boilerplate — while a human stays in control of what actually goes out.
- **Example requests we'd type to the agent:**
  1. *"Sichte die neuen E-Mails, beantworte Fragen anhand der FAQ, prüfe für Terminanfragen die Verfügbarkeit im Kalender und entwirf passende Antworten."*
  2. *"Fasse die neuen Anfragen kurz zusammen und markiere, was ich selbst beantworten muss."*
  3. *"Entwirf eine Antwort auf die letzte Terminanfrage mit zwei Terminvorschlägen nächste Woche."*

## Why does this need an *agent*? (not a fixed chain)

The model **routes and decides** per mail:
- Is this a **question** (→ look it up in the FAQ), a **booking request** (→ check the calendar, pick a free slot), or **something else** (→ escalate to a human, draft nothing)?
- Which slot to offer, and what alternative if the first is taken?

A fixed script can't make those branches; that decision is the "agentic" part.

## DATA / SYSTEMS / ACTIONS / AI-or-HUMAN

| Field | For this use case |
|---|---|
| **Goal** | Fast, good reply drafts for routine mail in the shared inbox |
| **Data** | Incoming mail (from strangers!), internal mail/attachments, FAQ content, calendar entries |
| **Systems** | Email (Gmail), calendar (Google Calendar), FAQ knowledge source |
| **Actions** | **Read** (mail, calendar, FAQ) · **Draft** a reply · *(not automatic: send, delete)* |
| **AI or human?** | AI drafts & proposes · **human approves and sends** (anything irreversible) |
| **Why MCP?** | Connect three existing systems (mail, calendar, FAQ) to one agent, without custom development |
| **Simpler solution possible?** | Pure auto-reply would be a chain — but routing (question vs. booking vs. escalate) needs the AI decision |

## The security twist (foreshadowing `03`)

A shared inbox is **untrusted input by definition** — anyone can email it, including an attacker. Combine that with private KISZ data and an outbound channel and you have the full Lethal Trifecta. That's why this pleasant little helper is also the perfect security teaching case — see `03_security_assessment.md`.
