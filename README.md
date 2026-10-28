# agents

A home for my AI agents, skills, steering files, and agentic workflows — organized so
anyone can clone the repo and try them out.

Different AI tools (Kiro, Claude, Cursor, …) define agents, skills, and steering in their
own formats, so the repo is organized by tool first, with cross-tool **workflows** kept
separately.

**Clone and use.** Every tool folder contains a drop-in artifact named exactly what that
tool looks for — e.g. `.kiro/` for Kiro. Copy that artifact into the root of your own
project and the tool picks it up. Same rule inside each workflow.

Only Kiro is set up today. Other tools (e.g. `claude/` with `CLAUDE.md`, `cursor/` with
`.cursor/`) follow the same pattern and can be added later as sibling folders.

## Layout

```
agents/
├── kiro/
│   ├── README.md
│   └── .kiro/       # ← drop into your project
└── workflows/       # Self-contained agentic workflows (one folder each)
    └── spec-driven-dev/
        ├── README.md     # What the workflow is and how to use it
        └── kiro/.kiro/   # Kiro implementation (drop-in)
```

### Tool folders (`kiro/`, …)

Reusable building blocks for a single tool, in that tool's native format. Each holds a
drop-in artifact with the tool's magic name plus a README explaining it:

- **agents** — individual agent definitions
- **skills** — packaged skills
- **steering / rules** — standalone operating rules / context files

### Workflows (`workflows/`)

Each subfolder is one complete agentic workflow. A workflow bundles several agents,
steering, and docs that work together toward a process (not just a single agent). Every
workflow has a `README.md` plus a per-tool implementation you can copy into your own
project.

Start with [`spec-driven-dev`](workflows/spec-driven-dev/README.md).

## License

Released under the [MIT License](LICENSE).
