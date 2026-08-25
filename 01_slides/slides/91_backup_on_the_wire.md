<!-- _paginate: false -->

# Backup · What's actually on the wire

<style scoped>
pre { font-size: 0.5em; line-height: 1.35; }
p { font-size: 0.85em; }
</style>

**Discovery: the client asks, every server answers the same way**

```
→  {"method": "tools/list"}
←  {"tools": [{
      "name": "get_forecast",
      "description": "Daily weather forecast for a city. Use for questions
                      about rain, temperature or wind on a specific date.",
      "inputSchema": {"type": "object",
                      "properties": {"city": {"type": "string"},
                                     "date": {"type": "string", "format": "date"}},
                      "required": ["city", "date"]}}, …]}
```

**The call, after the model has picked the tool** *(JSON-RPC envelope trimmed)*

```
→  {"method": "tools/call",
    "params": {"name": "get_forecast", "arguments": {"city": "Potsdam", "date": "2026-08-01"}}}
←  {"content": [{"type": "text", "text": "Sat 2026-08-01, Potsdam: light rain from 14:00, high 19 °C"}]}
```

**Plain JSON-RPC · discovery at runtime · the `description` is a prompt**

<!-- Notes:
Backup slide for "what is actually exchanged?". Copied from workshop-agentic-workflows/02, slide 03.
The entire protocol is a handful of JSON-RPC methods, and these two are the ones that matter. Read the exchange top to bottom once, slowly.
Honesty footnote: every real message also carries "jsonrpc": "2.0" and an id, and responses wrap the payload in "result" — trimmed for legibility.
inputSchema is plain JSON Schema. The host hands name, description, and schema to the model in the model's NATIVE function-calling format (an OpenAI tools array, Anthropic tool blocks, ...). The model never sees MCP itself.
The whole protocol surface is about a dozen methods (tools/list, tools/call, resources/read, prompts/get, ...), all the same shape. Learn these two messages and you have essentially seen the protocol.
As of the 2026-07-28 spec revision, list responses are cacheable and the protocol core is stateless request/response; nothing on this slide changes.
-->
