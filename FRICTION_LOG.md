# Friction log: building Till for the Alexa+ track

Kept while building, Oct 14 to 22, 2026. Each entry: what happened, the cost, and a suggestion.

## 1. The Alexa+ developer tools are gated
**What happened:** The track points to Alexa+ but the Category SDK, MCP Toolkit, CLI and Web Simulator are
"select partners only" (FAQ). There is no way to test against a real Alexa+ surface.
**Cost:** We had to design for a generic MCP host and write our own voice web client to stand in for the device.
We can't confirm how Alexa+ will render MCP Apps cards or how it will read our spoken text.
**Suggestion:** A public Alexa+ simulator, even read-only, that takes a Streamable HTTP URL would let hackathon
builders confirm tool selection, speech output and card rendering.

## 2. No guidance on how Alexa+ uses tool output for speech
**What happened:** MCP tool results are text plus structured content, and nothing says which part Alexa+ speaks.
**Cost:** We guessed: the first text block is a sentence written for the ear ("16.7 thousand dollars", not
"$16,717.31"), followed by detail for the model, plus a card in structuredContent.
**Suggestion:** Document a convention, for example a `_meta` speech hint or "first text block is spoken".

## 3. MCP Python SDK 2.x renamed the server class
**What happened:** `from mcp.server.fastmcp import FastMCP`, used in most tutorials, now raises
ModuleNotFoundError in mcp 2.x (it is `mcp.server.mcpserver.MCPServer`).
**Cost:** About 10 minutes. The error message links the migration guide, which helped.
**Suggestion:** Hackathon resources could name the SDK version they assume.

## 4. MCP Apps host handshake is spread across documents
**What happened:** To host our own card iframe we needed the `ui/initialize` →
`ui/notifications/initialized` → `ui/notifications/tool-result` sequence. The server-side Apps API is
documented in the SDK, but the host side is only in the ext-apps spec.
**Cost:** About 30 minutes of reading to write a roughly 20-line host.
**Suggestion:** Add a minimal reference host (one HTML file) to the resources page.

## 5. The rules pages could not be fetched by automated readers
**What happened:** The Devpost pages for the hackathon blocked our research tool's fetch, so we read the rules
another way.
**Cost:** Small.
**Suggestion:** A plain-text or PDF copy of the official rules.

## 6. `httpx` was not installed by default for our proxy
**What happened:** Our Claude pass-through route imported httpx and failed on first run.
**Cost:** About 2 minutes. This one was our own mistake, so we added requirements.txt.
