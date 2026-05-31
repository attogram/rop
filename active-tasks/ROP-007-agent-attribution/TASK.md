# Task: Agent Attribution
# Ticket: ROP-007

Implement a standardized agent attribution footer for all status reports to
clearly identify PM and Worker roles.

## Goal

Every `STATUS.md` must have a footer in the format `({PM agents}, {Worker
agents})`, with the current PM listed first.

## Definition of Done

- `AGENTS.md` and `HROP.md` updated with the new footer requirement.
- `skills/task-status-update/SKILL.md` updated to v4.0 with new template.
- All `STATUS.md` files in `active-tasks/` (including global) updated to
  conform to the new format.

## Master Plan

- Phase 1: Protocol and Skill Update (Active)
- Phase 2: Repository-wide Application

## Packet List

- 001 - update-protocol-and-skill - Complete - Update AGENTS.md, HROP.md and status skill.
- 002 - apply-attribution-format - Complete - Update all STATUS.md files in the repo.

## Log

- 2026-05-31: Task initialized by Jules.
- 2026-05-31: PM scaffolded task directory and initialized TASK.md/STATUS.md.
- 2026-05-31: Executed Packet 001: Updated protocol and skills.
- 2026-05-31: Executed Packet 002: Applied new attribution format repository-wide.
