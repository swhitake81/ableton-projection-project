# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is an early-stage project exploring programmatic generation and live control of Ableton Live sessions. The core idea is defining Ableton session structures (channels, device chains, routing, volumes) in a declarative config format (YAML-like or Pkl) and having a program communicate with Ableton Live to render and manipulate sessions in real time.

## Key Concepts

- **No Max for Live** — the goal is to control Ableton without relying on Max for Live
- **Declarative session templates** — define channel chains, device instances, routing, and volumes in config files that can be templatized and reused
- **Live communication** — the program should interface with Ableton Live threads to modify session data in real time (Session View and Arrangement View)
- **Pkl as a candidate config language** — Pkl (Apple's configuration language) is being evaluated as an alternative to YAML for defining session templates, offering typed schemas, constraints, and template inheritance

## Current State

No application code exists yet. The repo contains design notes:

- `WHATIF.md` — initial concept and pseudocode for the declarative session format
- `Notes.md` — research notes on Pkl language features and patterns, and the OSC spec
