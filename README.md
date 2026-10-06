# addopencodeskill

CLI tool to install [OpenCode](https://opencode.ai) skills into any project directory.

Creates a project's `.opencode/skills/` folder with symlinked or copied skill directories, enabling per-project skill profiles.

## Install

```bash
# Clone and link to PATH
git clone https://github.com/ArifDharmawan/addopencodeskill.git
cd addopencodeskill
ln -s "$(pwd)/bin/addopencodeskill" ~/.local/bin/addopencodeskill
```

Or copy directly:

```bash
cp bin/addopencodeskill ~/.local/bin/
chmod +x ~/.local/bin/addopencodeskill
```

## Usage

```
addopencodeskill <project_dir> <skills_dir> [options]
```

### Options

| Flag | Description |
|------|-------------|
| `-c, --copy` | Copy skills (frozen snapshot) |
| `-s, --symlink` | Symlink skills (default, live updates from source) |
| `-f, --force` | Overwrite existing skills |
| `-n, --dry-run` | Preview without making changes |
| `--skills-filter` | Comma-separated glob/regex to install subset |
| `-h, --help` | Show help |

### Examples

```bash
# Install all backend skills into a project (symlinked)
addopencodeskill ~/works/github/nucleus ~/.config/opencode/skill-libraries/backend

# Copy skills so project has its own independent copies
addopencodeskill ~/chatpdf-backend ~/.config/opencode/skill-libraries/backend --copy

# Install only API-related skills
addopencodeskill ~/projects/app ~/.config/opencode/skill-libraries \
  --skills-filter "api-*,fastapi*,graphql"

# Preview what would be installed
addopencodeskill ~/repo ~/.config/opencode/skills --dry-run

# Overwrite existing skills
addopencodeskill ~/repo ~/.config/opencode/skills --force
```

## How it works

```
your-project/
└── .opencode/
    └── skills/
        ├── api-analyzer/          → symlink to source skill
        ├── fastapi-router-py/     → symlink to source skill
        └── .addopencodeskill-manifest  ← tracks what was installed
```

OpenCode automatically loads skills from `.opencode/skills/` when running in that project directory.

## Requirements

- Bash 4+
- `realpath`, `find`, `ln`, `cp` (standard Linux/macOS)
- OpenCode installed

## License

MIT
