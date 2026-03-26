# Skill Starter Template

A template repository for creating custom [Claude Code](https://docs.anthropic.com/en/docs/claude-code) skills.

## What is a Skill?

A skill is a reusable prompt that extends Claude Code with specialized capabilities. Skills can be invoked within Claude Code to perform specific, well-defined tasks — like generating boilerplate, running audits, or following a multi-step workflow.

## Getting Started

1. **Clone or fork** this repository
2. **Rename** `SKILL-STARTER-TEMPLATE.md` to match your skill (e.g., `my-skill.md`)
3. **Fill in** each section of the template with your skill's details
4. **Register** the skill with Claude Code

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

## License

MIT
