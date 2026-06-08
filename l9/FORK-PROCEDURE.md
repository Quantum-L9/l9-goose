# Forking & Fully Configuring Goose for L9

This is the exact, runnable procedure. The agent runtime stays upstream Goose (you do NOT
need to modify Rust source); all L9 behavior lives in config + recipes that overlay on top.

## 1. Fork is done
Your fork lives at https://github.com/cryptoxdog/goose

## 2. Build the binary (optional — prebuilt also works)
```bash
# Rust toolchain required
cargo build --release
# or install the released CLI:
curl -fsSL https://github.com/block/goose/releases/download/stable/download_cli.sh | bash
```

## 3. Apply the L9 config overlay
Config + recipes resolve from `~/.config/goose/`.

```bash
mkdir -p ~/.config/goose/recipes
cp l9/config.yaml ~/.config/goose/config.yaml
export GOOSE_RECIPE_PATH="$HOME/.config/goose/recipes"
```

## 4. Set provider + keys (model is replaceable per L9 Kernel §0)
```bash
goose configure        # interactive: pick provider, paste key
# or non-interactive env:
export GOOSE_PROVIDER=anthropic
export ANTHROPIC_API_KEY=sk-...   # or OLLAMA_HOST for local/air-gapped
```

## 5. Validate then run
```bash
goose session start
# or with a recipe:
goose run --recipe ~/.config/goose/recipes/exec-plan.yaml \
  --params task_slug=add-odoo-contract-risk-flags --interactive
```

## 6. Keep the fork current
```bash
git remote add upstream https://github.com/block/goose.git
git fetch upstream && git rebase upstream/main
```
