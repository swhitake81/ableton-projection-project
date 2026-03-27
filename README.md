# ableton-projection-project

> What if you could generate and control Ableton Live sessions programmatically — without Max for Live?

This is an active research project exploring that question. No application code exists yet. What's here is design thinking, pseudocode, and research notes on the tools and protocols that could make it work.

## The Idea

Define an Ableton Live session — channels, device chains, routing, volumes — in a declarative config format. Have a program read that config and communicate with Ableton Live in real time to render and manipulate the session, both in Session View and Arrangement View.

The deliberate constraint: **no Max for Live**. The goal is to control Ableton through its exposed interfaces without requiring an M4L license or patching environment.... MAYBE.

## How It Might Work

Two distinct capabilities are being explored:

**Session generation (offline)** — using Ableton's official C++ export library to write `.als` files programmatically. Useful for scaffolding reusable beat templates from a config file.

**Live control (real-time)** — using [AbletonOSC](https://github.com/ideoforms/AbletonOSC), a community remote script that exposes Ableton's Live API over OSC without Max for Live. Sonic Pi (or another live coding environment) sends OSC messages to control the session in real time.

**Config language** — [Pkl](https://pkl-lang.org) is being evaluated as the format for defining session templates. It offers typed schemas, constraints, and template inheritance — making it a stronger candidate than raw YAML for something that needs to be both human-readable and structurally enforced.

## Repo Structure

| File        | Purpose                                                                                                                                                    |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `WHATIF.md` | Original concept, pseudocode for the declarative session format, OSC research, and key resources                                                           |
| `Notes.md`  | Working research notes on Pkl and OSC as they're being learned                                                                                             |
| `CLAUDE.md` | Context file for Claude Code — provides project background so AI-assisted sessions stay on track                                                           |
| `.claude/`  | Claude Code's local memory for this project — stores context between sessions. Can be safely ignored or added to `.gitignore` if you don't use Claude Code |

## Status

Early research. The design is still being validated. Contributions, questions, and ideas are welcome.
