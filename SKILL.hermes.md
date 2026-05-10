---
name: ultrawork
version: 1.1.0
description: Parallel execution engine — run multiple tasks simultaneously — Hermes Edition
compatible-with: hermes-agent
---

# Ultrawork — Hermes Edition

Parallel execution engine that runs multiple independent tasks simultaneously using Hermes-native `delegate_task` batch mode.

## What It Does

- Takes multiple independent tasks
- Fires them all at once (not sequentially)
- Routes each to appropriate subagent
- Waits for all to complete
- Returns combined results

## Usage (Hermes)

### Batch Mode (recommended)

```python
# Hermes delegate_task supports parallel execution via tasks array
result = delegate_task(
    tasks=[
        {"goal": "Add TypeScript types to auth.ts", "toolsets": ["terminal", "file"]},
        {"goal": "Fix bug in utils.ts date parsing", "toolsets": ["terminal", "file"]},
        {"goal": "Update README with new API docs", "toolsets": ["terminal", "file"]},
    ]
)
# All 3 run in parallel. Result is an array of summaries.
```

### Tier Routing

| Tier | Hermes Tool | Use For |
|------|------------|---------|
| FAST | `terminal()` with simple commands | Trivial lookups, typos |
| STANDARD | `delegate_task(goal=..., toolsets=['terminal','file'])` | Normal implementation |
| DEEP | `delegate_task(goal=..., toolsets=['terminal','file','web'])` | Complex analysis |
| ORCHESTRATOR | `delegate_task(role='orchestrator', ...)` | Multi-step workflows |

### Background Execution

For long-running tasks that don't need immediate results:

```python
# Start in background
terminal("npm run build", background=True, notify_on_complete=True)

# Or delegate to subagent with full toolset
delegate_task(
    goal="Refactor auth module to OAuth2",
    context="Project uses Next.js 15, src/auth/ directory",
    toolsets=["terminal", "file", "web"]
)
```

## When to Use

Use Ultrawork when:
- Multiple independent tasks can run simultaneously
- Tasks don't depend on each other
- You want to reduce total execution time

Do NOT use when:
- Tasks have dependencies (B needs A to finish)
- Only one sequential task
- You need guaranteed completion with verification (use Ralph pattern instead)

## Parallel vs Sequential

```
Sequential:                    Parallel (Ultrawork):
Task A → 10s → Task B → 10s    Task A → 10s
Total: 20s                     Task B → 10s
                               Total: 10s (3x+ speedup)
```

## Hermes-Native Equivalents

| OpenClaw | Hermes |
|----------|--------|
| `openclaw sessions spawn` | `delegate_task(goal=...)` |
| `/ultrawork "a" "b" "c"` | `delegate_task(tasks=[...])` |
| Background `&` | `terminal(background=True)` |
| Results collection | `delegate_task` returns array of summaries |

---

Built by [nerudek](https://github.com/nerudek). Support: [PayPal.me/nerudek](https://www.paypal.me/nerudek)
