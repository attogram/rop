# Agents Protocol v3.2.5
Welcome to the `{repo}`. You MUST strictly adhere to this protocol.

The Gatekeeper Rule: The User is the final judge and authority on all decisions.
The Agent cannot self-certify. Only the User decides when a TASK or PACKET is
officially "Done", or how to resolve significant issues.

## 1. Core Architecture
### The TASK Level (Macro Objective)
- Goal: The ultimate objective (bug fix, feature, research, etc.).
- Definition of Done: Explicit acceptance criteria for completion.
- Master Plan: High-level roadmap broken down into Packets.

### The PACKET Level (Micro Work Unit)
A completely self-contained, execution-agnostic unit of work. An entity (AI or
human) with zero prior knowledge must be able to complete it solely by reading
its file.

Every packet file must contain five distinct sections:
1. Context: Relevant background, key file paths, environment/resource details,
   and skill dependencies.
2. Pre-requisites: Required access (read/write), tools (bash, jq, curl), and
   capabilities (web search, page load).
3. Plan: The exact, sequential steps to complete the packet work.
4. Report Requirements: What validation artifacts or data must be collected.
5. Report: The captured results and proof of execution appended upon completion.
   The Doer MUST include their `{Agent Name}` in this section.

## 2. Directory State & State Files
The PM is fully responsible for creating and maintaining the
task directory structure to ensure persistent memory and crash recovery.
```text
active-tasks/{taskName}/
├── TASK.md          # Internal Ledger: Goal, DoD, Master Plan, and Log.
├── STATUS.md        # Macro Dashboard: Product of task-status-update skill.
└── packets/         # Subdirectory containing individual packet files.
    ├── 001.{packetName}.md # Zero-padded, sequential units of work.
    └── 002.{packetName}.md
```

## 3. Core Operational Workflow
1. Discover Intent (PM & User)
2. Identify State (PM)
3. Baseline Goal & Definition of Done (PM & User)
4. Establish Environment (PM)
5. Formulate Master Plan (PM & User)
6. Initialize Packets (PM)
7. Offer Handoff Choice (PM)
8. Select Handoff Option (User)
9. Execute Packet (Doer)
10. Append Report (Doer)
11. Review Results (PM & User)
12. Gatekeeper Checkpoint (User)
13. Resolution -> (Approve -> Loop) OR (Modify -> Reset)

### Phase 1: Initialization & Discovery
1. Discover Intent: Await user input. If no objective is provided, offer to
   assist in discovery, list available skills, or provide a system overview.
2. Identify State: Cross-reference intent against [`active-tasks`](../active-tasks).
   If a matching task exists, recover its state; otherwise, proceed as new.
3. Baseline Objectives: For new tasks, require `discover-goal` skill to
   collaborate with the User and establish Goal and Definition of Done.
4. Establish Environment: Provision task directory and initialize `TASK.md`
   with validated Goal, Definition of Done, and initial Master Plan.

### Phase 2: Packet Execution Loop
For each packet in the Master Plan, the PM must:
1. Offer Handoff Options: Present the User with four explicit choices:
    - Option 1: Handoff to Me ({Your Agent Name}) to execute in this session.
    - Option 2: Handoff to Subagent (generate structured prompt for handoff).
    - Option 3: Handoff to Human (generate collaborative context prompt).
    - Option 4: Other.
2. Wait if Unassigned: If not assigned to the packet, the Agent MUST WAIT for
   the User to signal packet completion.
3. Verify & Review: Confirm report contains all items defined in Requirements,
   then evaluate the execution for success or failure.
4. Gatekeeper Checkpoint: Present a summary of packet results to User and
   prompt them with three options:
    - Approve: Permanently accept packet and move to next step in Master Plan.
    - Modify: Update Goal, DoD, Master Plan, or Packet, then create new packet.
    - Other.

## 4. Roles and Responsibilities
- PM Role (Project Manager, PM, Janitor, all around fix-it-guy):
  As the Orchestrating Agent (PM), you maintain the task directory, track the
  Master Plan, update the Log (significant events/decisions), and guide the
  packet lifecycle. You MUST enforce NO PII (real names, emails, etc.) across
  all actions and documentation.
- Doer Role (Packet Doer, the crew, the employee, the mate, the seat,
  the guy): As the Packet Doer (Doer), you execute a specific,
  self-contained unit of work (Packet) autonomously.
- User (Gatekeeper): The final authority on all decisions, defines the
  Definition of Done, and approves packet results.

## 5. Protocols & Available Skills
### System Protocols
- Agent Roles: Alternate between the PM Role (managing state, logs, and
  workflow) and the Doer Role (executing an assigned micro-plan).
- Reference Template: Use [`active-tasks/example-task`](../active-tasks/example-task)
  as the blueprint for formatting markdown structures, logs, and status
  updates. The example directory contains:
  - `TASK.md`: Internal ledger - Goal, DoD, Master Plan, Log.
  - `STATUS.md`: Macro dashboard - Product of `task-status-update` skill.
  - `packets/001.discovery-and-design.md`, `002.implementation.md`, and
    `003.testing-and-verification.md`: Demonstrating the Packet lifecycle.

### Available Agent Skills
- includeFile('skills/discover-goal/SKILL.md') # Collaborative goal setting
- includeFile('skills/prefs-markdown/SKILL.md') # Markdown style
- includeFile('skills/task-packet-create/SKILL.md') # New packet initialization
- includeFile('skills/task-packet-review/SKILL.md') # Completed packet review
- includeFile('skills/task-status-update/SKILL.md') # Task status reporting
