# High ROP Workflow (HROP)
HROP is our opinionated implementation of High ROPness in a workflow.

## Target Audience
HROP is designed for small teams (the 1-3 member "sweet spot"). It is built
as a "drop-in the agents.md and go" solution for rapid scaling without
immediate infrastructure investment.

### The Janitor Tax
While HROP can scale further, increased team size leads to a rise in "janitor
fails" where state management becomes fragmented. The coordination complexity
(Janitor Tax) increases non-linearly with each additional user beyond the first.

## Human Summary of AGENTS.md
AGENTS.md is the formal contract for HROP. In simple terms:
- **Tasks** are the big goals.
- **Packets** are the small, self-contained work units.
- **PMs** (Project Managers) manage the state and task directories.
- **Workers** execute the individual packets.
- **User** is the final authority (Gatekeeper) who approves all work.

Everything is tracked in `active-tasks/{taskName}/` using `TASK.md`, `STATUS.md`,
and the `packets/` subdirectory to ensure persistent memory and easy recovery
from context restarts.

## Implementation
To maintain high ROP, you must save state continuously. The PM/User
collaboratively define Goals and Definitions of Done, then break the work into
sequential packets. After each packet, the User reviews the results and decides
whether to approve, modify, or pivot.

## Reporting & Metrics
We use standardized reporting loops for qualitative and quantitative analysis.

### FLUFFP Metric
FLUFFP is a metric (0-100) of wasted tokens vs. required tokens in a data
packet. It provides insight into possible optimizations per repo, task, or
packet.

### Standardized Reporting Loop
For `fluffp.md` and `reviews.md`, the workflow follows a strict loop:
1. **Assignment**: PM assigns packets to each agent (e.g., Gemini, Copilot,
   Jules).
2. **Intake**: PM collects all agent reports.
3. **Listing**: PM lists all reports in the target file (`{file}.md`).
4. **Distillation**: PM adds a summary with the most important issues
   distilled from all reports.
5. **User Feedback**: PM creates a packet for the User to reply to the summary.
6. **Restart**: Once approved, the loop restarts with the previous reports and
   User replies included as context.
