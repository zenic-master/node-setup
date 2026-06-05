# Node.js Environment Setup (Windows)

A reference guide for setting up and managing Node.js on Windows using [nvm-windows](https://github.com/coreybutler/nvm-windows). This documents the installation process, configuration, version management, and troubleshooting tips.

## Prerequisites

- **OS**: Windows 10/11 (x64)
- **Shell**: PowerShell 7+ recommended
- **Package manager**: [winget](https://learn.microsoft.com/en-us/windows/package-manager/winget/) (ships with Windows 11 and modern Windows 10)

## Installation

### 1. Install nvm-windows

```powershell
winget install CoreyButler.NVMforWindows --silent --accept-package-agreements --accept-source-agreements
```

> The installer requires admin elevation — accept the UAC prompt when it appears.
> Restart your terminal after installation for PATH changes to take effect.

### 2. Install Node.js versions

```powershell
nvm install 22        # LTS (v22.22.3)
nvm install 24        # Current (v24.16.0)
```

### 3. Activate a version

```powershell
nvm use 24.16.0       # Requires admin terminal
```

### 4. Update npm (optional)

```powershell
npm install -g npm@latest
```

### 5. Install GitHub CLI (optional)

```powershell
winget install GitHub.cli --silent --accept-package-agreements --accept-source-agreements
gh auth login
```

## Installed Software

| Tool | Version |
|------|---------|
| nvm-windows | 1.2.2 |
| Node.js | v22.22.3, v24.16.0 |
| npm | 11.16.0 (Node 24), 10.9.8 (Node 22) |
| GitHub CLI | 2.93.0 |

## Key Paths

- **NVM_HOME**: `C:\Users\Owner\AppData\Local\nvm` — where nvm and Node versions are stored
- **NVM_SYMLINK**: `C:\nvm4w\nodejs` — symlink pointing to the active Node version

## nvm-windows Command Reference

### List installed versions

```powershell
nvm list
```

### List available versions for download

```powershell
nvm list available
```

### Install a specific version

```powershell
nvm install 22        # latest 22.x
nvm install 24.16.0   # exact version
```

### Switch versions

> Requires an administrator terminal.

```powershell
nvm use 22.22.3   # Switch to Node 22
nvm use 24.16.0   # Switch to Node 24
```

### Check active version

```powershell
nvm current
node --version
npm --version
```

### Uninstall a version

```powershell
nvm uninstall 22.22.3
```

## Updating npm

npm is installed **per Node version**. To update npm for the currently active version:

```powershell
npm install -g npm@latest
```

To install a specific npm version:

```powershell
npm install -g npm@10.9.2
```

> Switching Node versions will revert to that version's bundled npm.

## Verification

To confirm the environment is working correctly:

```powershell
# Check versions
node --version
npm --version
nvm current

# Quick smoke test
node -e "console.log('Node.js ' + process.version + ' is working')"

# Test npm package management
mkdir test-project && cd test-project
npm init -y
npm install chalk
node -e "import('chalk').then(m => console.log(m.default.green('npm works')))"
cd .. && Remove-Item test-project -Recurse -Force
```

## Troubleshooting

### `nvm` not recognized after install

Restart your terminal, or refresh the PATH manually:

```powershell
$env:NVM_HOME = "C:\Users\Owner\AppData\Local\nvm"
$env:NVM_SYMLINK = "C:\nvm4w\nodejs"
$env:Path = "$env:NVM_HOME;$env:NVM_SYMLINK;$env:Path"
```

### `nvm use` fails with access denied

Run the terminal as Administrator. The `nvm use` command creates a symlink at `C:\nvm4w\nodejs` which requires elevated permissions.

### Node/npm not found after `nvm use`

Restart the terminal to pick up the updated symlink.

### npm warns about permissions

Avoid using `sudo` or running npm as admin for package installs. If global installs fail, check that `NVM_SYMLINK` is writable by your user.

### winget can't find older Node.js versions

winget only carries recent versions. Use nvm-windows to install any version:

```powershell
nvm install 18.20.0   # older LTS versions available via nvm
```

## License

ISC
