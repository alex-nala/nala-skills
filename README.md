# Nala skills

Skills for using your [Nala](https://usenala.co.uk) research in your own AI. Nala reads your interviews and feedback and does the counting: themes, who raised them, the quotes. These skills let your AI take that evidence further, combined with what it knows about your product: your analytics, your codebase, your roadmap.

## Install

**1. Add the skills** (Claude Code, Cursor, Codex, and any agent that reads Agent Skills):

```bash
npx skills add alex-nala/nala-skills
```

**2. Connect Nala's MCP server**, `https://mcp.usenala.co.uk/mcp`, and sign in when your AI asks. In Claude Code:

```bash
claude mcp add --transport http nala https://mcp.usenala.co.uk/mcp
```

Then type `/mcp`, choose nala and Authenticate. For other apps, Settings › AI apps in Nala shows the steps.

**Claude Code, in one step:** `/plugin marketplace add alex-nala/nala-skills`, then `/plugin install nala@nala-skills`. That adds the skills and connects the MCP server.

**claude.ai:** add Nala as a connector (Settings → Connectors → `https://mcp.usenala.co.uk/mcp`), then upload a skill's folder under Settings → Capabilities → Skills, with `using-nala` beside it.

## Skills

| Skill | What it does |
| --- | --- |
| [`synthesising-a-study`](skills/synthesising-a-study/SKILL.md) | Writes up a study's findings: each research question answered, the rest of the themes, what people ask for, and what to test next. |
| [`writing-a-case`](skills/writing-a-case/SKILL.md) | Writes a decision case from a study into Nala, as suggestions you keep or dismiss line by line. |
| [`identifying-opportunities`](skills/identifying-opportunities/SKILL.md) | Builds an opportunity solution tree from a study: the needs behind your outcome, each resting on Nala's evidence, and the one to work on first. |
| [`designing-ux-experiments`](skills/designing-ux-experiments/SKILL.md) | Turns a theme or request into the experiment that tests its riskiest assumption, with pass and fail criteria set before it runs. |
| [`planning-the-next-round`](skills/planning-the-next-round/SKILL.md) | Finds what the study left open and turns it into questions to test, who to talk to next, and an interview guide. |
| [`checking-claims`](skills/checking-claims/SKILL.md) | Checks a PRD, deck or message against a study, and rewrites what says more than the research shows. |
| [`tidying-a-study`](skills/tidying-a-study/SKILL.md) | Suggests interview snapshots and sub-theme names on a study's own pages in Nala. |
| [`using-nala`](skills/using-nala/SKILL.md) | The rules every skill follows: Nala's tools, how to give its counts and cite its quotes. Install it with the others. |

## How these skills keep your research honest

Every skill follows the same rule for where a claim comes from. Each claim is one of:

- **From Nala:** a count with its denominator ("7 of 18 people") and a link back to the theme or quote, so anyone can check it.
- **From your data:** something your AI found in your analytics, code or docs, with its source named.
- **Inference:** your AI's reading, said as one.

Interviews show that a problem exists and what it's like; they can't tell you how common it is across your users. Where a skill needs reach, it gets it from your data, never by scaling up an interview count.

Whatever a skill writes into Nala lands as a suggestion. Someone on your team keeps it or dismisses it; nothing is published until they do.

## License

MIT
