---
name: Refined project vision and architecture direction
description: User's clarified vision — middleware layer between IDE, Sonic Pi, and Ableton. Key architectural insights from early design discussion.
type: project
---

User's vision is a **middleware layer** that sits between an IDE (live coding interface), a live music engine (Sonic Pi or similar), and Ableton Live. Pkl was initially considered as a translation lingua franca between all three.

Key architectural realization: this is a **real-time communication/message-passing problem with config features**, NOT a config problem with real-time features. The config layer (Pkl or otherwise) is downstream of the communication protocol design.

Three distinct sub-problems identified:
1. **Template engine** — scaffolding Ableton sessions from config
2. **Live control layer** — talking to Ableton in real time, mutating state
3. **Declarative music programming** — describing musical intent in code

User wants all three eventually but needs to start with understanding the communication layer first.

**Why:** The protocol constraints (what Ableton can actually receive and respond to) define the entire product scope. Language/config choices come after.
**How to apply:** Always ground suggestions in the realities of Ableton's external interfaces (MIDI, OSC, Remote Scripts, Max for Live, community bridges like AbletonOSC). Push toward specifics over abstractions.
