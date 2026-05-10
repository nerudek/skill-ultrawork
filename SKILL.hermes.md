---
name: ultrawork
version: 1.0.1
description: Parallel execution engine — run multiple tasks simultaneously — Hermes Edition
compatible-with: [openclaw, hermes]
---

# Ultrawork — Hermes Edition

Parallel execution engine that runs multiple independent tasks simultaneously. Speed through parallelism.

## What It Does

- Takes multiple independent tasks
- Fires them all at once (not sequentially)
- Routes each to appropriate model/tier
- Waits for all to complete
- Returns combined results

## Usage (Hermes)

```bash
# Using delegate_task for parallelism (Hermes native)
# Load this skill, then use delegate_task with tasks array

# Install
git clone https://github.com/nerua1/skill-ultrawork.git ~/.hermes/skills/ultrawork/
```

## Usage (OpenClaw)

```bash
openclaw skill run ultrawork
```

---

Built by [nerua1](https://github.com/nerua1). Support: [PayPal.me/nerudek](https://www.paypal.me/nerudek)
