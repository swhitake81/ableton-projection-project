---
name: Two-pronged architecture emerging
description: Project likely needs both static .als generation (via ableton export lib) and live OSC control (via M4L or remote script)
type: project
---

Two architectural approaches are emerging for the project:

1. **Static generation** — Ableton's export library (ableton.github.io/export/) can write .als files programmatically from templates
2. **Live control** — Real-time manipulation needs OSC/MIDI bridge; M4L Connection Kit or AbletonOSC (community remote script) are candidates

**Why:** The export library only writes files, it can't talk to a running Ableton instance. Live control requires a separate mechanism.

**How to apply:** When discussing implementation, keep these as distinct concerns. The user is still researching which live control approach to use — don't assume M4L is chosen yet, as the "No Max for Live" goal is still a preference.
