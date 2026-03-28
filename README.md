# critique

A [Claude Code skill](https://docs.anthropic.com/en/docs/claude-code/skills) that performs adversarial review of plans, design docs, code, or projects — like a lawyer reviewing a contract on your behalf.

## What it does

When invoked with `/critique`, it reads the target material (code, design doc, recent commits), forms its own understanding, then reports findings ranked by severity:

1. **Showstoppers** — fundamentally wrong approaches, security issues, architectural mistakes
2. **Gaps** — missing error handling, unhandled edge cases, deferred decisions
3. **Inconsistencies** — contradictions between sections, shifting terminology
4. **Underspecified areas** — ambiguities where an implementer might guess wrong
5. **Suggestions** — simpler approaches, unnecessary complexity
6. **What looks good** — brief note on what's solid (calibrates trust)

It targets the review based on arguments you pass, or auto-detects the most recent work (design docs vs commits).

## Install

```bash
git clone https://github.com/dlowd/claude-skill-critique ~/.claude/skills/critique
```

## Usage

In Claude Code:

```
/critique                          # auto-detect most recent work
/critique path/to/file.py          # review a specific file
/critique "use of ffmpeg"          # review a topic across the codebase
/critique "commits from today"     # review recent changes
```

## Design principles

- **Be specific** — reference exact files, lines, and decisions, not vague "could be better"
- **Be honest about severity** — don't inflate minor issues to fill a list
- **Identify problems, don't rewrite** — the user wants to know what's wrong
- **Speculative findings must name a mechanism** — "this might be slow" isn't enough; name what breaks and how
- **Intentional decisions can still be wrong** — deliberateness doesn't get a pass

## Customization

The skill is a single `SKILL.md` file. Fork it and edit to match your review style — adjust severity categories, output format, ground rules, or the persona.

## License

MIT
