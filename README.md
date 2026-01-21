# pyenv Skill for Claude Code

A Claude Code skill that helps manage Python versions using **pyenv** (Linux/macOS) and **pyenv-win** (Windows).

Credit to (pyenv)[https://github.com/pyenv/pyenv], it's a fantastic project

## What is pyenv?

pyenv is a simple Python version management tool that lets you:
- Switch between multiple Python versions easily
- Set project-specific Python versions
- Install and uninstall Python versions
- Manage global, local, and shell-specific Python versions

## What This Skill Does

This skill enables Claude Code to help you with:
- Installing pyenv on Linux, macOS, or Windows
- Setting up shell configuration (Bash, Zsh, Fish, PowerShell)
- Installing specific Python versions
- Switching between Python versions (`global`, `local`, `shell`)
- Troubleshooting common pyenv issues
- Understanding version selection priority
- Integrating with virtual environments

## Installation

### Option 1: Clone to User Skills Directory (Recommended)

```bash
# Create the skills directory if it doesn't exist
mkdir -p ~/.claude/skills

# Clone this repository
git clone https://github.com/yourusername/pyenv-skill.git ~/.claude/skills/pyenv
```

### Option 2: Clone to Project Skills Directory

```bash
# Create the skills directory in your project
mkdir -p .claude/skills

# Clone this repository
git clone https://github.com/yourusername/pyenv-skill.git .claude/skills/pyenv
```

### Option 3: Manual Installation

1. Download `SKILL.md` from this repository
2. Place it in either:
   - `~/.claude/skills/pyenv/SKILL.md` (user-wide)
   - `.claude/skills/pyenv/SKILL.md` (project-specific)

## Usage

Once installed, Claude Code will automatically load this skill when relevant. You can:

1. **Let Claude detect it automatically** - Mention Python version management or pyenv
2. **Invoke directly** - Type `/pyenv` in your Claude Code session

### Example Conversations

```
You: I want to install Python 3.12 on my Mac
Claude: [Uses pyenv skill to guide you through installation]

You: Switch my project to Python 3.11
Claude: [Uses pyenv skill to run 'pyenv local 3.11']

You: pyenv isn't working, command not found
Claude: [Uses pyenv skill to troubleshoot PATH and shell configuration]
```

## Quick Start (pyenv itself)

This skill manages pyenv, but you also need to install pyenv itself:

### Linux/macOS
```bash
curl -fsSL https://pyenv.run | bash
# Add to your shell config, then restart shell
```

### Windows (PowerShell)
```powershell
Invoke-WebRequest -UseBasicParsing -Uri "https://raw.githubusercontent.com/pyenv-win/pyenv-win/master/pyenv-win/install-pyenv-win.ps1" -OutFile "./install-pyenv-win.ps1"
&"./install-pyenv-win.ps1"
```

## Supported Platforms

| Platform | Tool | Status |
|----------|------|--------|
| Linux | pyenv | Fully Supported |
| macOS | pyenv | Fully Supported |
| Windows | pyenv-win | Fully Supported |
| WSL | pyenv | Fully Supported |

## Resources

- [pyenv GitHub](https://github.com/pyenv/pyenv)
- [pyenv-win GitHub](https://github.com/pyenv-win/pyenv-win)
- [Claude Code Skills Documentation](https://code.claude.com/docs/en/skills)

## License

MIT

## Contributing

Contributions welcome! Feel free to submit issues or pull requests.
