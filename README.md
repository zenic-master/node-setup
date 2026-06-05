# Node.js Environment Setup (Windows)

## Installed Software

| Tool | Version |
|------|---------|
| nvm-windows | 1.2.2 |
| Node.js | v22.22.3, v24.16.0 |
| npm | 11.16.0 (Node 24), 10.9.8 (Node 22) |

## Key Paths

- **NVM_HOME**: `C:\Users\Owner\AppData\Local\nvm`
- **NVM_SYMLINK**: `C:\nvm4w\nodejs`

## nvm-windows Usage

### List installed versions

```powershell
nvm list
```

### List available versions for download

```powershell
nvm list available
```

### Install a new version

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

npm is installed per Node version. To update npm for the currently active version:

```powershell
npm install -g npm@latest
```

Switching Node versions will revert to that version's bundled npm.

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
