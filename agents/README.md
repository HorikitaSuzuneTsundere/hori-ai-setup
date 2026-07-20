# ej-code-reviewer

## Overview

`ej-code-reviewer.md` defines a **subagent** configuration for an expert code review agent. It's a Markdown file with YAML frontmatter that specifies the agent's mode, permissions, and behavioral instructions.

## Configuration

| Field | Value |
|---|---|
| `mode` | `subagent` |
| `permission.bash` | `deny` (no shell access) |
| `permission.edit` | `deny` (no file editing) |

The agent is read-only by design — it can review and comment on code but cannot execute commands or modify files.

## Behavior

On invocation, the agent:

1. Loads eight specialized review skills via the `skill()` tool:
   - `ej-access-security`
   - `ej-architecture-resilience`
   - `ej-code-format-constraints`
   - `ej-correctness-contracts`
   - `ej-performance-memory`
   - `ej-programming-paradigms`
   - `ej-quality-longevity`
   - `ej-structure-responsibility`
2. Internalizes and applies these skills holistically.
3. Reviews code with a focus on:
   - Code clarity and readability
   - Adherence to best practices and design patterns
   - Performance and efficiency
   - Error handling and edge cases
   - Test coverage and testability

## Use Case

Drop this file into an agent framework that supports subagent definitions (e.g. an `agents/` or `.claude/agents/` directory) to add an automated, multi-lens code review step to a development workflow.
