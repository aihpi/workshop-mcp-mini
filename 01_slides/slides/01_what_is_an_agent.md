# What is an agent?

![w:430](../img/llm_allein.svg) ![w:430](../img/agent_schleife.svg)

> *"An LLM agent **runs tools in a loop** to achieve a goal."* — Simon Willison

**The model asks for an action · the software executes it · the result flows back · repeat until done**

<!-- Notes:
Merged from the overview deck's "from LLM to agent" + "what is an agent" (source: workshop-agentic-workflows/01, slides_en 02+03). Two minutes.
Left image: an LLM on its own can only produce text. No tools (ask it to send an email, it can only draft one), no access to your data or anything after its training cutoff, no memory between calls. Everything beyond that comes from the software AROUND the model, not from the model.
Right image: give it tools (send_email, query_database, search_web) and a loop: the model requests an action, the surrounding software executes it, the result flows back, the model decides the next step, until the goal is reached. That loop is the whole trick.
Note for the audience: ChatGPT and Claude as apps have long since stopped being bare LLMs — web search is a tool, chat history is memory. You have all used an agent already.
The one-sentence definition to anchor: tools in a loop, to achieve a goal. Everything about MCP today is about the word "tools" in that sentence: where do they come from, how does the model reach them, and whose tools do you dare hand it.
-->
