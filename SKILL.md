---
name: pyenv
description: Manage Python versions with pyenv (Linux/macOS) and pyenv-win (Windows). Use when installing Python versions, switching between Python versions, or troubleshooting Python version issues.
argument-hint: [command]
---

# pyenv - Python Version Management

**Linux/macOS**: `pyenv` | **Windows**: `pyenv-win` | **WSL**: use `pyenv`

## Installation

**Linux/macOS:**
```bash
curl -fsSL https://pyenv.run | bash
# Or: brew install pyenv (macOS)
```

**Windows (PowerShell):**
```powershell
Invoke-WebRequest -UseBasicParsing -Uri "https://raw.githubusercontent.com/pyenv-win/pyenv-win/master/pyenv-win/install-pyenv-win.ps1" -OutFile "./install-pyenv-win.ps1"; &"./install-pyenv-win.ps1"
```

## Shell Configuration

**Bash (`~/.bashrc`)**: `eval "$(pyenv init - bash)"`
**Zsh (`~/.zshrc`)**: `eval "$(pyenv init - zsh)"`
**Fish (`~/.config/fish/config.fish`)**: `pyenv init - fish | source`

Also add:
```bash
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
```

**Windows PATH**: Add `%USERPROFILE%\.pyenv\pyenv-win\bin` and `%USERPROFILE%\.pyenv\pyenv-win\shims`

Restart shell after configuration.

## Commands

| Command | Description |
|---------|-------------|
| `pyenv install -l` | List available versions |
| `pyenv install <ver>` | Install version |
| `pyenv versions` | List installed |
| `pyenv version` | Show current |
| `pyenv global <ver>` | Set system default |
| `pyenv local <ver>` | Set for current directory |
| `pyenv shell <ver>` | Set for session |
| `pyenv uninstall <ver>` | Remove version |
| `pyenv rehash` | Refresh shims |
| `pyenv which python` | Show executable path |

## Version Priority

1. `PYENV_VERSION` env var (`pyenv shell`)
2. `.python-version` file (`pyenv local`)
3. Parent `.python-version` files
4. `$(pyenv root)/version` (`pyenv global`)
5. System Python

## Build Dependencies (Linux)

**Ubuntu/Debian:**
```bash
sudo apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev
```

**Fedora/CentOS:**
```bash
sudo dnf install -y gcc make patch zlib-devel bzip2 bzip2-devel readline-devel sqlite sqlite-devel openssl-devel tkinter libffi-devel xz-devel
```

**macOS:** `brew install openssl readline sqlite3 xz zlib`

## Virtual Environments

```bash
pyenv local 3.11.0
python -m venv .venv
source .venv/bin/activate  # Linux/macOS
.venv\Scripts\Activate.ps1  # Windows
```

**pyenv-virtualenv plugin:**
```bash
git clone https://github.com/pyenv/pyenv-virtualenv.git $(pyenv root)/plugins/pyenv-virtualenv
pyenv virtualenv 3.11.0 myproject
pyenv local myproject
```

## Troubleshooting

| Issue | Solution |
|-------|----------|
| `command not found` | Check shell config, restart shell, verify `PYENV_ROOT` |
| Build fails | Install build dependencies, check [common problems](https://github.com/pyenv/pyenv/wiki/Common-build-problems) |
| Wrong version | Check `pyenv version`, `which python`, `.python-version` file |
| pyenv-win issues | Run PowerShell as Admin, verify PATH, restart terminal |

## Uninstallation

**Linux/macOS:** `rm -rf $(pyenv root)` (remove config from shell first)
**Windows:** Remove PATH entries, then `rmdir /s %USERPROFILE%\.pyenv`

## Resources

- https://github.com/pyenv/pyenv
- https://github.com/pyenv-win/pyenv-win
