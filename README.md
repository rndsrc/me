# Style Guides

This repository stores reusable AI agent style guides.

## Use A Style Guide

Add an `AGENTS.md` file to your project:

```markdown
# Agent Instructions

Read `<FILE>.md` before <working-on-task>.
Follow it as the local policy for this repository.

If higher-priority instructions conflict with `<FILE>.md`, follow the
higher-priority instructions and mention the conflict in the final
response.
```

## Verify It Loaded

Ask the agent:

```text
Did you load the guide for <task>?
```

The agent should report:
* A marker.
* The local instruction source it used.
* Two or three rules that affected the work.

The marker is only a debugging canary.
It is not a secret.
