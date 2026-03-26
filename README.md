# Skill Starter Template

A template for creating custom AI coding agent skills — compatible with **Claude Code**, **Cursor**, and **Kiro**.

## What is a Skill?

A skill is a reusable prompt that gives an AI coding agent specialized capabilities. Skills can be invoked to perform specific, well-defined tasks — like generating boilerplate, running audits, or following a multi-step workflow.

The template in this repo (`SKILL-STARTER-TEMPLATE.md`) provides a structured format you can adapt for any AI coding tool.

## Getting Started

1. **Clone or fork** this repository
2. **Copy** `SKILL-STARTER-TEMPLATE.md` and rename it to match your skill (e.g., `my-skill.md`)
3. **Fill in** each section of the template with your skill's details
4. **Install** the skill into your tool of choice (see guides below)

---

## Setup by Tool

### Claude Code

Claude Code uses a `.claude/` directory and `CLAUDE.md` files for project-level instructions.

**Skill location:**

```
project-root/
  .claude/
    commands/         # Skill files (markdown)
      my-skill.md
  CLAUDE.md           # Project-wide instructions (always loaded)
```

**How to install a skill:**

1. Create `.claude/commands/` in your project root
2. Place your skill `.md` file inside it
3. Invoke the skill in Claude Code with `/my-skill`

**Settings reference:**

| File | Purpose |
|------|---------|
| `CLAUDE.md` | Project-wide instructions, always included in context |
| `.claude/commands/*.md` | Slash-command skills, invoked with `/<filename>` |
| `.claude/settings.json` | Permissions, allowed/denied tools, MCP servers |
| `~/.claude/CLAUDE.md` | Global instructions across all projects |
| `~/.claude/commands/*.md` | Global slash-command skills |

---

### Cursor

Cursor uses `.cursor/rules/` for project-level rules in `.mdc` format (YAML frontmatter + markdown).

**Skill location:**

```
project-root/
  .cursor/
    rules/            # Rule files (.mdc format)
      my-skill.mdc
```

**How to install a skill:**

1. Create `.cursor/rules/` in your project root
2. Convert your skill to `.mdc` format (add YAML frontmatter to the markdown)
3. The rule is picked up automatically based on its inclusion mode

**`.mdc` format example:**

```markdown
---
description: "Generates accessible React components"
alwaysApply: false
globs: "src/components/**/*.tsx"
---

# Your skill content here
```

**Inclusion modes:**

| Mode | Frontmatter | Behavior |
|------|-------------|----------|
| **Always** | `alwaysApply: true` | Included in every session |
| **Auto Attached** | `globs: "*.tsx"` | Included when matching files are referenced |
| **Agent Requested** | `description: "..."` only | AI decides based on user intent |
| **Manual** | No description, no globs | Include with `@rule-name` in chat |

**Settings reference:**

| File | Purpose |
|------|---------|
| `.cursor/rules/*.mdc` | Project rules (version-controlled) |
| `.cursorrules` | Legacy root-level rules (deprecated) |
| Cursor Settings > General > Rules for AI | Global user rules |

---

### Kiro

Kiro uses a `.kiro/` directory with **steering files** (markdown with YAML frontmatter) for persistent AI instructions.

**Skill location:**

```
project-root/
  .kiro/
    steering/         # Steering files (markdown)
      my-skill.md
    specs/            # Spec-driven development artifacts
    hooks/            # Automation triggers
    agents/           # Custom agent definitions (.json)
```

**How to install a skill:**

1. Create `.kiro/steering/` in your project root
2. Place your skill `.md` file inside it with YAML frontmatter
3. The steering file is picked up based on its inclusion mode

**Steering file format example:**

```markdown
---
inclusion: auto
name: my-skill
description: "Generates accessible React components"
---

# Your skill content here
```

**Inclusion modes:**

| Mode | Frontmatter | Behavior |
|------|-------------|----------|
| **Always** | `inclusion: always` | Loaded into every interaction |
| **File Match** | `inclusion: fileMatch` + `fileMatchPattern: "*.tsx"` | Included when working with matching files |
| **Auto** | `inclusion: auto` + `description` | AI decides based on request context |
| **Manual** | `inclusion: manual` | Include with `#steering-file-name` in chat |

**Settings reference:**

| File / Directory | Purpose |
|------------------|---------|
| `.kiro/steering/*.md` | Project steering files (always or conditional) |
| `.kiro/specs/` | Spec-driven requirements, design, and task docs |
| `.kiro/hooks/*.kiro.hook` | Automation triggers (file events, prompt submit, etc.) |
| `.kiro/agents/*.json` | Custom agent definitions with tool/permission config |
| `.kiro/settings/mcp.json` | MCP server configuration |
| `~/.kiro/steering/` | Global steering files across all projects |
| `~/.kiro/agents/` | Global custom agents |

---

## Quick Comparison

| Feature | Claude Code | Cursor | Kiro |
|---------|-------------|--------|------|
| **Config directory** | `.claude/` | `.cursor/rules/` | `.kiro/steering/` |
| **Skill file format** | Markdown (`.md`) | MDC (`.mdc`) | Markdown (`.md`) |
| **Always-on instructions** | `CLAUDE.md` | `alwaysApply: true` | `inclusion: always` |
| **File-pattern matching** | N/A | `globs` field | `fileMatchPattern` field |
| **AI-decided inclusion** | N/A | Agent Requested (`description`) | `inclusion: auto` |
| **Manual invocation** | `/<command-name>` | `@rule-name` | `#steering-file-name` |
| **Global config** | `~/.claude/` | Settings UI | `~/.kiro/` |

---

## Template Structure

The template (`SKILL-STARTER-TEMPLATE.md`) guides you through defining:

| Section | Purpose |
|---------|---------|
| **Skill Metadata** | Name and one-line description |
| **When to Use** | Activation conditions and anti-patterns |
| **Goal** | Intended outcome for the user |
| **Inputs** | Required parameters and formats |
| **Workflow** | Step-by-step execution instructions |
| **Output Format** | Return structure and formatting rules |
| **Example** | Sample request and expected output |
| **Quality Checklist** | Validation criteria before completion |
| **Notes / Edge Cases** | Limitations and constraints |
| **Changelog** | Version history |

## Tips for Writing Good Skills

- **Be specific** — clearly define when the skill should and should not be used
- **Keep workflows ordered** — number each step and include validation checkpoints
- **Include examples** — a concrete input/output example removes ambiguity
- **Define quality criteria** — the checklist ensures consistent results
- **Keep it portable** — write the core skill in plain markdown, then adapt the frontmatter per tool

## License

MIT
