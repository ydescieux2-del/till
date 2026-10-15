# Devpost submission draft: Till (Alexa+ track)

Draft for Von. Edit freely. Nothing here has been submitted. Copy rules: no client names, no "Apex",
no banned words, and no dashes in the prose fields.

**Project name:** Till
**Tagline:** A voice CFO for small businesses. Ask about your cash out loud, get the answer in one sentence.
**Track:** Alexa+ (self-hosted MCP server, spec 2025-11-25, Streamable HTTP)
**Side challenge:** Open Source (only if the repo is public; otherwise leave unchecked)
**Built with:** python, mcp (python sdk 2.3.0), mcp-apps, streamable-http, sqlite, starlette, claude, web-speech-api, javascript

## Inspiration
Small business owners don't have a CFO. They have a bank app, a spreadsheet, and a late-night worry about
payroll. The questions are simple. How much do I have? Will I be short next month? Did I get charged twice?
Can I afford to hire? Answering them takes an hour of reconciling. I have spent twenty years building finance and
AI systems for large companies, and I wanted the owner of a bakery to get the same answers by asking out loud.

## What it does
Till is an MCP server with ten tools for a small business owner's money questions. Ask "anything I should worry
about?" and the morning brief gives cash on hand, the tightest week in the next 13, and the charges that need a
look. Say "dispute the flour one" and Till remembers, so tomorrow's brief only shows what is new. Ask "can I afford
a part-time baker at 1,800 a month?" and it re-runs the forecast with the new cost and answers comfortable, tight,
or not yet. Every answer leads with one sentence written to be heard, and every tool also returns a card (through
MCP Apps) with the number, a forecast line against your cash alert, and the details.

## How we built it
The math is deterministic Python with no model in the loop: recurring-bill detection, a 13-week cash forecast,
rule-based checks for duplicate payments, price jumps and large first-time vendors, and an affordability test.
The model's job is to choose and chain tools and to talk. The server uses the MCP Python SDK 2.3.0 over
Streamable HTTP and negotiates protocol 2025-11-25. Every tool is bound to one MCP Apps resource
(ui://till/card.html). Memory (cash alerts, reviewed charges, the last brief) lives in SQLite per business, so it
holds across sessions. Because Alexa+ tools are not open to hackathon builders, we built a voice web client that
is a real MCP client: it sends initialize, tools/list and tools/call over Streamable HTTP, hosts the MCP Apps card in
a sandboxed iframe, and uses Claude to pick and chain tools. With no API key it falls back to a keyword router.

## Challenges
There is no public way to test against Alexa+, so we had to decide what a voice host should speak. Our answer:
the first text block of every result is a sentence written for the ear, so any host can read it as-is.
Writing our own MCP Apps host meant piecing the handshake together from the spec.

## Accomplishments
One spoken sentence like "dispute that flour payment, and can I swing a 2,400 dollar mixer next week?" becomes two
tool calls and a two-sentence answer, with every number traceable to code. The anomaly rules find exactly the four
problems planted in the demo books and nothing else.

## What we learned
Voice changes the output format more than the logic. "$16,717.31" is unreadable aloud; "about 16.7 thousand" is
an answer. Remembering past decisions matters more for voice than for screens, because nobody wants to hear the
same four warnings every morning.

## What's next
Bank feeds instead of CSV, a weekly spoken digest, and multi-location businesses.

## What was built during the submission window
All of Till's code was written for this hackathon, from Oct 14, 2026. It does not include code from any
earlier product.

## Product feedback (required, one per tool)
- **MCP Python SDK 2.3.0.** Used for the server, Streamable HTTP transport, and the MCP Apps extension.
  Worked well: `Apps()` binding a tool to a ui:// resource took three lines, and the server negotiates 2025-11-25.
  Needs work: v1 tutorials break on the FastMCP rename. Would use again: yes.
- **MCP Apps (io.modelcontextprotocol/ui).** Used for the cards. Worked well: one resource serves every tool.
  Needs work: the host-side handshake needs a reference implementation. Would use again: yes.
- **Claude API (claude-haiku-5-5).** Used in the demo client to choose and chain tools. Worked well: it chained
  review_charge and can_i_afford from one sentence and kept answers short. Would use again: yes.
- **Web Speech API (Chrome).** Used for mic input and spoken output in the demo client. Needs work: it only works
  in Chromium browsers. Would use again: yes, for demos.

## Friction log
Attach FRICTION_LOG.md (optional, up to a 10% judging bonus).

## Repo and video
- GitHub: (Von: public with MIT license, or private and shared with the six reviewers listed in the rules
  brief plus the Devpost reviewer address. Invites expire after 7 days, so send them at submission time.)
- Video: public YouTube or Vimeo, under 3 minutes. Script in VIDEO_SCRIPT.md.
