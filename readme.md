# Dot Files

## Symlink Setup

To keep your Claude instructions synced with this repo, create a symlink from your user profile to this file.

### Windows (Command Prompt as Administrator)

Run from the repo root:

```cmd
mkdir "%USERPROFILE%\.claude"
mklink "%USERPROFILE%\.claude\CLAUDE.md" "%CD%\CLAUDE.md"
```

### Windows (PowerShell as Administrator)

Run from the repo root:

```powershell
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.claude"
New-Item -ItemType SymbolicLink -Path "$env:USERPROFILE\.claude\CLAUDE.md" -Target "$PWD\CLAUDE.md"
```

### macOS / Linux

Run from the repo root:

```bash
mkdir -p ~/.claude
ln -s "$PWD/CLAUDE.md" ~/.claude/CLAUDE.md
```

## Helpful Links
 - [Setup VSCode Like Neovim by Lazar Nikolov](https://www.youtube.com/watch?v=JRnwt7oT1ZE)
 - [Delete outdated local branches with the prune git option and the branch delete command](https://dillionmegida.com/p/delete-outdated-branches/)