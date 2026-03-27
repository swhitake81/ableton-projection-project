---
name: Research action items — protocol investigation
description: Concrete next steps user was given for investigating Ableton communication protocols before any further design work.
type: project
---

User's next research task (as of 2026-03-15):

1. **Read Sonic Pi source code** — find the module (Ruby/Erlang layer) that constructs outbound OSC messages to external apps. Note exact host, port, path, arguments.
2. **Identify Ableton's listener** — what receives those OSC messages on Ableton's side? A Remote Script? Max for Live device? Third-party bridge (e.g., AbletonOSC)?
3. **Map the boundaries** — with Ableton + Sonic Pi + an OSC monitor running, try ~10+ different operations (play note, arm track, change send level, add device, record, etc.) and document what works, what silently fails, what errors. This "wall map" defines product scope.

**Why:** No config language or architecture decisions should be made until the communication constraints are understood empirically.
**How to apply:** When user returns with findings, use them to guide which of the three sub-problems (template engine, live control, declarative programming) to tackle first.
