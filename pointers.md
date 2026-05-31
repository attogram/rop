# Agent Pointers Guide

To ensure all agents follow the same core protocol, we use pointer files that
redirect to `AGENTS.md`. This maintains a single source of truth for the
contract between the User and the Agent.

## How to Configure Redirects

For any new agent-specific configuration file (e.g., `.clinerules`, `ROO_CLINE_USAGE_GUIDELINES.md`, etc.),
use the following format to point to the primary protocol:

```text
requireFile('{$PROJECT_ROOT}/AGENTS.md')
```

## Legacy Pointer Files

The following files were previously used and have been consolidated here:
- `CLAUDE.md`
- `GEMINI.md`
