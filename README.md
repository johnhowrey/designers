# Designers

The parts of design your AI gets wrong, done properly.

**Live:** https://designers.allthepossibles.com (docs: `/docs`, every tool: `/tools`, machine-readable: `/llms.txt`)
**MCP endpoint:** `https://designers.allthepossibles.com/mcp`
**Built by:** [All the Possibles](https://allthepossibles.com)

## What it does

Designers is a remote MCP server for people who design with an AI assistant. The assistant is good at talking about design and bad at the parts that need arithmetic or a checklist. Designers does those deterministically and hands the numbers back to the model:

- **Contrast.** WCAG 2.2 ratios for text and UI pairs, APCA lightness contrast, the nearest color that passes, and a color-blind check that finds palette colors which merge under protanopia, deuteranopia and tritanopia.
- **Page accessibility.** Reads one page's HTML and names the WCAG 2.2 criterion behind each problem: missing alt, unlabelled fields, vague links, empty buttons, skipped headings, zoom locks, autoplay, tiny targets. Static markup only, and it says what it cannot see.
- **Touch targets, reflow, alt text quality, error message checks, page weight** and about thirty more small checks, each with a real input and output on its tool page.
- **Research and product hygiene.** Lint for interview questions, tracking plans and design critique; SUS scoring, sample sizes and test durations with the formula shown.
- **AI design slop.** Reads a live page's markup and CSS for the AI design defaults (purple gradients, Inter everywhere, pill buttons with arrows, eyebrow labels, identical card grids) and returns weighted signals, not a verdict.

It also carries the methods as MCP **prompts** (critique, heuristic evaluation, accessibility review, microcopy, research plan, handoff) that say which tools to call and how to use the Figma MCP when given a Figma link, and MCP **resources** (rubrics, templates, typography rules) that load into the conversation when asked.

No model calls happen on the server. Every tool answers with a `report` string you can read as well as structured output.

## Using it

**As an MCP server** (Claude Code, Claude Desktop, Cursor, VS Code, Codex, ChatGPT):

```json
{
  "mcpServers": {
    "designers": {
      "url": "https://designers.allthepossibles.com/mcp"
    }
  }
}
```

Claude Code: `claude mcp add --transport http designers https://designers.allthepossibles.com/mcp`

Per-client steps: https://designers.allthepossibles.com/docs/install

**Over REST:** every tool is also `POST https://designers.allthepossibles.com/api/<tool-id>` with a JSON body. Reference: https://designers.allthepossibles.com/docs

**Skills:** thirteen free Claude Skills that teach an assistant the same methods are in [atp-design-skills](https://github.com/johnhowrey/atp-design-skills).

## Free and Pro

Free covers every tool with a daily cap per tool (10 to 60 runs) and needs no signup. Pro is $5 a month: no daily caps, 300 requests a minute, a site-wide accessibility crawl, scored heuristic reports, bigger token matrices, saved project context and the industry playbooks. The key goes in as `Authorization: Bearer <key>`, or `?key=` on the server URL where your client has no header setting. Details: https://designers.allthepossibles.com/docs/pricing

## Limits, stated plainly

Automated checks reach roughly a third of WCAG. The page audit reads static HTML and cannot test color contrast on images, focus order, keyboard traps, screen reader announcements or anything built by script after load. Each tool page lists what it cannot see.

## Issues and questions

Open an issue here, or write to hello@allthepossibles.com. Tell us the tool, the input, and what you expected.

## License

The server is a hosted service. This repository holds its documentation and issue tracker and is CC0.
