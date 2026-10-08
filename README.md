# Spline Agent Skills

Build 3D scenes, websites and app screens in [Spline](https://spline.design)
from your AI agent. The agent works in a live Spline editor, so what it builds
is an editable Spline file, not generated code you have to maintain.

This repository is an agent plugin. It bundles:

- the **Spline MCP server**, hosted at `https://mcp.spline.design/mcp`
- a **skill** that teaches the agent how to work with it: when to use Spline,
  how to start, and the build–look–refine loop

## Install

### Cursor

Install **Spline** from the Cursor Marketplace (open **Customize** in the
sidebar, find Spline, select **Install**).

### Claude Code

```
/plugin marketplace add splinetool/spline-skills
/plugin install spline@spline
```

## Sign in

The first time the agent uses a Spline tool, your editor asks you to sign in
to Spline in the browser and approve access. The agent then works in your
Spline account.

When the agent creates or opens a file, it gives you a link to the Spline
editor. Open it in your browser: that tab connects to your agent, and you can
watch the design come together and edit it yourself.

## Learn more

- [Spline MCP server](https://docs.spline.design/generate/spline-mcp-server)
- [Spline Agent Skill](https://docs.spline.design/generate/spline-agent-skill)

## About this repository

This repository is published automatically from Spline's main codebase.
Pull requests here are not merged, and the next sync overwrites any change
made directly in this repository.
