---
name: task-status-update
description: >
    Use this when you need to draft a concise status update for a task.
    Generates a well-formatted report, ready for copy-pasting.
---

# Skill: Task Status Update v3.9
This skill drafts a clear, concise, and effective status update for a task.
The final output MUST be provided as plain Markdown text
to ensure easy copy-pasteability.

## Guiding Principles
- Target Audience: Design the update for a busy Project Manager skimming
  Jira tickets to grasp the exact status of the task instantly.
- Task-Level Context: Update must summarize progress on the entire task.
- Complete Scope: List every single packet to show the full picture,
  regardless of whether it has started or not.
- High Signal: Omit conversational filler, decorative spacers, and emojis.
- Report, Don't Direct: Do not give commands to the user.
- No Markdown Hyperlinks: Do not hide URLs inside markdown syntax.
  Raw URLs are allowed only if completely necessary and appropriate.
- Timestamps: Use UTC. You MUST verify the current date and time before
  reporting by using available tools (e.g., `date` in bash) or checking the
  system prompt. The format MUST be `{YYYY-MM-DD HH:MM UTC}`.
- Structural Layout: You MUST use a single `#` for the main headline and
  exactly `##` for content sections. No other header depths are allowed.
- Style Preferences: Adhere to guidelines in `skills/prefs-markdown/SKILL.md`.
- Flat Lists: Start every list item at the beginning of the line with `- `
  Do not add extra vertical line spaces or padding between list items.
- Line Length: Hard-wrap lines to a maximum of 80 characters.

## Status Update Structure
Generate your report using this exact structural template:

```
# {ICON} {Ticket ID} - {exact name of task directory} - {YYYY-MM-DD HH:MM UTC}

## Goal
- {Single-sentence summary of the overall task objective}

## Packet Status
- 🟢 001 - {Packet Name} - Complete - {Brief Description}
- 🟠 002 - {Packet Name} - In Progress - {Brief Description}
- 🟡 003 - {Packet Name} - Pending - {Brief Description}
- 🔴 004 - {Packet Name} - Blocked - {Brief Description}

## Next Steps
- {example: Packet 004 is next, pending completion of Packet 003}

(via {Agents} and {Users})
```

## Placeholders
- {ICON}: Status-specific icon (🔴, 🟡, 🟠, 🟢).
- {Ticket ID}: The task ID following the `ROP-####` format.
- {exact name of task directory}: The folder name in `active-tasks/`.
- {Agents}: Comma-separated list of all agents (Orchestrators and Executors)
  who have worked on this task, found in TASK.md Log or packet reports.
- {Users}: Comma-separated list of all Users who have contributed to the task.

## Status Icons
- 🔴 Blocked: The packet cannot proceed.
- 🟡 Pending: The packet is waiting to be started.
- 🟠 In Progress / Routed: The packet is currently being worked on.
- 🟢 Task done: The packet has been completed successfully.
