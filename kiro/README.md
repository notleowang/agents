# Kiro

Reusable, Kiro-specific agents, skills, and steering — packaged as a **drop-in** `.kiro/`
folder.

## Clone and use

Drag the `.kiro/` folder in this directory into the root of your own project. Kiro picks
it up automatically.

```bash
cp -r kiro/.kiro /path/to/your/project/
```

## Layout

```
kiro/
├── README.md       # this file
└── .kiro/          # ← drop this into your project
    ├── agents/     # agent definitions (<name>.json)
    ├── skills/     # skills, one folder each with a SKILL.md
    └── steering/   # standalone steering files (*.md)
```

## Formats

- **Agents**: JSON files describing name, description, tools, and permissions.
- **Skills**: a folder per skill with a `SKILL.md` entry point.
- **Steering**: Markdown, optionally with front-matter (`inclusion: always | fileMatch |
  manual | auto`) to control when it loads.

> These are standalone building blocks. For complete multi-agent processes, see
> [`../workflows/`](../workflows/).
