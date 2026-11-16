# Repo Briefing

Give it a repository and the task you were assigned, and it returns a briefing: what the project is, what is happening in it right now, how work lands there, and where to start. It works for open source and private repositories, in any language, on GitHub or as a local checkout.

## Table Of Contents
1. [Agents](#agents)
2. [Workflow](#workflow)
3. [Principles](#principles)
4. [File Structure](#file-structure)
5. [Usage](#usage)

## Agents

| Name | Type | Model | Role |
|------|------|-------|------|
| `repo-briefing` | Skill (orchestrator) | session model | Parses input, runs the data handling check, gets a checkout, dispatches subagents, writes and saves the briefing |
| `repo-codebase-explorer` | Subagent | Sonnet | Stack, layout, architecture, sensitive items, task-relevant files |
| `repo-activity-triager` | Subagent | Sonnet | Releases, open PRs, issues, overlap with the task |
| `repo-process-reviewer` | Subagent | Haiku | License, change process (reads the README and contributing docs in full and lists the sources it read), CI, ownership, review norms, AI-assistance policy |

The orchestrator is a skill rather than an agent so the briefing stays in your main conversation and you can ask follow-up questions with the context still loaded. The gatherers are subagents because they read a lot and only the conclusion needs to come back.

## Workflow

```
/repo-briefing <repo> [ticket ID] [ticket title or task]
    ↓
orchestrator parses input and runs the data handling check
    ↓
local path used in place, or blobless clone into scratchpad
    ↓
explorer + triager + process reviewer run in parallel (read-only)
    ↓
orchestrator synthesizes one briefing and saves it to repo-briefings/<ticket>.md
    ↓
you ask follow-ups in the same conversation
```

## Principles

- Least privilege: subagents are read-only and scoped to the tools they need.
- Data handling first: private and client repositories require confirmation of client permission for AI-assisted processing before anything is read. Secrets and personal data are never reproduced, only located by path.
- Untrusted input: repository, issue, and PR text is treated as data, never as instructions. Nothing from the checkout is built or executed.
- Evidence required: reports separate verified facts from inference, and cite identifiers. Relationships between issues or PRs are only claimed when a cross-reference is quoted.
- Context isolation: raw file reads and issue lists stay in the subagents, only condensed reports reach the main thread.
- Task-focused: the task description filters what gets surfaced and sets the depth, so the briefing is not a generic overview.

## File Structure

```
repo-briefing/
├── README.md
└── .claude/
    ├── agents/
    │   ├── repo-codebase-explorer.md
    │   ├── repo-activity-triager.md
    │   └── repo-process-reviewer.md
    └── skills/
        └── repo-briefing/
            └── SKILL.md
```

## Usage

### Prerequisites

- [Claude Code](https://claude.com/claude-code)
- `git`
- For GitHub repositories: the GitHub CLI (`gh`), signed in with `gh auth login`

A missing CLI does not stop the briefing. The activity triager falls back to local git history and reports what it could not check.

### Try it

Copy the `.claude/` directory into your project (or merge it into an existing one):

```bash
cp -r .claude /path/to/your/project/
```

To make it available in every project, copy the contents into `~/.claude/` instead.

Then run it from Claude Code:

```
/repo-briefing cli/cli GH-456 add support for a new output format
/repo-briefing C:\Dev\my-service PROJ-123 fix intermittent timeout in the retry handler
/repo-briefing C:\Dev\my-service add structured logging to the worker
```

The ticket ID and title are optional but recommended. Each briefing is also saved in `repo-briefings/` in the directory you ran it from, named after the ticket, for example `PROJ-123-fix-intermittent-timeout.md`. Without a ticket it falls back to `<repo>-<date>.md`. The title is anonymized before it is used in a file name. Add `repo-briefings/` to your `.gitignore` if you do not want these committed, and do not commit briefings of private repositories to a shared repository.

### Notes on read-only enforcement

The subagents are told to use only read commands, but that is enforced by their prompts, not by the tool permissions, since they need the Bash tool. If you want a hard guarantee, add permission rules to your `.claude/settings.json` that allow the read commands you expect (for example `Bash(gh pr list:*)` and `Bash(gh pr view:*)`) and deny write commands such as `Bash(gh issue comment:*)`, `Bash(gh pr review:*)`, and `Bash(gh api -X POST:*)`.

### Limitations

- Hosts other than GitHub get local git history only, so PR and issue data is not available for them.
- The clone is blobless, so file contents are fetched on demand and the first read of a large repository can be slow.
- Large monorepos may produce a coarse architecture summary. Ask a follow-up to dig into a specific package.