# kmac-claude-kit

A personal toolkit for building software with [Claude Code](https://docs.anthropic.com/en/docs/claude-code). This repo describes how the pieces fit together.

## Components

| Repo | Purpose |
|---|---|
| [claude-sandbox](https://github.com/kmacmcfarlane/claude-sandbox) | Sandboxed Docker container for running Claude Code sessions safely. Mounts the project directory and host Docker socket, provides Node.js and build tools, and supports interactive and ralph (autonomous loop) modes. |
| [claude-templates](https://github.com/kmacmcfarlane/claude-templates) | Project templates for quick-starting new repos. Each template includes a full agent workflow (CLAUDE.md, backlog, practices docs), Docker Compose, and an MCP server for Discord notifications. |
| [claude-skills](https://github.com/kmacmcfarlane/claude-skills) | Reusable Claude Code skills (slash commands). Includes a bootstrap skill for generating new skills. |

## How they relate

```
kmac-claude-kit (you are here)
│
├── claude-sandbox        Start a sandboxed Claude Code session
│     │
│     └── mounts your project repo
│           │
│           ├── .claude/skills/     ← symlink or copy from claude-skills
│           │
│           └── (project scaffolded from claude-templates)
│                 ├── CLAUDE.md
│                 ├── agent/        Workflow contract, backlog, practices
│                 ├── docs/         Architecture, database, API docs
│                 ├── scripts/mcp/  Discord notifications
│                 └── ...
│
├── claude-templates      Template source (copy into new repos)
│     └── local-web-app/  Go + Vue + Docker Compose
│
└── claude-skills         Skill source (copy or symlink into projects)
      └── skills/
            └── create-skill/
```

## Workflow

### Starting a new project

1. Copy a template from [claude-templates](https://github.com/kmacmcfarlane/claude-templates) into a new repo.
2. Replace placeholder values (see the template's README).
3. Copy or symlink skills from [claude-skills](https://github.com/kmacmcfarlane/claude-skills) into `.claude/skills/`.
4. Write your PRD in `agent/PRD.md` and add stories to `agent/backlog.yaml`.
5. Run `make claude` to start a sandboxed session, or `make ralph` for autonomous loops.

### Day-to-day development

- **Interactive**: `make claude` launches a [claude-sandbox](https://github.com/kmacmcfarlane/claude-sandbox) container with Claude Code.
- **Autonomous**: `make ralph` or `make ralph-auto` runs fresh-context loops that pick up stories from the backlog automatically.
- **Notifications**: Discord MCP server pings you when the agent starts a story, needs input, finishes, or gets blocked.

### Creating new skills

Use the `create-skill` skill from [claude-skills](https://github.com/kmacmcfarlane/claude-skills):

```
/create-skill A skill that runs the test suite and summarizes failures
```

## License

This project is licensed under the [GPL-3.0](LICENSE).
