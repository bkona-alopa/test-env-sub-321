# Skills Directory

This directory contains custom skills for this project. Skills are specialized workflows that bundle instructions, templates, and assets for specific tasks.

## Structure

Each skill is organized in its own folder with the following structure:

```
skills/
├── skill-name/
│   ├── SKILL.md          # Main skill definition
│   ├── template/         # (Optional) Template files used by the skill
│   ├── scripts/          # (Optional) Helper scripts
│   └── docs/             # (Optional) Additional documentation
```

## Creating a New Skill

1. Create a new folder in `.github/skills/` with your skill name
2. Add a `SKILL.md` file with the required frontmatter and documentation
3. (Optional) Add supporting files like templates, scripts, or docs

## Example Skill Structure

See `example-skill/` for a template of how to structure a skill.

## Skill Frontmatter

All `SKILL.md` files must start with YAML frontmatter:

```yaml
---
name: skill-name
description: "Brief description of what this skill does. Use when: specific trigger phrases"
---
```

### Required Fields

- **name**: The identifier for the skill (must match folder name)
- **description**: What the skill does and when to use it. This is crucial for discovery.

### Optional Fields

- **user-invocable**: Set to `false` to hide from slash commands (default: `true`)
- **tags**: Array of tags for categorization
- **version**: Semantic version of the skill

## Discovery

The `description` field is how the AI agent decides whether to load and use your skill. Make it specific and include "Use when:" patterns with relevant keywords.

## Best Practices

1. Keep skill descriptions concise but informative
2. Include trigger phrases in descriptions (e.g., "Use when: testing Python code")
3. Bundle related templates and scripts together
4. Document any external dependencies
5. Keep skills focused on a single domain or workflow
