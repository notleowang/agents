# Spec-Driven Development

One concrete workflow built on my [Agent Framework](../README.md): a team-leader drives a
spec, and specialized agents implement and validate the work one task at a time.

## Table Of Contents
1. [Agents](#agents)
2. [Workflow](#workflow)
3. [Principles](#principles)
4. [File Structure](#file-structure)
5. [Usage](#usage)

## Agents

- **Miku (team-leader)** - 
- **Luka (developer)** - 
- Bug fixer
- Researcher
- Code-reviewer

Other
- Logger

PR Reviewing
- Panel of agents that can review a PR

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

## Principles

A list of principles in my framework that are set for the agents to adhere to.

- Least privilege (explicit tool scoping)
- Spec-driven (plan before execute)
- One task at a time (small changes)
- Independent validation (tester + reviewer)
- Evidence required (tests run, diffs shown)


## File Structure

This workflow ships a per-tool implementation so you can clone just the part you need.
Right now only the Kiro implementation is scaffolded (placeholder definitions). Other
tools (`claude/`, `cursor/`, …) follow the same pattern and can be added as sibling
folders later.

```
spec-driven-dev/
├── README.md         # this file
└── .kiro/
    ├── agents/       # Agent definitions
    │   ├── team-leader.json
    │   ├── researcher.json
    │   ├── developer.json
    │   ├── tester.json
    │   └── code-reviewer.json
    └── steering/     # Operating rules
        └── operating-model.md
```

## Usage

Feel free to follow the instructions below if you want to try out my agentic workflow.

### Compatability Check

This agentic workflow is currently implemented for **Kiro**. Other tools can be added as
sibling folders later.

### Try it (Kiro)

Copy the `.kiro/` directory from the Kiro implementation into your own project:

```bash
cp -r .kiro /path/to/your/project/
```