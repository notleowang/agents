# Agent Framework

This is a framework I like to follow when working with agents. It's inevitable to not be utilizing AI in the software development lifecycle now so the goal here is to do so in a way that still feels structured and organized.

### Goal & Inspiration

Like I said before, it's impossible to not be using AI to boost your productivity whether that's for work, design, or personal projects. The thing I don't like is that I could vibe-code entire products and apps now, but obviously that would be bad.

Hence, I hope to adhere to a framework like this so that I can still learn and be the one piloting the entire development process.

### Disclaimer

This framework is by no means a standard. Everyone has different ways of utilizing agents in their work, and with AI constantly changing and coming out with new features, I understand that it can be difficult to mold a strict agentic workstyle.

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
├── README.md             # this file
└── kiro/                 # Kiro implementation (clone-and-drop)
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
cp -r kiro/.kiro /path/to/your/project/
```