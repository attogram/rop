---
name: task-packet-create
description: >
  Use this when you need to initialize
  a new Packet. It ensures the Packet is fully self-contained and 
  adheres to the AGENTS.md standard.
---

# Skill: Task Packet Create v1.0

This skill ensures that every Packet is a self-contained unit of work that
can be executed by any entity (AI or Human) with zero prior context.

## The Self-Containment Standard

A Packet is considered "Faulty" if the Executor must stop and ask for 
information that should have been provided. To prevent faulty packets, 
every file MUST include:

- Context: The "Why" and "What" of the work.
  - Goal: One clear, actionable sentence.
  - Background: Necessary history or architectural context.
  - Key Files: Absolute paths to every file the Executor must touch or read.
  - Resources: Specific URLs, docs, or environment variables.
- Pre-requisites: List of required tools (bash, jq), access (read/write), and
  capabilities (web search).
- Plan: The exact, sequential steps (1, 2, 3) to complete the work.
- Report Requirements: Precise list of artifacts or data the Executor must
  capture in their Report.

## Rules for the Orchestrator

1. Provide Path Certainty: Never use relative paths like `./src`. Use absolute
   paths based on the project root.
2. Explicit Dependencies: If the packet requires a specific skill (e.g., 
   `skills/prefs-markdown`), you MUST list it in the Context.
3. Proof of Design: Do not create a "Code Change" packet until a "Research"
   or "Design" packet has identified the exact lines of code to be modified.

## Faulty Packet Check

Before finalizing a packet, ask: "If I deleted my entire memory of this task
right now, could I still finish this work using ONLY this file?" If the
answer is No, the packet is incomplete.
