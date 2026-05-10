# tapas-engineering-marketplace

A Claude Code plugin marketplace providing curated plugins for professional software engineering workflows.

---

## Quick Start

```bash
# Add this marketplace to Claude Code
claude plugin marketplace add sharma-tapas/ai-skills

# Browse available plugins
claude plugin marketplace list tapas-engineering-marketplace

# Install a plugin
claude plugin install tapas-engineering-toolkit@tapas-engineering-marketplace
```

---

## Available Plugins

| Plugin | Description | Skills |
|--------|-------------|--------|
| [tapas-engineering-toolkit](plugins/tapas-engineering-toolkit/) | TDD workflows, idiomatic Go & Python patterns, design challenges, Jira integration, PRD generation, and production guardrails | 11 |

---

## Marketplace Structure

```
ai-skills/
├── .claude-plugin/
│   └── marketplace.json              # Marketplace catalog
├── plugins/
│   └── tapas-engineering-toolkit/    # Plugin: engineering toolkit
│       ├── .claude-plugin/
│       │   └── plugin.json           # Plugin manifest
│       ├── skills/                   # 11 skill definitions
│       ├── claude.md/                # Project-level rules
│       ├── CHEAT_SHEET.md
│       └── README.md
├── README.md                         # ← You are here
└── LICENSE
```

---

## Adding New Plugins

To add a new plugin to this marketplace:

1. Create a new directory under `plugins/<plugin-name>/`
2. Add a `.claude-plugin/plugin.json` manifest inside it
3. Add your `skills/`, `commands/`, `hooks/`, or `agents/` directories
4. Register the plugin in `.claude-plugin/marketplace.json` under the `plugins` array
5. Include a `README.md` documenting the plugin's skills and usage

### Plugin name rules
- Must be **kebab-case** (e.g. `my-awesome-plugin`)
- Must use **SemVer** versioning in `plugin.json`
- Avoid hardcoded paths — use `${CLAUDE_PLUGIN_ROOT}` for internal references

---

## License

MIT
