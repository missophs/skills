# Skills Setup

How this repo connects to Claude Code and other agents.

## How Claude Code reads these skills

Claude Code reads skills from `~/.claude/skills/` — which is a git clone of this repo (`github.com/missophs/skills`).

**To update skills after pushing changes:**

```bash
cd ~/.claude/skills && git pull origin webhooks
```

Then restart your Claude Code session. Skills appear as `/skill-name` commands.

> **Note:** `npx skills add missophs/skills` installs to the local project's `.agents/` directory, which works for Codex/Copilot but NOT for Claude Code's global `/` commands. Always use the `git pull` method above for Claude Code.

---

## Repo structure

Each skill lives at the root level:

```
<skill-name>/SKILL.md
```

The `npx skills` CLI auto-discovers `SKILL.md` files one level deep at the repo root. Do NOT nest under a `skills/` subdirectory — that breaks auto-discovery.

### Current skills

| Slash command | File |
|---|---|
| `/caveman` | `caveman/SKILL.md` |
| `/api-design` | `api-design/SKILL.md` |
| `/frontend-developer` | `frontend-developer/SKILL.md` |
| `/llm-council` | `llm-council/SKILL.md` |
| `/chro` | `chro/SKILL.md` |
| `/hrbp` | `hrbp/SKILL.md` |
| `/caveman-commit` | `caveman-commit/SKILL.md` |
| `/caveman-review` | `caveman-review/SKILL.md` |
| `/morning-email-digest` | `morning-email-digest/SKILL.md` |
| `/generium-design-kit` | `generium-design-kit/SKILL.md` |

---

## Adding a new skill

1. Create `<skill-name>/SKILL.md` with YAML frontmatter:
   ```yaml
   ---
   name: skill-name
   description: When to use this skill (one sentence).
   ---
   ```
2. Add an entry to `.claude-plugin/manifest.json`
3. Commit and push to `webhooks` branch
4. Run: `cd ~/.claude/skills && git pull origin webhooks`
5. Restart Claude Code — skill appears as `/skill-name`

### Large file note

`npx skills add` silently skips files over ~50KB. If a skill is large (like `chro` or `hrbp`), manually copy it:

```bash
mkdir -p ~/.claude/skills/<skill-name>
cp <skill-name>/SKILL.md ~/.claude/skills/<skill-name>/SKILL.md
```

---

## .gitignore

`.agents/` is gitignored — it's the project-scoped install directory created by `npx skills add` and is not needed in the repo.
