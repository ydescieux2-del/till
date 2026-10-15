# Demo video script (target 2:40, hard limit under 3:00)

Record the screen at 1920x1080 in Chrome with QuickTime (File > New Screen Recording). Speak the questions into
the mic so the judges hear real voice in and voice out. Before recording, reset the demo memory so the counts
match this script:

    cd ~/alexa-faos-mcp && rm -f data/till_state.db && source ~/.secrets && .venv/bin/python -m till.server

Then open http://127.0.0.1:8765/ in Chrome and allow the microphone.

No Alexa or Amazon logos in the video. Say "built for the Alexa+ track" in the narration only. No music, or use
royalty-free music only.

| Time | On screen | Von says (voiceover) or asks (into the mic) |
|---|---|---|
| 0:00 to 0:15 | Demo page, idle | VO: "Small business owners don't have a CFO. They have a bank app and a worry about payroll. This is Till, a voice CFO, built as an MCP server for the Alexa+ track." |
| 0:15 to 0:40 | Tap mic | ASK: "Morning. Anything I should worry about?" Let Till answer and the brief card render. |
| 0:40 to 1:00 | Point at the card | VO: "Every number comes from code, not the model. Here's cash on hand, the 13-week forecast line against my alert, and four charges that need a look." |
| 1:00 to 1:20 | Tap mic | ASK: "What are the weird charges?" |
| 1:20 to 1:45 | Tap mic | ASK: "That duplicate flour payment, I'm going to dispute it. And can I swing a 2,400 dollar mixer next week?" Point at the two tool calls in the trace. VO: "One sentence, two tools, chained by the agent." |
| 1:45 to 2:05 | Tap mic | ASK: "Can I afford a part-time baker at 1,800 a month?" Card shows "Yes, but it gets tight." |
| 2:05 to 2:25 | Reload the page (new session), tap mic | ASK: "Give me my morning brief." VO: "New session. Till remembered the dispute, so now it's three charges, not four." |
| 2:25 to 2:40 | Terminal: run tests/test_protocol.py, show ALL PROTOCOL CHECKS PASSED | VO: "Spec 2025-11-25 over Streamable HTTP, ten tools, MCP Apps cards, open source. Till." |

Upload to YouTube as Public (or Unlisted only if the rules allow it; they say public), in English, titled
"Till: a voice CFO for small businesses (Alexa+ track)".
