# Moonlit skills

Curated skills for the Moonlit MCP server, authored and maintained by Moonlit.

A skill is a plain markdown file of instructions that an AI assistant reads once and applies from then on. These skills govern how an assistant works with Moonlit's legal research tools: the governing law is found first, verified at the source, and every claim of law carries a citation that can be checked in place.

This repository is the source of truth for the skill content. The skill library, with downloads and per-skill pages, is published at [www.moonlit.ai/docs/mcp/skills](https://www.moonlit.ai/docs/mcp/skills).

## The skills

| Skill | What it governs | Install it when |
|---|---|---|
| [`moonlit-operator`](moonlit-operator/SKILL.md) | Sourcing discipline: what counts as a source and what a citation must be | Any legal work with Moonlit tools available |
| [`moonlit-reasoning`](moonlit-reasoning/SKILL.md) | Analysis method: how law is applied to facts once sources are established | The assistant should analyze rather than merely report |
| [`moonlit-memo`](moonlit-memo/SKILL.md) | The full research memo: both disciplines embedded, plus the memo deliverable | You want written memos; it needs neither of the other two |

## Install

Per-client installation steps are on the [skills page](https://www.moonlit.ai/docs/mcp/skills). Each skill is served in two forms:

- `https://www.moonlit.ai/docs/skills/<slug>.zip` for clients with native skill support (claude.ai, ChatGPT, Microsoft 365 Copilot, Langdock, Mistral, Claude Code)
- `https://www.moonlit.ai/docs/skills/<slug>.md` as plain markdown, for any other client and for agents reading directly

## Format

One folder per skill, `<slug>/SKILL.md`, following the open Agent Skills format. The frontmatter carries `name` (equal to the folder name) and `description`; an optional `metadata` map is read by the docs site and ignored by clients:

```yaml
metadata:
  version: "1.0"
  works-best-with: "Reasoning on high effort; an app that can create files and run parallel subtasks"
  pairs-with: "moonlit-operator"
  updated: "2026-08-01"
```

All metadata keys are optional; absence renders nothing on the site. The phrasing is guidance ("works best with"), never a hard requirement: a skill degrades gracefully in clients without these capabilities.

## Governance

Skills in this repository are authored, reviewed and versioned by Moonlit. The repository history is the changelog; the `version` and `updated` frontmatter fields are the user-facing signal. Questions: [support@moonlit.ai](mailto:support@moonlit.ai).

## License

[MIT](LICENSE), Moonlit Legal Technologies B.V.
