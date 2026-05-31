---
name: task-packet-review
description: >
  Use this when a Packet is reported as complete. It provides a
  rigorous framework for verifying that the work meets the Report 
  Requirements and the Definition of Done.
---

# Skill: Task Packet Review v1.0

This skill ensures that the PM does not approve faulty or
incomplete work. Every report must be audited against the original 
Packet and the global project standards.

## The Review Checklist

A Packet Report is only valid if it passes all of the following:

1. Requirement Alignment: Does the Report contain every item listed in the
   "Report Requirements" section of the Packet?
2. Plan Execution: Were all steps in the "Plan" followed? If not, did the
   Doer provide a valid justification for the deviation?
3. Quality Standards: Does the work pass project-specific linting, 
   type-checking, and test suites?
4. Criteria Alignment: Does this specific unit of work satisfy the
   acceptance criteria or milestones assigned to this Packet?

## Review Outcomes

- Pass: The report is complete and verified. Proceed to the Gatekeeper
  Checkpoint.
- Fail: The report is missing data, has failed tests, or deviates from the
  plan without explanation. Send the Packet back to the Doer for
  remediation.

## No Blind Trust

The PM must independently verify the claims in the Report. If
the Doer says "All tests passed," the PM should confirm
the test output or rerun the command before approving.
