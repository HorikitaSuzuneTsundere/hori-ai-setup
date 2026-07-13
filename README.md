# 🔧 OpenCode Setup

A minimal, modern development environment powered by Neovim, Rust, and a fast terminal.
Follow the steps below to get everything installed and configured.

---

## ✅ Prerequisites

- [ ] **Git** — Make sure `git` is available in your global `PATH`
- [ ] **Nerd Font** — Install [Hack Nerd Font](https://www.nerdfonts.com/font-downloads) for icon support in the terminal

---

## 🧱 Compilers & Runtimes

- [ ] **C compiler**
  - Windows: use the **Visual Studio Installer** (C++ workload) or **MinGW‑w64**
  - macOS: `xcode-select --install`
  - Linux: `sudo apt install build-essential` (or equivalent)
- [ ] **Rust compiler**
  ```bash
  curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
  ```
  Then restart your shell or run `source "$HOME/.cargo/env"`

---

## 🛠 Command‑Line Tools

- [ ] **ripgrep (`rg`) & fd & ast-grep (`sg`)**
  ```bash
  cargo install ripgrep fd-find ast-grep
  ```
- [ ] **Node.js** (via Chocolatey on Windows)
  ```powershell
  choco install nodejs
  ```
  *On macOS/Linux consider [`fnm`](https://github.com/Schniz/fnm) or `nvm` instead.*

---

## 🖥 Terminal & Shell

- [ ] **Alacritty** or **Kitty** (Unix)
  - Alacritty: [alacritty.org](https://alacritty.org/)
  - Kitty: [sw.kovidgoyal.net/kitty](https://sw.kovidgoyal.net/kitty/)
  - Windows users can also use **Windows Terminal** (preinstalled or from the Microsoft Store)
- [ ] **PowerShell (`pwsh`)**
  ```powershell
  # Windows (if not already installed)
  winget install --id Microsoft.PowerShell

  # macOS / Linux
  brew install powershell         # macOS
  sudo snap install powershell    # Linux (snap)
  ```

---

## ✍️ Editor

- [ ] **Neovim**
  ```bash
  # macOS / Linux
  brew install neovim            # macOS
  sudo apt install neovim        # Debian/Ubuntu
  sudo pacman -S neovim          # Arch

  # Windows
  winget install Neovim.Neovim
  ```
  *Optional: kickstart your config with [NvChad](https://nvchad.com/) or [LazyVim](https://www.lazyvim.org/).*

---

## 🔌 OpenCode Plugins

The author uses preconfigured plugins to streamline the coding experience:

- **OmO** — combines **OpenAI** and **Moonshot** AI models
- **OmO-slim** — combines **OpenAI** and **Opencode Go** AI models

### Setup

1. **Install OpenCode** (if not already present):  
   *Refer to the official OpenCode documentation for installation instructions for your platform.*

2. **Install a plugin** using `bunx`:
   ```bash
   # Install OmO
   bunx oh-my-openagent@latest install
   # or the slim variant
   bunx oh-my-opencode-slim@latest install
   ```
   *`bunx` is part of the Bun runtime. If you don't have Bun, install it from [bun.sh](https://bun.sh).*

3. **Before launching OpenCode**, authenticate and refresh the model list:
   ```bash
   opencode auth login
   opencode models --refresh
   ```

Now you're ready to start coding with OpenCode and your chosen plugin! 🚀
