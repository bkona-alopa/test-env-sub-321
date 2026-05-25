---
name: jira-workflow
description: "JIRA-integrated task management workflow. Use when: starting a new task, creating a branch, or raising a pull request - ensures JIRA ticket is captured and used consistently in branch names and PR titles."
tags:
  [
    "jira",
    "branching",
    "pull-requests",
    "workflow",
  ]
version: "1.0.0"
---

# JIRA Workflow Skill

Streamline your development workflow by integrating JIRA tickets into your branch names and pull requests.

## Overview

This skill guides you through a complete JIRA-integrated workflow:

1. **Start Task** - Asks for your JIRA ticket identifier
2. **Create Branch** - Generates a branch name using the JIRA ticket
3. **Raise PR** - Automatically includes the JIRA ticket in the PR title

## When to Use

- **Starting a new task**: Ask me to "start work on a task" or "begin a new feature"
- **Creating a branch**: Use the JIRA ticket to generate a properly-named branch
- **Raising a PR**: Let me know you're ready, and I'll ensure the PR title includes the JIRA ticket

## Workflow Steps

### 1. Start a Task

Ask me: _"I want to start work on a task"_ or _"Help me begin a new feature"_

I will:

- Ask you for your JIRA ticket ID (e.g., `PROJ-123`)
- Ask for a brief description of the work
- Use GitLens to create a branch linked to the issue

### 2. Create Branch

Based on your JIRA ticket, I'll create a branch with a name like:

```
PROJ-123-add-user-authentication
PROJ-456-fix-login-bug
JIRA-789-implement-payment-integration
```

Branch naming convention: `{TICKET}-{description}`

### 3. Make Your Changes

Make all your code changes and commits as usual.

### 4. Raise a Pull Request

When you're ready, ask me: _"Create a pull request"_ or _"Raise the PR"_

I will:

- Create the PR with a title that includes your JIRA ticket
- Example PR title: `[PROJ-123] Add user authentication`
- Use the branch name and commit history to populate the description

## Example Workflow

```
You: "I want to start work on a task"
Me:  "What's your JIRA ticket ID?"
You: "PROJ-123"
Me:  "What are you working on?"
You: "Implement user authentication"
Me:  [Creates branch: PROJ-123-implement-user-authentication]

[You make changes...]

You: "I'm ready to raise the PR"
Me:  [Creates PR with title: "[PROJ-123] Implement user authentication"]
```

## JIRA Ticket Format

Your JIRA ticket should follow standard format:

- `PROJECT-NUMBER` (e.g., `PROJ-123`, `DEV-456`, `BUG-789`)
- Can be uppercase or lowercase
- The ticket will be preserved as-is in branch names and PR titles

## Related Tools

This workflow integrates with:

- **GitLens** - For creating work-linked branches
- **Git operations** - For branch creation and PR management
- **GitHub API** - For pull request creation

## Best Practices

1. **Consistent format**: Always use your project's JIRA ticket naming convention
2. **Descriptive branches**: Include a brief description after the ticket ID
3. **Clear PR titles**: Include the JIRA ticket at the start of the PR title
4. **Link tracking**: The ticket in branch/PR makes it easy to track work across systems

## Troubleshooting

**"What if I don't have a JIRA ticket?"**

- You can still use this workflow by providing a descriptive identifier
- Consider creating a JIRA ticket first for better tracking

**"Can I modify the branch name?"**

- Yes! The generated name is a suggestion. You can adjust it if needed.

**"How do I use this with existing branches?"**

- If you already have a branch without a JIRA ticket, you can still reference the ticket when creating the PR

---

**To use this skill**: Just ask me to help you start a task, and I'll guide you through the workflow!
