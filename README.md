# learning-skills

A [Claude Code](https://code.claude.com/docs/en/plugins) plugin that bundles skills for
**capturing what you learn while coding** into one central, teachable knowledge base —
so notes are never scattered across project repos again.

All skills live under the `learning:` namespace:

| Skill | Command | What it does |
|-------|---------|--------------|
| capture | `/learning:capture` | Save a standalone, book-depth learning note into `~/Desktop/Learnings/`. |

_More learning skills (review, curate, …) will be added to the same namespace over time._

## Install (Claude Code plugin — namespaced)

```
/plugin marketplace add rimakes/learning-skills
/plugin install learning@rimakes-learning
```

Skills then appear as `learning:capture`, `learning:review`, etc.

## Install (skills.sh / any agent — single skill)

```
npx skills add rimakes/learning-skills
```

This installs the raw `SKILL.md` files (without the `learning:` namespace prefix, which is
a Claude Code plugin feature).

## Repo layout

```
learning-skills/
├── .claude-plugin/
│   ├── plugin.json          # the "learning" plugin (name = namespace prefix)
│   └── marketplace.json     # makes this repo an installable marketplace
└── skills/
    └── capture/
        └── SKILL.md         # → learning:capture
```

To add another skill, drop a new folder under `skills/` (e.g. `skills/review/SKILL.md`);
it automatically joins the `learning:` namespace — no manifest change needed.

## License

MIT © Ricardo Sala
