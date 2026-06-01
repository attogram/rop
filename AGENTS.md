# Agents Protocol v3.2.5
This is the agent control for the High ROP Workflow (HROP). All agents MUST
strictly adhere to this protocol to ensure consistent state management and
successful handoffs.

## The Gatekeeper Rule
The User is the final judge and authority. The Agent cannot self-certify. Only
the User decides when a TASK or PACKET is "Done".

## 1. Core Architecture
- **TASK**: The macro objective (bug fix, feature, research). Tracked via
  `TASK.md` (ledger) and `STATUS.md` (dashboard).
- **PACKET**: A self-contained unit of work that can be executed by anyone
  with zero prior knowledge.

## 2. Directory Structure
```text
active-tasks/{taskName}/
├── TASK.md          # Internal Ledger: Goal, DoD, Master Plan, and Log.
├── STATUS.md        # Macro Dashboard: Product of task-status-update skill.
└── packets/         # Sequential units of work (001.name.md).
```

## 3. Operational Workflow
1. **Discovery**: PM & User define Goal and Definition of Done.
2. **Environment**: PM initializes task directory and `TASK.md`.
3. **Execution**: Work is broken into packets. PM offers handoff options to
   the User (Self, Subagent, Human, Other).
4. **Review**: Worker appends a Report. PM and User review against the DoD.
5. **Checkpoint**: User approves or requests modifications.

## 4. Roles
- **PM Role**: Maintains state, tracks Master Plan, and guides the lifecycle.
  When a task is Done, the PM must analyze if it is useful for the current
  global state:
  - If useful: suggest move to `done-tasks/`.
  - If not useful: suggest deleting the task.
- **Worker Role**: Executes a specific, assigned packet autonomously.

## 5. Skills
The repository provides standardized skills for common operations like goal
discovery, packet creation, and status reporting. See `skills/` for details.
