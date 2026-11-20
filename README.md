# Inspek for Claude Code

[Inspek](https://inspek.dev) is a browser extension for inspecting, editing and annotating any web page. This repository is the Claude Code plugin marketplace for Inspek: the plugin connects Claude Code to the extension, so Claude can read your visual CSS edits and annotations, preview CSS in your browser, propose changes you keep or discard, study a site's design and verify its fixes.

## Install

In Claude Code:

```
/plugin marketplace add arsyadcc/inspekdev
/plugin install inspek@inspek
/inspek:setup
```

`/inspek:setup` installs the small helper that lets the extension connect to Claude Code on this computer. Then open the Inspek extension's options (right-click the Inspek icon → Options) and press **Connect to Claude Code**.

Not using the plugin? `npx inspekdev setup` adds the same MCP server to Claude Code directly.

## What is in the plugin

- **MCP server** `inspek`, run with `npx inspekdev mcp` ([inspekdev on npm](https://www.npmjs.com/package/inspekdev)).
- **Skill** `inspek`: when to use which Inspek tool, and how to verify a fix.
- **Skill** `/inspek:setup`: installs the browser connection and checks it with `npx inspekdev doctor`.

Everything runs on your computer: the extension talks to a hub on `127.0.0.1` that only paired clients can use.

You need the Inspek browser extension (Chrome, Edge, Brave, Arc, Helium and other Chromium browsers) and Node 20 or newer.

## Support

Questions and bug reports: open an issue in this repository.

## License

PolyForm Strict 1.0.0 (see LICENSE). Inspek, the extension, is sold separately at inspek.dev.
