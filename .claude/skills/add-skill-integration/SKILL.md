---
name: add-skill-integration
description: Create new skills to integrate third-party services or features into user projects. Use this skill when adding new service integrations.
---

# Add Skill Integration

## Overview

This skill guides you on how to install skills into user projects. Skills are modular integration guides that help integrate third-party services and features.

## When to Use This Skill

Use this skill when users:
- Need to add new service integrations (databases, APIs, etc.)
- Want to create custom skill documentation

## Quick Start

### Install Skills

Use `add-skill` to install skills from a Git repository to your agent:

```bash

# Install to Claude Code
npx add-skill https://github.com/your-org/your-skills -a claude-code -y

# GitHub shorthand
npx add-skill vercel-labs/agent-skills -a claude-code -y

# Full GitHub URL
npx add-skill https://github.com/vercel-labs/agent-skills -a claude-code -y

# Direct path to a skill in a repo
npx add-skill https://github.com/vercel-labs/agent-skills/tree/main/skills/ frontend-design -a claude-code -y

# GitLab URL
npx add-skill https://gitlab.com/org/repo -a claude-code -y

# Any git URL
npx add-skill git@github.com:vercel-labs/agent-skills.git -a claude-code -y
### Supported Agents

- More agents see [add-skill documentation](https://github.com/vercel-labs/add-skill)

```

## Example References

Reference existing skill implementations:

- [Vercel Agent Skills](https://github.com/vercel-labs/agent-skills)
- [Remotion Skills](https://github.com/remotion-dev/skills)


