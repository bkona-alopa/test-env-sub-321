# Custom Agents Configuration

This file can be used to define custom agents for your project. As your skills library grows, you may want to create specialized agents that combine multiple skills or have specific tool restrictions.

## Example Custom Agent

```yaml
---
name: my-custom-agent
description: "A specialized agent for [specific domain]"
tools: ["all"]  # or specific tools to restrict
---

# Agent Description

Your agent description here.
```

## Workspace Customizations

- **Skills**: Define domain-specific workflows in `.github/skills/`
- **Instructions**: Add general guidance in `.github/copilot-instructions.md`
- **Hooks**: Configure deterministic behaviors in `.github/hooks/`

See `.github/skills/SKILLS_README.md` for more information about adding skills.
