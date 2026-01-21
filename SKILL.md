---
name: pyenv
description: Manage Python versions with pyenv (Linux/macOS) and pyenv-win (Windows). Use when installing Python versions, switching between Python versions, or troubleshooting Python version issues.
argument-hint: [command]
---

# pyenv - Python Version Management

pyenv allows you to easily switch between multiple versions of Python. This skill covers both **pyenv** (Linux/macOS) and **pyenv-win** (Windows).

## Platform Detection

First, determine which platform you're working with:
- **Linux/macOS**: Use `pyenv` (original project)
- **Windows**: Use `pyenv-win` (native Windows fork) OR use WSL with regular pyenv

---

## Linux/macOS (pyenv)

### Installation

#### Automatic Installer (Recommended)
```bash
curl -fsSL https://pyenv.run | bash
```

#### Manual GitHub Checkout
```bash
git clone https://github.com/pyenv/pyenv.git ~/.pyenv
cd ~/.pyenv && src/configure && make -C src
```

#### Homebrew (macOS)
```bash
brew update
brew install pyenv
```

### Shell Configuration

**Bash** - Add to `~/.bashrc` AND `~/.bash_profile` or `~/.profile`:
```bash
export PYENV_ROOT="$HOME/.pyenv"
[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init - bash)"
```

**Zsh** - Add to `~/.zshrc`:
```bash
export PYENV_ROOT="$HOME/.pyenv"
[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init - zsh)"
```

**Fish** - Add to `~/.config/fish/config.fish`:
```bash
set -Ux PYENV_ROOT $HOME/.pyenv
test -d $PYENV_ROOT/bin; and fish_add_path $PYENV_ROOT/bin
pyenv init - fish | source
```

After configuring, restart your shell:
```bash
exec "$SHELL"
```

### Common Commands

| Command | Description |
|---------|-------------|
| `pyenv install -l` | List all available Python versions |
| `pyenv install 3.12.0` | Install Python 3.12.0 |
| `pyenv install 3.12` | Install latest 3.12.x version |
| `pyenv versions` | List all installed versions |
| `pyenv version` | Show current active version |
| `pyenv global 3.12.0` | Set global default version |
| `pyenv local 3.11.0` | Set version for current directory |
| `pyenv shell 3.10.0` | Set version for current shell session |
| `pyenv uninstall 3.10.0` | Remove a Python version |
| `pyenv which python` | Show which Python executable is being used |
| `pyenv rehash` | Rebuild shim binaries (after installing pip packages) |

### Version Selection Priority

pyenv selects Python version in this order:
1. `PYENV_VERSION` environment variable (set via `pyenv shell`)
2. `.python-version` file in current directory (set via `pyenv local`)
3. Parent directory `.python-version` files
4. `$(pyenv root)/version` file (set via `pyenv global`)
5. System Python

---

## Windows (pyenv-win)

### Installation Methods

#### Method 1: PowerShell Install (Recommended)
```powershell
Invoke-WebRequest -UseBasicParsing -Uri "https://raw.githubusercontent.com/pyenv-win/pyenv-win/master/pyenv-win/install-pyenv-win.ps1" -OutFile "./install-pyenv-win.ps1"; &"./install-pyenv-win.ps1"
```

#### Method 2: Git Checkout
```powershell
git clone https://github.com/pyenv-win/pyenv-win.git "%USERPROFILE%\.pyenv"
```

#### Method 3: ZIP Download
1. Download from: https://github.com/pyenv-win/pyenv-win/releases
2. Extract to `%USERPROFILE%\.pyenv`

### PATH Configuration

Add to PATH in order:
1. `%USERPROFILE%\.pyenv\pyenv-win\bin`
2. `%USERPROFILE%\.pyenv\pyenv-win\shims`

**PowerShell** - Add to `$PROFILE`:
```powershell
[System.Environment]::SetEnvironmentVariable('PYENV',$env:USERPROFILE + '\.pyenv\pyenv-win','User')
$path = [System.Environment]::GetEnvironmentVariable('PATH','User')
[System.Environment]::SetEnvironmentVariable('PATH', $path + ';C:\Users\YourUsername\.pyenv\pyenv-win\bin;C:\Users\YourUsername\.pyenv\pyenv-win\shims','User')
```

Restart your terminal after configuration.

### Common Commands (pyenv-win)

Most commands mirror the Linux pyenv commands but use Windows-style executable names:

| Command | Description |
|---------|-------------|
| `pyenv --help` | Show all available commands |
| `pyenv install -l` | List available Python versions |
| `pyenv install 3.12.0` | Install Python 3.12.0 |
| `pyenv install 3.12` | Install latest 3.12.x version |
| `pyenv versions` | List installed versions |
| `pyenv global 3.12.0` | Set global version |
| `pyenv local 3.11.0` | Set version for current directory |
| `pyenv shell 3.10.0` | Set version for current session |
| `pyenv uninstall 3.10.0` | Remove a version |
| `pyenv rehash` | Refresh shims |
| `pyenv which python` | Show which Python is being used |
| `pyenv whence <command>` | Show all versions with command |

