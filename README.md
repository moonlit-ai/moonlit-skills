# Moonlit skills

Skills for the [Moonlit](https://www.moonlit.ai) MCP server. A skill is a plain markdown file of instructions that Claude (or any agent that accepts instructions) reads once and applies automatically from then on. These skills teach an agent to work with Moonlit's legal search tools the way a careful lawyer would: governing law first, verified at the source, citations that can be checked in place.

This repo is the source of truth for skill content. The user-facing library, with downloads and full skill text, lives at [www.moonlit.ai/docs/mcp/skills](https://www.moonlit.ai/docs/mcp/skills). That page rebuilds from this repo automatically: merge a skill folder to `main` and it appears on the next docs build with no further steps.

## The skills

| Skill | What it governs | Install it when |
|---|---|---|
| [`moonlit-operator`](moonlit-operator/SKILL.md) | Sourcing discipline: what counts as a source and what a citation must be | Any legal work with Moonlit tools available |
| [`moonlit-reasoning`](moonlit-reasoning/SKILL.md) | Analysis method: how law is applied to facts once sources are established | Claude should analyze rather than merely report |
| [`moonlit-memo`](moonlit-memo/SKILL.md) | The full research memo: both disciplines embedded, plus the memo deliverable | You want written memos; needs neither of the other two |

## Install

Zips are served from the docs site, one per skill: `https://www.moonlit.ai/docs/skills/<slug>.zip`.

**claude.ai**

1. Download the skill archive from [the skills page](https://www.moonlit.ai/docs/mcp/skills)
2. In claude.ai, open Customize, then Skills
3. Click the + button, choose Create skill, then Upload a skill
4. Upload the downloaded archive

Skills need the code execution capability; if Skills is not visible, enable it under Settings, then Capabilities.

**Claude Code**

```bash
unzip <skill>.zip -d ~/.claude/skills/
```

Agents can read each skill directly without downloading: `https://www.moonlit.ai/docs/skills/<slug>.md`.

## Repo layout and metadata

One folder per skill, `<slug>/SKILL.md`. Slugs are kebab-case and `moonlit-` prefixed for first-party skills. Frontmatter carries `name` (equal to the slug) and `description` (required), plus an optional `metadata:` map that Claude ignores and the docs generator reads:

```yaml
metadata:
  version: "1.0"
  works-best-with: "Reasoning on high effort; a client that can create files and run parallel subtasks"
  pairs-with: "moonlit-operator"
  updated: "2026-08-01"
```

All keys are optional, unknown keys are ignored, and absence renders nothing on the docs page. Phrasing is guidance ("works best with"), never a hard requirement: a skill degrades gracefully.

## Contributing

PRs welcome. Before merge, every skill must pass this checklist:

- [ ] Frontmatter parses: `name` equals the folder slug; `description` is one paragraph in plain language, reads correctly to a lawyer out of context, 300 to 600 characters
- [ ] Zero em-dashes and en-dashes anywhere in the file (grep for the U+2014 and U+2013 characters)
- [ ] No slop adjectives (robust, seamless, powerful, comprehensive, and their kin); be concrete
- [ ] No binary files unless the skill genuinely needs them; anything over about 100 KB gets questioned
- [ ] Description approved by Moonlit

The repo history is the changelog. The optional `version` and `updated` frontmatter fields are the user-facing signal; there is no semver ceremony.

## License

[MIT](LICENSE), Moonlit Legal Technologies B.V.
