# Task: Task Bloat Management
# Ticket: ROP-008

Establish a protocol for managing finished tasks to prevent `active-tasks/`
bloat and execute the first cleanup.

## Goal

Formalize the archiving protocol in `AGENTS.md`, create a `done-tasks/`
directory, and move completed tasks there to maintain a lean `active-tasks/`
directory while preserving history.

## Definition of Done

- `AGENTS.md` updated with PM archiving responsibilities.
- `done-tasks/` directory created at the root.
- Completed tasks (ROP-004, ROP-005, ROP-007) moved from `active-tasks/` to
  `done-tasks/`.
- Global `active-tasks/STATUS.md` updated.
- `README.md` updated with a "Done Tasks" section and correct hyperlinks.
- All markdown links verified.

## Master Plan

- Phase 1: Task Finalization and Auditing
- Phase 2: Cleanup and Relocation
- Phase 3: Documentation Update

## Packet List

- 001 - execute-cleanup - Complete - Move completed tasks and update docs.

## Log

- 2026-05-31: Task initialized to address active-tasks bloat.
- 2026-05-31: Formalized archiving protocol in AGENTS.md.
- 2026-05-31: Cleanup executed: ROP-004, ROP-005, ROP-007 moved to done-tasks/.
