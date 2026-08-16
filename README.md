# zed-config

My Zed editor config. Machine-independent parts only.

| File | What |
|---|---|
| `settings.json` | Zed settings + `auto_install_extensions` (extensions reinstall themselves) |
| `keymap.json` | Key bindings |

## Install on a new machine (macOS / Linux)

```sh
git clone git@github.com:tomdapchai/zed-config.git ~/repo/personal/zed-config
mkdir -p ~/.config/zed
ln -sf ~/repo/personal/zed-config/settings.json ~/.config/zed/settings.json
ln -sf ~/repo/personal/zed-config/keymap.json   ~/.config/zed/keymap.json
```

Restart Zed. It installs the extensions listed in `auto_install_extensions` on
its own. Symlinks mean edits made in Zed land straight in the repo — just commit.

Prefer no symlinks? `cp` instead of `ln -sf`, then re-copy by hand after changes.

Windows: config path is `%APPDATA%\Zed\` instead of `~/.config/zed/`.

## Not in here

- `prompts/` — local LMDB of the AI prompt library, binary machine state.
- `themes/` — empty; themes come from the extensions above.
- API keys — Zed stores those in the OS keychain, not in `settings.json`.
- `settings_backup.json` — old local backup.

## Machine-specific bits to fix after cloning

`agent.tool_permissions.terminal.always_allow` contains an absolute path
(`/Users/tam.vo/repo/company/document-validator`). Adjust or drop it per machine.
