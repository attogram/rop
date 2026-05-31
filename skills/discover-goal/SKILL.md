---
name: discover-goal
description: >
  Use this skill to collaborate with the user to define the macro Goal
  and Definition of Done for a task.
---

# Skill: Discover Goal v2.0

This skill enforces a collaborative process to isolate the exact, high-signal
objective of a task. The process depends on the clarity of the user's intent.

## Discovery States

### 1. No Goal (Vague/None)
If the user's request is non-existent or completely opaque:
- **Soft Scan**: Perform a "soft scan" of existing tasks in `active-tasks/` to
  understand current priorities and context.
- **Prompt User**: Suggest a MAXIMUM of 3 options on how to continue.
- **Style**: Use very short messages until vagueness is reached or a goal
  begins to emerge.

### 2. Vague Goal
If the user provides a goal that is directionally correct but lacks detail:
- **Immediate Scaffolding**: Start scaffolding the task directory immediately
  in `active-tasks/ROP-###-{name}/`.
- **Placeholders**: Initialize `TASK.md` and `STATUS.md` with placeholders for
  details that are still being discovered.
- **Iterate**: Refine the Goal and DoD collaboratively while working within
  the scaffolded directory.

### 3. Strong Goal
If the user's intent is crystal clear and all requirements are understood:
- **Discovery Done**: Proceed directly to finalizing the `TASK.md` Master Plan
  and initializing packets.

## Refinement Process

### Step 1: Define the Goal
- Proactively suggest refinements to remove ambiguity.
- Guide collaboratively: "Based on the request, I suggest our goal be [X]. Does
  that capture the core objective?"

### Step 2: Define the Definition of Done (DoD)
- Propose a concrete checklist of technical requirements.
- Invite user modification: "How should we adjust this list to ensure absolute
  alignment?"

### Step 3: Secure Final Gatekeeper Approval
- Present the combined Goal and DoD.
- Await explicit confirmation from the user that the definitions are final.
- Do not proceed with execution until the user approves.
