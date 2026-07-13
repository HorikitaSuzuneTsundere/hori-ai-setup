# Terminal Configuration

This snippet sets up a terminal emulator (e.g., Alacritty) with PowerShell as the default shell and a custom Nerd Font.

## What’s inside

- **Shell:** PowerShell (`pwsh.exe`) with no profile logo for a cleaner startup.
- **Font:** Hack Nerd Font Mono, size 12 – gives you powerline glyphs and ligatures.

## Usage

1. Place this configuration in your terminal’s config file (e.g., `alacritty.toml`).
2. Make sure **Hack Nerd Font Mono** is installed on your system.  
   You can get it from [Nerd Fonts](https://www.nerdfonts.com/).
3. Restart your terminal to apply the changes.

## Example config file location

- **Alacritty**: `%APPDATA%\alacritty\alacritty.toml` (Windows)  
  or `~/.config/alacritty/alacritty.toml` (Linux/macOS)