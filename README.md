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

## Install on Windows

Config lives in `%APPDATA%\Zed\` (Roaming — *not* `%LOCALAPPDATA%`, which is
where Zed keeps extensions and other data). PowerShell:

```powershell
git clone git@github.com:tomdapchai/zed-config.git $HOME\repo\personal\zed-config
$src = "$HOME\repo\personal\zed-config"
$dst = "$env:APPDATA\Zed"
New-Item -ItemType Directory -Force -Path $dst | Out-Null
Copy-Item "$src\settings.json" "$dst\settings.json" -Force
Copy-Item "$src\keymap.json"   "$dst\keymap.json"   -Force
```

Want the same live-sync symlinks as macOS? Turn on **Settings → System → For
developers → Developer Mode** (lets a normal user create symlinks; otherwise run
PowerShell as admin), then swap the two `Copy-Item` lines for:

```powershell
New-Item -ItemType SymbolicLink -Path "$dst\settings.json" -Target "$src\settings.json" -Force
New-Item -ItemType SymbolicLink -Path "$dst\keymap.json"   -Target "$src\keymap.json"   -Force
```

Restart Zed either way.

## Not in here

- `prompts/` — local LMDB of the AI prompt library, binary machine state.
- `themes/` — empty; themes come from the extensions above.
- API keys — Zed stores those in the OS keychain, not in `settings.json`.
- `settings_backup.json` — old local backup.

## Machine-specific bits to fix after cloning

`agent.tool_permissions.terminal.always_allow` contains an absolute path
(`/Users/tam.vo/repo/company/document-validator`). Adjust or drop it per machine.
