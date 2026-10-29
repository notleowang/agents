---
inclusion: always
---

# Operating Model

<!-- PLACEHOLDER — define the rules every agent in this workflow follows. -->

## Principles

- Least privilege (explicit tool scoping)
- Spec-driven (plan before execute)
- One task at a time (small changes)
- Independent validation (tester + reviewer)
- Evidence required (tests run, diffs shown)

## Workflow

```
team-leader creates spec
    ↓
researcher investigates (if external deps)
    ↓
developer implements
    ↓
tester + code-reviewer validate (parallel)
    ↓
approved? → next task
blocked? → developer fixes → re-validate
```
