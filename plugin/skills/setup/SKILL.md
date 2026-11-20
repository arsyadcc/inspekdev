---
name: setup
description: Connect this computer's browser to Inspek for Claude Code. Run once after installing the plugin, or when Inspek says no browser is connected.
disable-model-invocation: true
allowed-tools: Bash(npx -y inspekdev@0.50.1 setup --no-mcp) Bash(npx -y inspekdev@0.50.1 doctor)
---

Set up the browser side of Inspek. This plugin already provides the MCP server, so only the browser connection is installed.

1. Run `npx -y inspekdev@0.50.1 setup --no-mcp`. It installs a small native messaging host in `~/.inspek/native` and tells each Chromium browser on this computer (Chrome, Chromium, Brave, Edge, Vivaldi, Arc, Helium) where to find it.
2. Tell the user to open the Inspek extension's options (right-click the Inspek icon → Options) and press **Connect to Claude Code**, then allow the browser's prompt. If the Inspek extension is not installed, say so: it is available from inspek.dev.
3. Run `npx -y inspekdev@0.50.1 doctor` and report what it says, in a short list. If it found problems, explain each fix in one sentence.
