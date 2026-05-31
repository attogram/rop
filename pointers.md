# Agent Pointers Guide

To ensure all agents follow the same core protocol, 
use pointer files that redirect to `AGENTS.md`. 
This maintains a single source of truth for the
contract between the User and the Agent.

## How to Configure Redirects

For any new agent-specific configuration file
use the following format to point to the primary protocol:

```text
requireFile('{PROJECT_ROOT}/AGENTS.md')
```

## Example Pointers files

- `CLAUDE.md`
- `GEMINI.md`
- `.clinerules`
- `ROO_CLINE_USAGE_GUIDELINES.md`
