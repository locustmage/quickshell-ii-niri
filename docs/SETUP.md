# Setup & Updates

## Install

```bash
git clone https://github.com/snowarch/quickshell-ii-niri.git
cd quickshell-ii-niri
./setup install
```

Add `-y` for non-interactive mode.

## Update

```bash
./setup update
```

Checks remote for updates, pulls changes, syncs QML code, restarts shell, and offers pending migrations. Creates a snapshot before updating for easy rollback.

## Doctor

```bash
./setup doctor
```

Diagnoses and **automatically fixes** common issues:
- Missing directories
- Script permissions
- Python packages (via uv)
- Version tracking
- File manifest
- Starts shell if not running

## Rollback

```bash
./setup rollback
```

Restore a previous snapshot if something breaks after an update. Shows available snapshots with dates and lets you choose which one to restore.

## Commands

| Command | Description |
|---------|-------------|
| `./setup` | Interactive menu |
| `./setup install` | Full installation |
| `./setup update` | Check remote, pull, sync, restart |
| `./setup doctor` | Diagnose and auto-fix |
| `./setup rollback` | Restore previous snapshot |
| `./setup uninstall` | Remove ii configs and safe-to-remove packages |

Options: `-y` (skip prompts), `-q` (quiet), `--no-packages` (uninstall only, do not remove packages), `-h` (help)

## What Gets Installed

| Source | Destination |
|--------|-------------|
| QML code | `~/.config/quickshell/ii/` |
| Niri config | `~/.config/niri/config.kdl` |
| ii config | `~/.config/illogical-impulse/config.json` |
| GTK/Qt themes | `~/.config/gtk-*/`, `~/.config/kdeglobals` |

On first install, existing configs are backed up. On updates, your configs are never touched - only QML code is synced.

## Migrations

Some features need config changes (new keybinds, layer rules, etc). After `update`, you're asked if you want to apply pending migrations. Each shows exactly what will change, with automatic backup.

## Backups

- Install backups: `~/ii-niri-backup/`
- Update backups: `~/.local/state/quickshell/backups/`

## Uninstall

Preferred method (safe and reversible):

```bash
./setup uninstall
```

Configs-only uninstall (leave all packages installed):

```bash
./setup uninstall --no-packages
```

The uninstall command will:
- stop the ii shell if it is running
- remove ii's configuration and state files
- optionally remove ii-related packages that are **not** required by anything else on your system (unless `--no-packages` is passed)

If you prefer to uninstall manually:

```bash
# Stop ii from starting
# Comment out in ~/.config/niri/config.kdl:
# spawn-at-startup "qs" "-c" "ii"

# Remove configs
rm -rf ~/.config/quickshell/ii
rm -rf ~/.config/illogical-impulse
```
