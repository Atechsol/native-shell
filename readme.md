# Native Shell

**A lightweight skin for macOS Terminal.app.** Modern keyboard editing, better history, a clean developer prompt and good-looking presets, without replacing your terminal.

Native Shell keeps you in the Terminal.app you already have. It configures Zsh, the Zsh line editor (ZLE) and Terminal.app profiles. It runs no background process, has no runtime dependencies, and everything it changes can be undone.

> **Status:** early development (v0.x). Things will change. Feedback and issues are welcome.

---

## Install

Pick whichever suits you. All three run the same installer and give the same result.

**No dependencies (recommended)**
```sh
zsh <(curl -fsSL nativeshell.sh)
```

**With Node**
```sh
npx nativeshell
```

**With Homebrew**
```sh
brew install aleem/tap/nativeshell && nativeshell setup
```

Setup will:
1. Back up your `~/.zshrc` and Terminal.app preferences
2. Ask you to pick a skin
3. Add **one** guarded line to `~/.zshrc`
4. Import the chosen Terminal.app profile

Open a new Terminal window when it finishes. To skip the questions, use `nativeshell setup --yes`.

---

## Features

**Keyboard editing** (done in ZLE, so it only applies at the shell prompt)

| Shortcut | Action |
|---|---|
| `⌥ ←` / `⌥ →` | Move by word |
| `⌘ ←` / `⌘ →` | Start / end of line* |
| `⌥ ⌫` | Delete previous word |
| `⌘ ⌫` | Delete to start of line* |
| `⇧` + any of the above | Select* |

\* Depends on what Terminal.app can pass through. Run `nativeshell doctor` to see what works on your Mac.

**Shell**
- Better history search (prefix-matching `↑`/`↓`, incremental search)
- Optional minimal prompt with Git branch and status
- Each feature can be turned on or off on its own

**Skins**
- Developer presets for Terminal.app: font, colors, cursor, window size, scrollback
- Your own changes survive updates

**Coding agents**
- Claude Code, Codex, Gemini CLI and other CLI agents run normally
- Optional vendor-neutral launch aliases

---

## Usage

```sh
nativeshell setup               # first-time setup (interactive)
nativeshell theme list          # list available skins
nativeshell theme apply <name>  # switch skin
nativeshell config edit         # open ~/.nativeshell/config.json
nativeshell apply               # re-apply config (safe to run repeatedly)
nativeshell doctor              # show active config and detect problems
nativeshell uninstall           # restore your backups and remove Native Shell
```

---

## What it touches

Native Shell tells you exactly what it changes:

| File | Change |
|---|---|
| `~/.zshrc` | One line that sources `~/.nativeshell/init.zsh` (skipped safely if missing or broken) |
| `~/.nativeshell/` | Config, generated scripts, skins and backups |
| Terminal.app preferences | An imported Native Shell profile, optionally set as the default |

No `sudo`. No daemons. No other files.

---

## Compatibility

- **macOS** with Terminal.app and Zsh (the default shell since Catalina)
- Works with SSH, tmux, Vim, Nano, less and other full-screen apps. Bindings only apply at the Zsh prompt.
- Designed to coexist with Oh My Zsh, Starship and Powerlevel10k (compatibility work in progress)

---

## Privacy

- Your commands, history, environment variables and files are **never** sent anywhere.
- Core features need no network connection.
- No telemetry.

---

## Principles

- **Enhance the terminal you have, don't replace it.** No custom terminal engine (PTY) or renderer.
- **Zero overhead.** Target is under 50 ms added to shell startup, and no background processes.
- **Safe by default.** Backups before every change, re-running never duplicates anything, and a broken config never breaks your shell.
- **Honest limits.** If Terminal.app can't do something reliably, we say so instead of faking it.

---

## Roadmap

- [ ] Installer with backup and restore
- [ ] ZLE navigation, deletion and selection widgets
- [ ] History search improvements
- [ ] Minimal Git prompt
- [ ] First skin presets
- [ ] `doctor` diagnostics
- [ ] Homebrew tap and npm package
- [ ] Settings UI that doesn't stay running in the background
- [ ] Adapters for other terminals (Ghostty, iTerm2)

---

## Uninstall

```sh
nativeshell uninstall
```

This restores your original `~/.zshrc` and Terminal.app preferences from backup. If the command itself is missing:

```sh
zsh ~/.nativeshell/bin/nativeshell uninstall
```

---

## Contributing

Issues and pull requests are welcome. Please include your macOS version and the output of `nativeshell doctor` when reporting bugs.

## License

MIT © Boehmtech