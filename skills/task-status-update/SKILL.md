---
name: task-status-update
description: >
    Use this when you need to draft a concise status update for a task.
    Generates a well-formatted report, ready for copy-pasting directly into Jira, Slack, or Email.
---

# Skill: Task Status Update v3.6
This skill drafts a clear, concise, and effective status update for a task.
The final output MUST be provided as plain Markdown text
to ensure easy copy-pasteability.

## Guiding Principles
- Target Audience: Design the update for a busy Project Manager skimming
  Jira tickets to grasp the exact status of the task instantly.
- Task-Level Context: The update must summarize progress on the entire task.
- Complete Scope: List every single packet to show the full picture,
  regardless of whether it has started or not.
- High Signal: Omit conversational filler, decorative spacers, and emojis.
- Report, Don't Direct: Do not give commands to the user.
- No Markdown Hyperlinks: Do not hide URLs inside markdown syntax like `[text](url)`.
  Raw URLs are allowed only if completely necessary and appropriate.
- Timestamps: Use UTC. You MUST verify the current date and time before reporting
  by using available tools (e.g., `date` in bash) or checking the system prompt
  for the current time. If the exact time is inaccessible,
  use the last known timestamp or omit the time portion (YYYY-MM-DD only).
- Structural Layout: You MUST use a single `#` for the main headline and exactly
  `##` for content sections. No other header depths are allowed.
- Style Preferences: Adhere to style guidelines in `skills/prefs-markdown/SKILL.md`.
- Flat Lists: Start every list item at the absolute beginning of the line with `- `
  Do not add extra vertical line spaces or padding between list items.
- Line Length: Hard-wrap lines to a maximum of 80 characters.

## Status Update Structure
Generate your report using this exact structural template:

```
# Status Report - {Ticket ID} - {Task Name} - {YYYY-MM-DD HH:MM}

## Goal
- {Single-sentence summary of the overall task objective}

## Progress
- {High-level summary of milestone accomplishments and business/domain impact}

## Packet Status
- 001 - {Packet Name} - {Status} - {Brief Description of packet}
- 002 - {Packet Name} - {Status} - {Brief Description of packet}
- 003 - {Packet Name} - {Status} - {Brief Description of packet}
- 004 - {Packet Name} - {Status} - {Brief Description of packet}
- 005 - {Packet Name} - {Status} - {Brief Description of packet}

## Next Steps
- {example: Packet 004 is next in line to start, pending completion of Packet 003}
```
