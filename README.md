# VS Code setup

Portable copy of my current VS Code setup for macOS. It includes the default
settings, shared keybindings and MCP servers, eight language profiles, and an
extension manifest for each profile. `core.jsonc` and the profile JSONC files
are the editable sources; `sync.py` generates VS Code's `settings.json` files.

## Set up a new Mac

1. Install VS Code and add its `code` command to `PATH` from the Command Palette.
2. Launch VS Code once, then quit it. This creates its user data directory.
3. Clone this repository and run:

   ```sh
   cd vscode-setup
   python3 sync.py --dry-run
   python3 sync.py
   ```

The script registers Web, Ruby, Python, Java, Go, Elixir, Ruby Focus, and
Rust Focus profiles. It writes settings and shared keybindings, then installs each
profile's extension list. Existing files that change get a one-time
`.vscode-setup.bak` backup alongside them. Rerun the script after editing a
source file or extension manifest.

The Ruby Focus profile inherits Ruby settings and replaces the extension list
with only the theme, icon, and keymap extensions. Rust Focus does the same on
top of core settings alone: no rust-analyzer, completion, hovers, or AI
features, so code is checked with `cargo` in the terminal. The default profile
has its own extension list in `extensions/default.txt`.

## Local dependencies

- Install JetBrainsMono Nerd Font for the configured editor and terminal font.
- Ruby expects `asdf` at `/opt/homebrew/bin/asdf`; change `ruby.jsonc` if it
  lives elsewhere.
- Language runtimes, formatters, and project dependencies are installed
  separately. The extension manifests capture extension IDs, not their versions.
- MCP servers in `mcp.json` use `uvx`, `npx`, and GitHub Copilot. Install those
  tools and sign in to GitHub as needed. No account state or credentials are
  stored here.

This repository excludes VS Code's history, workspace storage, global state,
profile databases, and installed extension binaries. Those files contain local
state and are not needed to recreate the configuration.
