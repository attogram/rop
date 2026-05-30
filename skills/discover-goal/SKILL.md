---
name: discover-goal
description: >
  Use this skill to collaborate with the user to define the macro Goal
  and Definition of Done for a task.
---

# Skill: Discover Goal v1.4

This skill enforces a collaborative process where the agent and user work
together to propose, refine, and finalize clear task boundaries.

## Step 1: Define the Goal
Collaborate with the user to isolate the exact, high-signal objective of the
task.

- Prompt the user to describe the primary objective, or analyze the initial
  request and propose a draft objective to the user.
- Proactively suggest refinements to remove ambiguity and boil the goal down
  to a single concise statement.
- Guide the refinement collaboratively:
    - "Based on the request, I suggest our goal be [X]. Does that capture the
      exact core objective, or should we modify it?"

## Step 2: Define the Definition of Done (DoD)
Collaborate with the user to establish the explicit, verifiable acceptance
criteria.

- Analyze the goal and propose a concrete checklist of technical requirements
  (e.g., specific test coverage, files updated, or behaviors verified).
- Invite the user to add, modify, or remove criteria from the proposed list.
- Guide the refinement collaboratively:
    - "To verify this, I propose these criteria: [List]. How should we adjust,
      expand, or trim this list to ensure absolute alignment?"

## Step 3: Secure Final Gatekeeper Approval
Confirm the objectives are entirely accurate before exiting the skill.

- Present the combined, collaboratively drafted Goal and Definition of Done.
- Await explicit confirmation from the user that the definitions are final.
- Do not proceed or perform any other workflow steps until the user approves.
