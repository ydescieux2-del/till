# Friction log: building Till for the Alexa+ track

Kept while building, Oct 14 to 22, 2026. Severity: High (blocked or changed the design), Medium (cost real
time), Low (minor).

## 1. Testing against Alexa+ itself
- **Task:** Confirm that Alexa+ picks Till's tools, speaks the right text, and shows the cards.
- **Steps:** Read the track resources and FAQ, then looked for the Alexa+ Category SDK, MCP Toolkit, CLI and Web Simulator.
- **Expected:** Some way to point an Alexa+ test surface at a self-hosted Streamable HTTP MCP server.
- **Actual:** The FAQ says these tools are "select partners only" and that hackathon participants can't get access.
- **Severity:** High.
- **Workaround:** Built a voice web client that is a real MCP client (initialize, tools/list, tools/call over Streamable HTTP), with Web Speech for voice and our own MCP Apps host for the cards.
- **Suggestion:** A public, read-only Alexa+ simulator that accepts a Streamable HTTP URL and shows the chosen tool, the spoken text and the rendered card.

## 2. Which part of a tool result does a voice host speak?
- **Task:** Format tool results so Alexa+ reads a natural answer aloud.
- **Steps:** Searched the track docs and the MCP spec for guidance on spoken output.
- **Expected:** A documented convention, such as a speech field or "the first text block is spoken".
- **Actual:** No guidance. MCP results carry text blocks plus structuredContent, and the spoken part is up to the host.
- **Severity:** Medium.
- **Workaround:** The first text block of every result is one or two sentences written for the ear ("about 16.7 thousand dollars", not "$16,717.31"). The second block has the detail for the model, and the card lives in structuredContent.
- **Suggestion:** Document the convention Alexa+ uses, or support a `_meta` speech hint.

## 3. MCP Python SDK 2.x renamed the server class
- **Task:** Start an MCP server from the common tutorials.
- **Steps:** `from mcp.server.fastmcp import FastMCP` with mcp 2.3.0.
- **Expected:** The import works.
- **Actual:** ModuleNotFoundError. In 2.x the class is `mcp.server.mcpserver.MCPServer`.
- **Severity:** Low (about 10 minutes). The error message links the migration guide, which helped.
- **Workaround:** Read the SDK source for the new API.
- **Suggestion:** Hackathon resources should name the SDK major version they assume.

## 4. Hosting MCP Apps cards ourselves
- **Task:** Render each tool's `ui://till/card.html` in our own web client.
- **Steps:** Server side: `Apps().tool(resource_uri=...)` and `add_html_resource`, which is easy. Host side: looked for a reference host.
- **Expected:** A minimal host example showing the postMessage handshake.
- **Actual:** The host sequence (`ui/initialize` → `ui/notifications/initialized` → `ui/notifications/tool-result`) is only in the extension spec.
- **Severity:** Medium (about 30 minutes).
- **Workaround:** Wrote a 20-line host: a sandboxed iframe with srcdoc, answering initialize and posting the tool result.
- **Suggestion:** Add a one-file reference host to the MCP Apps docs and the hackathon resources.

## 5. Reading the rules automatically
- **Task:** Pull the official rules and FAQ into our notes.
- **Steps:** Fetched the Devpost pages with an automated reader.
- **Expected:** Page text.
- **Actual:** The fetch was blocked.
- **Severity:** Low.
- **Workaround:** Read the pages another way.
- **Suggestion:** Publish the rules as a plain-text or PDF download.

## 6. Our own dependency miss
- **Task:** First run of the server with the Claude pass-through route.
- **Actual:** `httpx` was not installed. Our mistake, not the platform's.
- **Severity:** Low (2 minutes).
- **Workaround:** Added requirements.txt.
