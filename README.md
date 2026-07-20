# 🔧 OpenCode Setup

A minimal, modern development environment powered by Bun, Node.js, and the OpenCode CLI, with a fast terminal and a plugin-based workflow on top.
Follow the steps below to get everything installed and configured.

---

## 🛠 Command‑Line Tools

- [ ] **Bun**
  ```powershell
  powershell -c "irm bun.sh/install.ps1 | iex"
  ```
  *On macOS/Linux, install with `curl -fsSL https://bun.sh/install | bash`.*
- [ ] **nodejs** (via Chocolatey on Windows)  
  ```powershell
  choco install nodejs
  ```
  *On macOS/Linux consider [`fnm`](https://github.com/Schniz/fnm) or `nvm` for nodejs.*
- [ ] **OpenCode**
  ```bash
  npm install -g opencode-ai@latest
  ```
  *Works the same on macOS/Linux — just run the command above in your terminal.*
- [ ] **ast-grep**
  ```bash
  npm install -g @ast-grep/cli
  ```
  *Same command on macOS and Linux.*

---

## 🖥 Terminal & Shell

- [ ] **Alacritty** or **Kitty** (Unix)
  - Alacritty: [alacritty.org](https://alacritty.org/)
  - Kitty: [sw.kovidgoyal.net/kitty](https://sw.kovidgoyal.net/kitty/)
- [ ] **Windows Terminal** (Windows)
  - Windows Terminal: (preinstalled or from the Microsoft Store)
  - [ ] **PowerShell (`pwsh`)**
    ```powershell
    # Windows (if not already installed)
    winget install --id Microsoft.PowerShell
    ```

---

## 🔌 OpenCode Plugins

The author uses preconfigured plugins to streamline the coding experience:

- **OmO Ultimate** — multi-agent orchestration for OpenCode, mixing models across providers
- **OmO-slim** — a leaner, token-efficient fork of oh-my-opencode
- **DCP** — dynamic context pruning that compresses stale conversation content to cut token usage

### Setup

1. **Install a plugin** using `bunx`:
   ```bash
   # Install OmO Ultimate
   bunx oh-my-openagent@latest install
   # Install OmO slim variant
   bunx oh-my-opencode-slim@latest install
   ```
   *`bunx` is part of the Bun runtime. If you don't have Bun, install it from [bun.sh](https://bun.sh).*

2. **Enable background subagents** (required for multi-agent orchestration):
   ```powershell
   [System.Environment]::SetEnvironmentVariable("OPENCODE_EXPERIMENTAL_BACKGROUND_SUBAGENTS", "true", "User")
   ```
   *Restart your terminal after running this so the variable takes effect.*

   *On macOS/Linux, add this to your shell profile (`~/.zshrc`, `~/.bashrc`, etc.) instead:*
   ```bash
   export OPENCODE_EXPERIMENTAL_BACKGROUND_SUBAGENTS=true
   ```
   *Then reload with `source ~/.zshrc` (or restart your terminal).*

3. **Before launching OpenCode**, authenticate and refresh the model list:
   ```bash
   opencode auth login
   opencode models --refresh
   ```

4. **Install the DCP plugin**:
   ```bash
   opencode plugin @tarquinen/opencode-dcp@latest --global
   ```

Now you're ready to start coding with OpenCode and your chosen plugin! 🚀

---

## 🩹 Troubleshooting

- **OpenCode can't use `glob` or `ripgrep`** — add `rg.exe` to `.config/opencode/bin/` and make sure that folder is on your user `PATH`.
