# dotfiles

chezmoi manages the files and mise manages the tools. Frontend setup: zsh, git, node/pnpm via mise, and CLI essentials.

## New machine

```sh
sh -c "$(curl -fsLS get.chezmoi.io)" -- -b ~/.local/bin init --apply --source ~/projects/dotfiles byrchenko
```

This installs chezmoi, clones this repo into `~/projects/dotfiles`, and applies it.

You'll be asked for your git name and email (Enter keeps byrch / byrchenko@gmail.com) and your sudo password (for apt and chsh). Then open a new terminal.

## Day to day

| Task | Command |
|---|---|
| Add a global tool | `chezmoi edit ~/.config/mise/config.toml`, then `chezmoi apply` |
| Edit a dotfile | `chezmoi edit ~/.zshrc`, then `chezmoi apply` |
| Start tracking a file | `chezmoi add ~/.config/whatever` |
| Pin node for a project | `mise use node@22` in the project (or keep its `.nvmrc`) |
| Pull changes on another machine | `chezmoi update` |
| Save changes | `cd ~/projects/dotfiles && git add -A && git commit -m "..." && git push` |

## Layout

- `dot_zshrc`: zsh config (history, completion, mise, starship, zoxide, fzf, aliases)
- `dot_gitconfig.tmpl`: git config. Name and email are asked on init. On WSL it uses the Windows credential manager.
- `dot_config/mise/config.toml`: global tools (node LTS, pnpm, gh, lazygit, ripgrep, ...)
- `.chezmoiexternal.toml`: zsh plugins, cloned straight from GitHub
- `run_onchange_before_10-install-packages.sh.tmpl`: apt packages and default shell
- `run_onchange_after_20-mise-install.sh.tmpl`: installs mise and runs `mise install` when the tool list changes
