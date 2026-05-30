# Coding Agents Protocol v3.2.3

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

Every packet file must contain four distinct sections:
1. Context: Relevant background, key file paths, environment/resource details,
   and skill dependencies.
2. Plan: The exact, sequential steps to complete the packet work.
3. Report Requirements: What validation artifacts or data must be collected.
4. Report: The captured results and proof of execution appended upon completion.

## 2. Directory State & State Files
The Orchestrator is fully responsible for creating and maintaining the
task directory structure to ensure persistent memory and crash recovery.
```text
active-tasks/{taskName}/
├── TASK.md          # Internal Ledger: Goal, Definition of Done, Master Plan, Packet List, and Log.
├── STATUS.md        # Macro Dashboard: Product of requireFile('skills/task-status-update/SKILL.md')
└── packets/         # Subdirectory containing individual packet files.
    ├── 001.{packetName}.md # Zero-padded, sequential units of work.
    └── 002.{packetName}.md
```

## 3. Core Operational Workflow

1. Discover Intent (Orchestrator & User)
2. Identify State (Orchestrator)
3. Baseline Goal & Definition of Done (Orchestrator & User)
4. Establish Environment (Orchestrator)
5. Formulate Master Plan (Orchestrator & User)
6. Initialize Packets (Orchestrator)
7. Offer Handoff Choice (Orchestrator)
8. Select Handoff Option (User)
9. Execute Packet (Executor)
10. Append Report (Executor)
11. Review Results (Orchestrator & User)
12. Gatekeeper Checkpoint (User)
13. Resolution -> (Approve -> Loop) OR (Modify -> Reset)

### Phase 1: Initialization & Discovery
1. Discover Intent: Await user input. If no objective is provided, offer to
   assist in discovery, list available skills, or provide a system overview.
2. Identify State: Cross-reference the intent against [`active-tasks`](../active-tasks). If a
   matching task exists, recover its state; otherwise, proceed as a new task.
3. Baseline Objectives: For new tasks, requireFile('skills/discover-goal/SKILL.md') to
   collaborate with the User and establish the macro Goal and Definition of Done.
4. Establish Environment: Provision the task directory structure and initialize
   `TASK.md` with the validated Goal, Definition of Done, and initial Master Plan.

### Phase 2: Packet Execution Loop
For each packet in the Master Plan, the Orchestrator must:
1. Offer Handoff Options: Present the User with four explicit choices:
    - Option 1: Handoff to Me ({Your Agent Name}) to execute in this session.
    - Option 2: Handoff to Subagent (generate structured prompt for handoff).
    - Option 3: Handoff to Human (generate collaborative context prompt).
    - Option 4: Other.
2. Wait if Unassigned: If not assigned to the packet, the Agent MUST WAIT for
   the User to signal packet completion.
3. Verify & Review: Confirm the packet report contains all items defined in the
   Report Requirements, then evaluate the execution for success or failure.
4. Gatekeeper Checkpoint: Present a summary of the packet results directly to
   the User and prompt them with three options:
    - Approve: Permanently accept packet and move to next step in Master Plan.
    - Modify: Update Goal, Definition of Done, Master Plan, or Packet, then create new packet.
    - Other.

## 4. Roles and Responsibilities

- Orchestrator Role: Maintains the task directory, tracks the Master Plan,
  updates the Log (significant events and decisions), and guides the packet
  lifecycle.
- Executor Role: Executes a specific, self-contained unit of work
  (Packet) autonomously.
- User (Gatekeeper): The final authority on all decisions, defines the
  Definition of Done, and approves packet results.

## 5. Protocols & Available Skills

### System Protocols
- Agent Roles: Alternate between Orchestrator Role (managing state, logs, and
  workflow) and Executor Role (executing an assigned micro-plan).
- Reference Template: Use [`active-tasks/example-task`](../active-tasks/example-task)
  as the blueprint for formatting markdown structures, logs, and status updates.
  The example directory contains:
  - `TASK.md`: Internal ledger - Goal, Definition of Done, Master Plan, Log.
  - `STATUS.md`: Macro dashboard - Product of requireFile('skills/task-status-update/SKILL.md')
  - `packets/001.discovery-and-design.md`, `002.implementation.md`, and
    `003.testing-and-verification.md`: Demonstrating the Packet lifecycle.

### Available Agent Skills
- includeFile('skills/task-status-update/SKILL.md') # How to write a status update for a task
- includeFile('skills/prefs-markdown/SKILL.md') # Markdown style
