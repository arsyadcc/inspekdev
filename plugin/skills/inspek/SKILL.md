---
name: inspek
description: Use when the user mentions Inspek, their browser edits or annotations, "what I changed in the browser", "my annotations", a page open in their browser that needs CSS or design fixes, or wants a site's design studied (colors, type, spacing, design.md). Covers which Inspek MCP tools to call and how to verify the result.
---

# Working with Inspek

Inspek is a browser extension in the user's own browser. Through the `inspek` MCP tools you read what they inspect, edit and annotate, preview CSS on the live page, and check your fixes. The page is real and the user is watching it.

## Pick the workflow

- **"Apply my browser edits"**: `get_changes`, edit the source where each change says (rule changes edit the rule and affect every element it matches; element changes edit that element's markup; Tailwind pages list classes to swap). Then `verify_changes` (with `reload: true` after the dev server rebuilt) until nothing is pending.
- **"Work through my annotations"**: `watch_annotations`. Read the whole batch and each screenshot first. Per annotation: `update_annotation` status `acknowledged`, make the change, then `resolved` with a one-line summary. Answer questions with a message instead of changing code. Never resolve one the user rejected.
- **"Try a style"**: `apply_css` previews it (recorded in the change log), `screenshot` to look, `revert_change` if it is wrong. Pass `edits` to make several changes in one call.
- **"What is this element?"**: `get_selection` is what the user points at; `inspect` describes any selector. Pass `selectors` to inspect several at once, and `properties` to keep answers short.
- **"Study this design"**: `extract_design` (`format: "design-md"` for a DESIGN.md file).
- **Review a page**: the `critique` and `self_driving` prompts walk it with `page_outline`, `audit_page`, `focus_element` and annotations.

## Habits that keep it fast and correct

- Results carry a short element `ref` (`e12`) next to each selector. Use refs in later calls; if one is stale, call `page_outline` or `inspect` again.
- Read `computedAfter` and `noEffect` from `apply_css` before taking a screenshot: they say whether the edit worked and why not.
- Screenshots are small JPEGs by default. Ask for `format: "png"` only to judge exact colors, and crop with `selector`.
- Fix the source, not the browser: browser edits are previews and vanish on reload.

## The user is in control

- If a tool says the user pressed **Stop**, stop at once and summarize what is done and what is left. Reading still works so you can report.
- On sites that are not local development servers Inspek may ask the user before your first change. If they decline, or the site is read-only for agents, describe the change instead of retrying.
- Password, payment and one-time-code fields are hidden from you in screenshots and markup. Do not try to read them another way.

## Next to Claude in Chrome

If the Claude in Chrome tools are also available, use them to interact (click, type, navigate, log in, open menus) and Inspek to understand and change the design (cascade-aware CSS, the change log, annotations, design study, verification). Both can work on the same tab.

## If nothing is connected

Call `status`. When no browser is connected, ask the user to run `/inspek:setup` (or `npx inspekdev setup`) once and to press **Connect to Claude Code** in the extension's options. `npx inspekdev doctor` says what is missing.
