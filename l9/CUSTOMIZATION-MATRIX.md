# Fork Customization Matrix

What stays upstream vs. what L9 overlays. Keeps the fork rebase-clean.

| Concern | Owner | Where | Rebase-safe? |
|---|---|---|---|
| Agent loop / context mgmt | upstream Goose | Rust core | yes (don't touch) |
| MCP client / ACP daemon | upstream Goose | Rust core | yes (don't touch) |
| Recipes & subrecipes | L9 overlay | `~/.config/goose/recipes/` | yes |
| Skills | L9 overlay | `~/.config/goose/skills/` | yes |
| Provider / model | L9 overlay | `l9/config.yaml` → copy to `~/.config/goose/` | yes |
| Extension permissions (HITL) | L9 overlay | `l9/config.yaml` | yes |
| Planner/Generator/Evaluator flock | L9 overlay | `l9/recipes/` | yes |
| Golden principles / drift sigs | L9 pack | `docs/`, `ops/` | yes |

## Rule
If a change requires editing Goose's Rust source, stop and ask whether a recipe, skill,
or MCP extension can express it instead. Source edits break rebases and forfeit the
commodity-runtime advantage. Almost all L9 behavior is expressible as config + recipes.

## Upstream sync cadence
Run the rebase weekly, or before any production deployment:
```bash
git fetch upstream && git rebase upstream/main
```