### pyenv-win Specific Features

- Automatically installs both `python` and `pythonX` (e.g., `python3.12`) shims
- Installs `pip` and `pipX` shims
- Supports architectural filtering (`--arch` flag for 32/64-bit)

---

## WSL (Windows Subsystem for Linux)

When using WSL, treat it as Linux and use regular `pyenv`:
- Follow the Linux/macOS instructions
- The installed Python will be Linux binaries, not Windows binaries

---

## Build Dependencies

Before installing Python on Linux, install build dependencies:

**Ubuntu/Debian:**
```bash
sudo apt-get update
sudo apt-get install -y make build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm \
libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev \
libffi-dev liblzma-dev
```

**Fedora/CentOS/RHEL:**
```bash
sudo dnf install -y gcc make patch zlib-devel bzip2 bzip2-devel \
readline-devel sqlite sqlite-devel openssl-devel tkinter \
libffi-devel xz-devel
```

**macOS:**
```bash
brew install openssl readline sqlite3 xz zlib
```

---

## Troubleshooting

### "command not found: pyenv"
- Ensure shell configuration is correct
- Restart your shell or run `source ~/.bashrc` (or appropriate config file)
- Verify `PYENV_ROOT` is set correctly

### Python build fails
- Install build dependencies (see above)
- Check for common build problems: https://github.com/pyenv/pyenv/wiki/Common-build-problems
- Try installing a different version

### Wrong Python version being used
- Check `pyenv version` to see active version
- Check `which python` to see executable path
- Verify `.python-version` file contents in current directory
- Run `pyenv rehash` after installing new packages

### Switching between versions
- Use `pyenv shell <version>` for temporary change
- Use `pyenv local <version>` for project-specific version
- Use `pyenv global <version>` for system-wide default
- Use "system" to revert to system Python

### pyenv-win specific issues
- Run PowerShell as Administrator during installation
- Manually verify PATH entries in System Environment Variables
- Restart terminal after installation
- Check that shims directory exists: `$env:USERPROFILE\.pyenv\pyenv-win\shims`

---

## Uninstallation

### Linux/macOS
```bash
# Remove pyenv configuration from shell startup files
# Then remove the directory:
rm -rf $(pyenv root)
```

### Windows
1. Remove pyenv-win entries from PATH in System Environment Variables
2. Remove the directory: `rmdir /s %USERPROFILE%\.pyenv`
3. Restart terminal

---

## Best Practices

1. **Always set a local version per project** using `pyenv local <version>` - this creates a `.python-version` file
2. **Use `.python-version` files** in your projects for team consistency
3. **Pin to specific versions** (e.g., `3.11.4`) rather than major versions (e.g., `3.11`) for reproducibility
4. **Combine with virtual environments** using `pyenv-virtualenv` plugin or Python's built-in `venv`
5. **Run `pyenv rehash`** after installing packages that provide executables

---

## Virtual Environments

pyenv works well with virtual environments:

### Using Python's built-in venv
```bash
# First ensure correct Python version is active
pyenv local 3.11.0

# Create virtual environment
python -m venv .venv

# Activate (Linux/macOS)
source .venv/bin/activate

# Activate (Windows)
.venv\Scripts\Activate.ps1
```

### Using pyenv-virtualenv plugin
```bash
# Install plugin
git clone https://github.com/pyenv/pyenv-virtualenv.git $(pyenv root)/plugins/pyenv-virtualenv

# Create virtual environment
pyenv virtualenv 3.11.0 myproject

# Activate
pyenv local myproject
```

---

## Quick Reference

```bash
# Quick start - Linux/macOS
curl -fsSL https://pyenv.run | bash
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo '[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(pyenv init - bash)"' >> ~/.bashrc
exec "$SHELL"
pyenv install 3.12.0
pyenv global 3.12.0

# Quick start - Windows (PowerShell)
Invoke-WebRequest -UseBasicParsing -Uri "https://raw.githubusercontent.com/pyenv-win/pyenv-win/master/pyenv-win/install-pyenv-win.ps1" -OutFile "./install-pyenv-win.ps1"; &"./install-pyenv-win.ps1"
# Then add to PATH and restart terminal
pyenv install 3.12.0
pyenv global 3.12.0
```

---

## Additional Resources

- pyenv GitHub: https://github.com/pyenv/pyenv
- pyenv-win GitHub: https://github.com/pyenv-win/pyenv-win
- pyenv wiki: https://github.com/pyenv/pyenv/wiki
- Common build problems: https://github.com/pyenv/pyenv/wiki/Common-build-problems
