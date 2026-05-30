# High ROP Workflow
Rooted in the "Commit early, commit often" philosophy, the High ROP (HROP)
workflow is the specific implementation of the Restart Often Protocol
witnessed in this repository.

## The Role of AGENTS.md
The AGENTS.md file is the primary contract for all agent behavior in this repo.
It defines the state management, roles, and the available skill registry.
Adherence to AGENTS.md is mandatory for both Orchestrator and Executor roles to
ensure consistent handoffs and high ROP efficiency.

## Implementation
To maintain high ROP, the Agent and/or User must save state continuously to the
repository within the `active-tasks/{taskName}/` directory:
- TASK.md: The internal ledger containing Goal, Definition of Done, Master
  Plan, and Log.
- STATUS.md: The macro dashboard for tracking overall progress.
- packets/: A subdirectory containing zero-padded, sequential work units
  (e.g., `001.discovery.md`).

## Session Management
- After every packet is completed and reviewed, the User should ideally restart
  in a new session to clear the LLM's active context.
- The User can (and should) restart anytime context becomes cluttered or the
  agent's performance begins to degrade.

By following the HROP workflow, you ensure that each packet remains focused,
costs remain linear, and agent success rates remain high by preventing
context-induced performance degradation.
