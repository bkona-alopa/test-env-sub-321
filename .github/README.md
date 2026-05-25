# Project Customizations

This workspace uses VS Code customization files to enhance the development experience. 

## Structure

```
.github/
├── skills/               # Custom skills for specific workflows
├── AGENTS.md            # Custom agents configuration
└── copilot-instructions.md  # Workspace-level instructions (coming soon)
```

## Components

### Skills (`.github/skills/`)

Skills are specialized workflows that bundle instructions, templates, and scripts for specific tasks. Each skill is self-contained and can be added independently.

**To add a new skill:**
1. Create a folder in `.github/skills/` with your skill name
2. Add a `SKILL.md` file with frontmatter and documentation
3. Include optional template files, scripts, or documentation
4. See `.github/skills/SKILLS_README.md` for detailed guidance

**Example:** `.github/skills/example-skill/SKILL.md`

### Custom Agents (`.github/AGENTS.md`)

As your skills grow, you can define custom agents that combine multiple skills or have specific tool configurations. See `AGENTS.md` for more information.

### Instructions (Coming Soon)

You can add workspace-level instructions in `copilot-instructions.md` to guide AI agent behavior across the project.

## Quick Start

1. **Browse existing skills**: Check `.github/skills/` to see available skills
2. **Add your first skill**: Copy `.github/skills/example-skill/` and customize the `SKILL.md`
3. **Reference the example**: Use the example skill as a template for new skills

## Resources

- [Agent Customization Documentation](https://code.visualstudio.com/api/advanced-topics/custom-instructions)
- `.github/skills/SKILLS_README.md` - Detailed guide for creating skills
- `.github/AGENTS.md` - Custom agents configuration

---

**Tip**: The `description` field in `SKILL.md` is crucial for discovery. Include specific "Use when:" phrases so the AI agent knows when to apply your skill.
