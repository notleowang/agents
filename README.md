# agents

A home for my AI agents, skills, steering files, and agentic workflows.

## Harness Compatability

**Supported**
- [Kiro CLI]()

**Planned**
- [Claude Code]()
- [Codex CLI]()

## Navigating the Repository

Below is a quick overview of how this repository is organized.

```
agents/
├── .kiro/                   # Kiro dot folder
│   ├── agents/
│   ├── steering/
│   └── skills/
├── .claude/                 # Claude dot folder (planned)
│   ├── agents/
│   └── skills/
└── workflows/               # Collection of multi-agent workflows
    └── spec-driven-dev/
    └── pr-reviewers/
```

### Dot folders (`.kiro/`, `.claude/`)

Each dot folder targets one harness. You can copy the one that matches the one you are using into your project.

```bash
cp -r .kiro <your-project>
```

Here are the respective documentation for where you can drop in these folders and their configuration scopes:
- [Kiro](https://kiro.dev/docs/configuration/)
- [Claude Code]() (todo)
- [Codex]() (todo)

### Workflows (`workflows/`)

Each subfolder is a complete agentic workflow. A workflow bundles several agents, steering, and docs that work together across a process. Every workflow has its own `README.md` and a drop-in folder for each supported harness.

List of workflows:
- [`spec-driven-dev`](workflows/spec-driven-dev/README.md): Agents that write code following a spec-driven development methodology
- (planned) [`pr-reviewers`](): A panel of agents that can review pull requests

## License

Released under the [MIT License](LICENSE).
