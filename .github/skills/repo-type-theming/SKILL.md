---
name: repo-type-theming
description: "Automatic theme selection based on repository type. Use when: opening a repository - asks for repo type (utility, service, library, documentation, etc.) and applies the appropriate theme and workspace settings."
tags: ["theme", "workspace", "repo-type", "developer-experience"]
version: "1.0.0"
---

# Repo Type Theming Skill

Automatically apply different themes and settings based on your repository type for better visual organization and context switching.

## Overview

This skill detects when you open a repository and asks what type of repo it is. Based on your selection, it applies:
- **Theme**: Specific color scheme for the repo type
- **Workspace Settings**: Optimized editor settings for that type of work
- **File Associations**: Smart defaults for common file types
- **Extensions Recommendations**: Relevant extensions for that repo type

## When to Use

- **Opening a new repository**: I'll ask what type of repo it is
- **Switching projects**: Different themes help mentally switch context
- **Team consistency**: All utilities repos look the same, all services repos look the same, etc.

## Supported Repository Types

### 🛠️ **Utility**
- **Theme**: One Dark Pro (dark, focused)
- **Purpose**: Helper libraries, toolkits, shared utilities
- **Example**: `test-env-sub-321` (environment substitution utility)

### 🔧 **Service/Microservice**
- **Theme**: Dracula (high contrast)
- **Purpose**: Standalone APIs, microservices, backend services
- **Example**: User service, Payment service

### 📚 **Library**
- **Theme**: Nord (cool, calm colors)
- **Purpose**: Reusable packages, SDKs, frameworks
- **Example**: React component library, API client

### 📖 **Documentation**
- **Theme**: GitHub Light (clean, readable)
- **Purpose**: Docs, wikis, content repositories
- **Example**: Project documentation, guides

### 🎨 **Frontend/UI**
- **Theme**: Peacock (colorful, creative)
- **Purpose**: Web apps, UI components, design systems
- **Example**: React app, Vue frontend

### 🧪 **Testing/QA**
- **Theme**: Solarized Dark (soft, comfortable)
- **Purpose**: Test suites, QA automation, testing frameworks
- **Example**: E2E test suite, load testing scripts

## How It Works

### First Time Opening a Repo

```
You: Open repository in VS Code
   ↓
Me: "What type of repository is this?"
   ├─ Utility
   ├─ Service/Microservice
   ├─ Library
   ├─ Documentation
   ├─ Frontend/UI
   └─ Testing/QA
   ↓
You: Select "Utility"
   ↓
Me: ✅ Apply theme + workspace settings for utility repos
   ✅ Create/update .vscode/settings.json
   ✅ Save preference for future opens
```

### Subsequent Opens

Next time you open the repo, the theme and settings are automatically applied!

## Configuration

The skill stores your choice in `.vscode/settings.json` with:

```json
{
  "repoType": "utility",
  "workbench.colorTheme": "One Dark Pro",
  "editor.fontSize": 13,
  "editor.lineHeight": 1.6
}
```

## Changing Your Mind

Want to switch repo type themes?

1. Ask me: *"Change the repo type theme"*
2. Or manually edit `.vscode/settings.json` and change `repoType`
3. I'll update the theme accordingly

## Benefits

✅ **Context Switching** - Different colors = different project mindset  
✅ **Team Alignment** - Utility repos always look the same for your team  
✅ **Optimized Settings** - Each repo type gets editor settings suited to it  
✅ **Consistency** - All your utility repos share the same theme  
✅ **Flexibility** - Easy to override if needed  

## Example: Current Repository

This repository (`test-env-sub-321`) is a **utility** repo, so it uses:
- **Theme**: One Dark Pro (dark, focused atmosphere)
- **Font Size**: 13px
- **Line Height**: 1.6

If you work on a microservice next, it would automatically switch to Dracula theme when you open it!

## Troubleshooting

**"Can I use custom themes not in the list?"**
- Yes! The skill is a pattern. You can create custom theme assignments for your specific themes.

**"What if I don't have all these themes installed?"**
- The skill will ask you to install the theme, or you can substitute with themes you have.

**"Can I override per-file settings?"**
- Yes! Your `.vscode/settings.json` always takes precedence. Modify it anytime.

---

**To use this skill**: Just open a repository, and I'll ask what type it is. Pick one, and the theme applies automatically! 🎨

