# 🚀 Complete Development Environment Setup

A comprehensive dotfiles repository with Neovim and Tmux configuration for an efficient development workflow.

## 📋 Table of Contents

- [Installation Guide](#-installation-guide)
- [Tmux Usage Guide](#-tmux-usage-guide)
- [Neovim Usage Guide](#-neovim-usage-guide)
- [Troubleshooting](#-troubleshooting)

---

## 🛠 Installation Guide

### Prerequisites

Before starting, ensure you have the following installed:

<details>
<summary><strong>📱 For macOS</strong></summary>

```bash
# Install Homebrew (if not already installed)
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install required tools
brew install git tmux neovim fzf cmake
```

</details>

<details>
<summary><strong>🐧 For Ubuntu/Debian</strong></summary>

```bash
# Update package list
sudo apt update

# Install required tools
sudo apt install git tmux neovim fzf build-essential curl cmake

# Install latest Neovim (if the default version is too old)
curl -LO https://github.com/neovim/neovim/releases/latest/download/nvim-linux64.tar.gz
sudo rm -rf /opt/nvim
sudo tar -C /opt -xzf nvim-linux64.tar.gz
echo 'export PATH="$PATH:/opt/nvim-linux64/bin"' >> ~/.bashrc
source ~/.bashrc
rm nvim-linux64.tar.gz
```

</details>

### Step-by-Step Installation

<details>
<summary><strong>1. Clone the Repository</strong></summary>

```bash
# Navigate to your home directory
cd ~

# Clone the repository
git clone <your-repo-url> dotfiles
cd dotfiles
```

</details>

<details>
<summary><strong>2. Set Up Environment Variables</strong></summary>

```bash
# Add to your shell profile (~/.bashrc, ~/.zshrc, etc.)
echo 'export XDG_CONFIG_HOME="$HOME/.config"' >> ~/.bashrc
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc

# For Zsh users:
echo 'export XDG_CONFIG_HOME="$HOME/.config"' >> ~/.zshrc
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc

# Reload your shell or run:
source ~/.bashrc
# or for zsh:
source ~/.zshrc
```

</details>

<details>
<summary><strong>3. Make Scripts Executable</strong></summary>

```bash
# Make all scripts executable
chmod +x dev-env
chmod +x run
chmod +x .ready-tmux
chmod +x .local/scripts/*
chmod +x runs/*
```

</details>

<details>
<summary><strong>4. Run the Installation Scripts</strong></summary>

```bash
# First, check what will be installed (dry run)
./dev-env --dry

# If everything looks good, run the actual installation
./dev-env

# Install additional libraries and tools
./run libs
```

</details>

<details>
<summary><strong>5. Set Up Shell Integration</strong></summary>

```bash
# For Zsh users, add fzf integration
echo 'source ~/.fzf.zsh' >> ~/.zshrc

# For Bash users
echo 'source ~/.fzf.bash' >> ~/.bashrc

# Reload shell
source ~/.bashrc  # or ~/.zshrc
```

</details>

<details>
<summary><strong>6. Verify Installation</strong></summary>

```bash
# Check Neovim version (should be 0.8.0+)
nvim --version

# Check Tmux version
tmux -V

# Test fzf
fzf --version

# Verify scripts are executable
ls -la ~/.local/bin/
```

</details>

<details>
<summary><strong>7. First Neovim Launch</strong></summary>

```bash
# Launch Neovim for the first time
nvim

# Lazy.nvim will automatically install all plugins
# Wait for installation to complete, then restart Neovim
# If you see any errors, press ENTER to continue and restart nvim
```

</details>

### Post-Installation Setup

<details>
<summary><strong>Directory Setup</strong></summary>

```bash
# Create personal projects directory (for tmux sessionizer)
mkdir -p ~/personal

# Create some test directories
mkdir -p ~/personal/test-project-1
mkdir -p ~/personal/test-project-2
```

</details>

<details>
<summary><strong>Test Installation</strong></summary>

```bash
# Test tmux
tmux new-session -s test

# Inside tmux, test sessionizer (should be Ctrl+a + f)
# This should open fzf to select from ~/personal directories

# Test neovim
nvim
# Inside nvim, test telescope with Space + ff
```

</details>

---

## 🖥 Tmux Usage Guide

Tmux is a terminal multiplexer that allows you to run multiple terminal sessions within a single window.

### 🔑 Essential Concepts

<details>
<summary><strong>📖 Understanding Tmux Components</strong></summary>

- **Session**: A collection of windows, like having multiple terminal tabs
- **Window**: A single screen within a session, like a browser tab
- **Pane**: Split sections within a window, like split screens
- **Prefix Key**: `Ctrl+a` (your configured prefix) - press this before other commands
</details>

### 🎯 Most Important Commands

<details>
<summary><strong>💼 Session Management</strong></summary>

```bash
# Start new session
tmux new-session -s session_name

# List all sessions
tmux list-sessions
tmux ls

# Attach to existing session
tmux attach-session -t session_name
tmux a -t session_name

# Detach from session (inside tmux)
Ctrl+a + d

# Kill session
tmux kill-session -t session_name

# Rename session (inside tmux)
Ctrl+a + $
```

</details>

<details>
<summary><strong>🪟 Window Management</strong></summary>

```bash
# Create new window
Ctrl+a + c

# Switch between windows
Ctrl+a + n    # Next window
Ctrl+a + p    # Previous window
Ctrl+a + 0-9  # Switch to window number
Ctrl+a + l    # Last window

# Rename current window
Ctrl+a + ,

# Close window
Ctrl+a + &

# List windows
Ctrl+a + w
```

</details>

<details>
<summary><strong>📱 Pane Management</strong></summary>

```bash
# Split window vertically (side by side)
Ctrl+a + %

# Split window horizontally (top and bottom)
Ctrl+a + "

# Navigate between panes (custom configured)
Ctrl+a + h    # Move left
Ctrl+a + j    # Move down
Ctrl+a + k    # Move up
Ctrl+a + l    # Move right

# Close current pane
Ctrl+a + x

# Toggle pane zoom (fullscreen)
Ctrl+a + z

# Show pane numbers
Ctrl+a + q

# Break pane into new window
Ctrl+a + !
```

</details>

<details>
<summary><strong>🚀 Custom Features (Your Configuration)</strong></summary>

```bash
# Reload tmux configuration
Ctrl+a + r

# Quick project switcher (tmux-sessionizer)
# This is your most powerful feature!
# It opens fzf to select from ~/personal directories
# Automatically creates/switches sessions
# Note: The exact keybinding may vary - check your tmux.conf
```

</details>

### 📚 Advanced Features

<details>
<summary><strong>📋 Copy Mode (Vi-style)</strong></summary>

```bash
# Enter copy mode
Ctrl+a + [

# Navigation in copy mode (vi keys)
h, j, k, l    # Move cursor
w, b          # Word movement
0, $          # Line start/end
gg, G         # Top/bottom of buffer

# Selection and copying
v             # Start selection
y             # Copy selection (copies to system clipboard)
Enter         # Copy selection and exit copy mode
q             # Exit copy mode without copying

# Paste
Ctrl+a + ]
```

</details>

<details>
<summary><strong>🎨 Pane Resizing</strong></summary>

```bash
# Enter command mode for resizing
Ctrl+a + :

# Resize commands (in command mode)
resize-pane -D 5    # Down
resize-pane -U 5    # Up
resize-pane -L 5    # Left
resize-pane -R 5    # Right

# Or use repeat mode
Ctrl+a + Ctrl+h    # Resize left (hold Ctrl and repeat h)
Ctrl+a + Ctrl+j    # Resize down
Ctrl+a + Ctrl+k    # Resize up
Ctrl+a + Ctrl+l    # Resize right
```

</details>

<details>
<summary><strong>🔍 Search and Find</strong></summary>

```bash
# Find window by name
Ctrl+a + f

# Find session
Ctrl+a + s

# Search in copy mode
Ctrl+a + [, then /pattern    # Search forward
Ctrl+a + [, then ?pattern    # Search backward
```

</details>

<details>
<summary><strong>🛠 Tmux Sessionizer Workflow</strong></summary>

This is your custom script that makes project switching super fast:

```bash
# 1. Use your configured keybinding (check tmux.conf for exact key)
# 2. fzf opens showing all directories in ~/personal
# 3. Select a project with arrow keys or start typing
# 4. Press Enter
# 5. Tmux automatically:
#    - Creates new session (if doesn't exist)
#    - Switches to session (if exists)
#    - Runs .ready-tmux script if present in project
#    - Changes to project directory
```

**Setting up projects:**

```bash
# Create project structure
mkdir -p ~/personal/my-awesome-project
cd ~/personal/my-awesome-project

# Create custom startup script
cat > .ready-tmux << 'EOF'
#!/usr/bin/env bash
# This runs when tmux-sessionizer opens this project

# Example: create development windows
tmux neww -n "editor"
tmux neww -n "server"
tmux neww -n "logs"

# Switch back to first window
tmux selectw -t 1
EOF

chmod +x .ready-tmux
```

</details>

### 🎯 Pro Tmux Tips

<details>
<summary><strong>⚡ Efficiency Tips</strong></summary>

1. **Use sessions for different projects** - Never lose your work context
2. **Master the sessionizer** - Fastest way to switch between projects
3. **Use descriptive window names** - `Ctrl+a + ,` to rename
4. **Detach instead of closing** - `Ctrl+a + d` keeps everything running
5. **Use copy mode for scrolling** - `Ctrl+a + [` then navigate with vi keys
</details>

---

## 📝 Neovim Usage Guide

Neovim is a highly configurable text editor built for efficiency. Your configuration includes LSP support, autocompletion, file exploration, and more.

### 🎯 Essential Concepts

<details>
<summary><strong>📖 Understanding Vim Modes</strong></summary>

- **Normal Mode**: Navigation and commands (default mode) - cursor is a block
- **Insert Mode**: Typing text - cursor is a line
- **Visual Mode**: Selecting text - text is highlighted
- **Command Mode**: Running commands - starts with `:`
- **Leader Key**: `Space` - your custom prefix for most commands
</details>

### 🔑 Most Important Commands

<details>
<summary><strong>🔄 Mode Switching</strong></summary>

```bash
# Enter Insert mode
i         # Insert at cursor
a         # Insert after cursor
o         # New line below and insert
O         # New line above and insert
I         # Insert at beginning of line
A         # Insert at end of line

# Return to Normal mode
ESC       # Standard way
jk        # Your custom mapping (faster)

# Enter Visual mode
v         # Character-wise selection
V         # Line-wise selection
Ctrl+v    # Block selection

# Enter Command mode
:         # Type commands like :w, :q, etc.
```

</details>

<details>
<summary><strong>🧭 Basic Navigation</strong></summary>

```bash
# Character movement
h         # Left
j         # Down
k         # Up
l         # Right

# Word movement
w         # Next word start
b         # Previous word start
e         # End of word
W, B, E   # Same but ignore punctuation

# Line movement
0         # Beginning of line
^         # First non-blank character
$         # End of line
g_        # Last non-blank character

# Screen movement
gg        # Go to top of file
G         # Go to bottom of file
Ctrl+u    # Half page up
Ctrl+d    # Half page down
Ctrl+f    # Full page down
Ctrl+b    # Full page up
```

</details>

### 🚀 Leader Key Commands (Space)

<details>
<summary><strong>📁 File Operations</strong></summary>

```bash
# File Explorer (NvimTree)
Space + ee    # Toggle file explorer
Space + ef    # Find current file in explorer
Space + ec    # Collapse file explorer
Space + er    # Refresh file explorer

# In file explorer:
Enter         # Open file/folder
a             # Create new file/folder
d             # Delete
r             # Rename
x             # Cut
c             # Copy
p             # Paste
R             # Refresh
```

</details>

<details>
<summary><strong>🔍 Finding Files and Text (Telescope)</strong></summary>

```bash
Space + ff    # Find files (fuzzy search) - MOST USED!
Space + fr    # Find recent files
Space + fs    # Find string in project (live grep) - VERY USEFUL!
Space + fc    # Find word under cursor in project
Space + ft    # Find todo comments

# Inside Telescope:
Ctrl+j        # Move down
Ctrl+k        # Move up
Enter         # Open file
Ctrl+t        # Open in new tab
Ctrl+v        # Open in vertical split
Ctrl+x        # Open in horizontal split
ESC           # Close telescope
```

</details>

<details>
<summary><strong>🪟 Window and Tab Management</strong></summary>

```bash
# Split windows
Space + sv    # Split vertically (side by side)
Space + sh    # Split horizontally (top/bottom)
Space + se    # Make splits equal size
Space + sx    # Close current split
Space + sm    # Maximize/minimize split (vim-maximizer)

# Navigate between splits (with vim-tmux-navigator)
Ctrl+h        # Move to left split
Ctrl+j        # Move to down split
Ctrl+k        # Move to up split
Ctrl+l        # Move to right split

# Tab management
Space + to    # Open new tab
Space + tx    # Close current tab
Space + tn    # Next tab
Space + tp    # Previous tab
Space + tf    # Open current buffer in new tab
```

</details>

<details>
<summary><strong>🔧 Utility Commands</strong></summary>

```bash
# Search and highlights
Space + nh    # Clear search highlights

# Numbers
Space + +     # Increment number under cursor
Space + -     # Decrement number under cursor

# Session management
Space + wr    # Restore session for current directory
Space + ws    # Save session

# Git operations
Space + lg    # Open LazyGit (full git interface)
```

</details>

### 📚 LSP (Language Server Protocol) Features

<details>
<summary><strong>🧭 Code Navigation</strong></summary>

```bash
# Go to definitions/references
gd        # Go to definition - MOST USED!
gD        # Go to declaration
gR        # Show all references
gi        # Go to implementation
gt        # Go to type definition

# Documentation
K         # Show documentation for symbol under cursor

# Navigation history
Ctrl+o    # Go back to previous location
Ctrl+i    # Go forward in location history
```

</details>

<details>
<summary><strong>⚡ Code Actions</strong></summary>

```bash
# Code modifications
Space + ca    # Show code actions (auto-fix, refactor, etc.)
Space + rn    # Rename symbol across project
Space + mp    # Format file or selection

# Quick fixes
# Put cursor on error/warning and use Space + ca
# Common actions: import missing modules, fix syntax, etc.
```

</details>

<details>
<summary><strong>🐛 Diagnostics (Errors/Warnings)</strong></summary>

```bash
# View diagnostics
Space + d     # Show diagnostics for current line
Space + D     # Show all diagnostics for current file

# Navigate diagnostics
]d            # Go to next diagnostic
[d            # Go to previous diagnostic

# Restart LSP if issues
Space + rs    # Restart language server
```

</details>

### 🎯 Autocompletion

<details>
<summary><strong>💡 Completion System</strong></summary>

```bash
# Trigger completion (in Insert mode)
Ctrl+Space    # Manually trigger completion

# Navigate completion menu
Ctrl+j        # Next suggestion
Ctrl+k        # Previous suggestion
Ctrl+b        # Scroll documentation up
Ctrl+f        # Scroll documentation down

# Accept/dismiss
Enter         # Accept selected completion
Ctrl+e        # Close completion menu

# Snippets (if available)
Tab           # Expand snippet or jump to next placeholder
Shift+Tab     # Jump to previous placeholder
```

</details>

### 🔍 Search and Replace

<details>
<summary><strong>🔎 Search</strong></summary>

```bash
# Basic search
/pattern      # Search forward
?pattern      # Search backward
n             # Next match
N             # Previous match (opposite direction)
*             # Search for word under cursor (forward)
#             # Search for word under cursor (backward)

# Clear search highlights
Space + nh
```

</details>

<details>
<summary><strong>🔄 Replace (Substitute Plugin)</strong></summary>

```bash
# Substitute operations
s + motion    # Substitute with motion (e.g., siw = substitute word)
ss            # Substitute entire line
S             # Substitute from cursor to end of line

# In visual mode
s             # Substitute selected text

# Traditional vim substitute
:s/old/new/g     # Replace in current line
:%s/old/new/g    # Replace in entire file
:%s/old/new/gc   # Replace with confirmation
```

</details>

### 🎨 Text Objects and Motions

<details>
<summary><strong>🎯 Enhanced Text Objects</strong></summary>

Your configuration includes powerful text objects for code:

```bash
# Function/Method objects
af            # Select outer function (including function keyword)
if            # Select inner function (just the body)
am            # Select outer method
im            # Select inner method

# Parameter objects
aa            # Select outer parameter (including commas)
ia            # Select inner parameter (just the parameter)

# Property objects (JavaScript/TypeScript)
a:            # Select outer object property
i:            # Select inner object property
l:            # Select left side of property (key)
r:            # Select right side of property (value)

# Conditional objects
ai            # Select outer conditional (if/else)
ii            # Select inner conditional

# Loop objects
al            # Select outer loop
il            # Select inner loop

# Class objects
ac            # Select outer class
ic            # Select inner class
```

</details>

<details>
<summary><strong>🏃 Movement Commands</strong></summary>

```bash
# Navigate by code structure
]f            # Next function call start
[f            # Previous function call start
]m            # Next method/function definition start
[m            # Previous method/function definition start
]c            # Next class start
[c            # Previous class start

# Navigate diagnostics/todos
]d            # Next diagnostic
[d            # Previous diagnostic
]t            # Next todo comment
[t            # Previous todo comment
```

</details>

<details>
<summary><strong>🔄 Swapping Objects</strong></summary>

```bash
# Swap parameters/arguments
Space + na    # Swap current parameter with next
Space + pa    # Swap current parameter with previous

# Swap object properties
Space + n:    # Swap current property with next
Space + p:    # Swap current property with previous

# Swap functions
Space + nm    # Swap current function with next
Space + pm    # Swap current function with previous
```

</details>

### 🎪 Advanced Text Manipulation

<details>
<summary><strong>💬 Comments</strong></summary>

```bash
# Line comments
gcc           # Toggle comment for current line
gc + motion   # Comment with motion (e.g., gc3j = comment 3 lines down)

# Block comments
gbc           # Toggle block comment for current line
gb + motion   # Block comment with motion

# In visual mode
gc            # Comment/uncomment selection
gb            # Block comment selection
```

</details>

<details>
<summary><strong>🎭 Surround Operations</strong></summary>

```bash
# Add surroundings
ys + motion + char    # Add surround
# Examples:
ysiw"                 # Surround word with quotes
yss)                  # Surround line with parentheses
ysip}                 # Surround paragraph with braces

# Change surroundings
cs + old + new        # Change surround
# Examples:
cs"'                  # Change " to '
cs)]                  # Change ) to ]
cst<div>              # Change tag to <div>

# Delete surroundings
ds + char             # Delete surround
# Examples:
ds"                   # Delete surrounding quotes
ds)                   # Delete surrounding parentheses
dst                   # Delete surrounding tag
```

</details>

<details>
<summary><strong>🎯 Multiple Cursors and Selection</strong></summary>

```bash
# Incremental selection (treesitter)
Ctrl+Space    # Start/expand selection intelligently
Backspace     # Shrink selection

# This selects based on syntax tree:
# First press: selects current word
# Second press: selects containing expression
# Third press: selects containing statement
# etc.
```

</details>

### 🔧 Plugin-Specific Features

<details>
<summary><strong>📊 Trouble (Error/Warning Panel)</strong></summary>

```bash
# Open diagnostic panels
Space + xw    # Workspace diagnostics (all files)
Space + xd    # Document diagnostics (current file)
Space + xq    # Quickfix list
Space + xl    # Location list
Space + xt    # Todo comments across project

# Inside Trouble panel:
Enter         # Jump to item
q             # Close panel
```

</details>

<details>
<summary><strong>🌳 File Tree (NvimTree)</strong></summary>

```bash
# Basic operations (when tree is focused)
Enter/o       # Open file or toggle folder
a             # Create new file/folder
d             # Delete (with confirmation)
r             # Rename
x             # Cut
c             # Copy
p             # Paste
R             # Refresh tree
q             # Close tree

# Navigation
j/k           # Move up/down
h             # Close folder or go to parent
l             # Open folder or file
P             # Go to parent directory
```

</details>

<details>
<summary><strong>📋 Todo Comments</strong></summary>

Your setup recognizes these special comments:

```bash
# Recognized patterns:
TODO: something to do
HACK: hacky code
BUG: something is wrong
FIXME: needs fixing
NOTE: important note
WARNING: be careful

# Navigate todos
]t            # Next todo
[t            # Previous todo
Space + ft    # Find all todos with Telescope
Space + xt    # View todos in Trouble panel
```

</details>

### 🎨 Visual Features

<details>
<summary><strong>🌈 Themes and UI</strong></summary>

Your setup includes:

- **Tokyo Night Theme**: Dark theme with custom blue colors
- **Lualine**: Status line showing mode, file info, git status
- **Bufferline**: Tab-like buffer display at top
- **Indent Guides**: Visual indentation markers
- **Git Signs**: Git change indicators in left gutter
- **LSP Diagnostics**: Error/warning icons in gutter

**Status Line Indicators:**

- Mode indicator (Normal/Insert/Visual) with colors
- Current file and modification status
- Git branch and changes
- LSP status and diagnostics count
- File encoding and type
</details>

<details>
<summary><strong>📂 Git Integration</strong></summary>

```bash
# LazyGit (full Git UI)
Space + lg    # Open LazyGit interface

# Git hunks (individual changes)
]h            # Next git hunk
[h            # Previous git hunk
Space + hs    # Stage current hunk
Space + hr    # Reset current hunk
Space + hp    # Preview hunk changes
Space + hS    # Stage entire buffer
Space + hR    # Reset entire buffer
Space + hu    # Undo stage hunk

# Git blame and diff
Space + hb    # Show blame for current line
Space + hB    # Toggle line blame display
Space + hd    # Diff current file
Space + hD    # Diff against HEAD~1

# In visual mode
Space + hs    # Stage selected lines
Space + hr    # Reset selected lines
```

</details>

### 🎯 Workflows and Pro Tips

<details>
<summary><strong>⚡ Daily Workflow</strong></summary>

**Opening a Project:**

1. Use tmux sessionizer to switch to project
2. `Space + ee` to open file tree
3. `Space + ff` to quickly find files
4. `Space + fs` to search across codebase

**Editing Code:**

1. `gd` to jump to definitions
2. `K` to read documentation
3. `Space + ca` for quick fixes
4. `Space + rn` to rename variables

**Managing Changes:**

1. `Space + lg` for git operations
2. `Space + hs` to stage individual hunks
3. `:w` to save, `Space + mp` to format
4. `Space + wr` to save session

**Debugging Issues:**

1. `Space + xd` to see all file errors
2. `]d` and `[d` to navigate diagnostics
3. `Space + ca` on errors for fixes
4. `Space + rs` to restart LSP if needed
</details>

<details>
<summary><strong>🚀 Efficiency Shortcuts</strong></summary>

```bash
# Quick file operations
Space + ff → type filename → Enter    # Fastest file opening
Space + fs → type text → Enter        # Find any text in project
gd → Ctrl+o                          # Jump to definition and back

# Quick editing
ciw           # Change entire word
ci"           # Change inside quotes
di)           # Delete inside parentheses
va{           # Select all inside braces
yap           # Yank (copy) entire paragraph

# Quick navigation
gg            # Top of file
G             # Bottom of file
:42           # Go to line 42
*             # Find next occurrence of current word
#             # Find previous occurrence of current word

# Quick fixes
Space + ca    # Auto-fix errors
Space + mp    # Format code
gcc           # Comment/uncomment line
Space + rn    # Rename symbol everywhere
```

</details>

<details>
<summary><strong>🎓 Learning Path</strong></summary>

**Week 1 - Basics:**

- Master mode switching (i, ESC/jk, v, :)
- Learn basic navigation (hjkl, w, b, 0, $)
- Use `Space + ff` and `Space + ee` for files
- Practice `:w` to save, `:q` to quit

**Week 2 - File Management:**

- Use telescope extensively (`Space + fs`, `Space + fr`)
- Learn window splits (`Space + sv`, `Space + sh`)
- Practice tab management (`Space + to`, `Space + tn`)
- Use `gd` and `K` for code navigation

**Week 3 - Text Editing:**

- Learn text objects (ciw, di", va}, etc.)
- Practice commenting (gcc, gc)
- Use surround operations (ys, cs, ds)
- Master search and replace (/, n, N, :s)

**Week 4 - Advanced Features:**

- LSP features (`Space + ca`, `Space + rn`, diagnostics)
- Git workflow (`Space + lg`, git hunks)
- Custom text objects (af, if, aa, ia)
- Session management (`Space + wr`, `Space + ws`)

**Month 2 - Mastery:**

- Customize keybindings for your workflow
- Learn advanced telescope features
- Master treesitter text objects
- Create custom snippets and configurations
</details>

---

## 🐛 Troubleshooting

<details>
<summary><strong>🔧 Common Neovim Issues</strong></summary>

**Plugin Installation Problems:**

```bash
# Reinstall all plugins
:Lazy clean
:Lazy install

# Update plugins
:Lazy update

# Check plugin status
:Lazy

# Rebuild telescope-fzf-native if architecture issues
:Lazy clean telescope-fzf-native.nvim
:Lazy install telescope-fzf-native.nvim
```

**LSP Not Working:**

```bash
# Check LSP status
:LspInfo

# Check Mason installer
:Mason

# Restart LSP
Space + rs
:LspRestart

# Check if mason-lspconfig is available
:lua print(vim.inspect(require('mason-lspconfig')))
```

**Treesitter Issues:**

```bash
# Update treesitter parsers
:TSUpdate

# Install specific parser
:TSInstall lua javascript typescript

# Check treesitter status
:TSInstallInfo
```

</details>

<details>
<summary><strong>🖥 Tmux Issues</strong></summary>

**Tmux Not Responding:**

```bash
# Kill all tmux sessions (last resort)
tmux kill-server

# Reload tmux config
Ctrl+a + r

# List sessions if tmux seems frozen
tmux list-sessions

# Force detach if stuck
tmux detach-client
```

**Copy/Paste Not Working:**

```bash
# Check if xclip is installed (Linux)
sudo apt install xclip

# Check if pbcopy/pbpaste work (macOS)
echo "test" | pbcopy && pbpaste

# Reload tmux config after installing clipboard tools
Ctrl+a + r
```

**Sessionizer Not Working:**

```bash
# Check if script is executable
ls -la ~/.local/bin/tmux-sessionizer

# Make executable if needed
chmod +x ~/.local/bin/tmux-sessionizer

# Check if ~/personal directory exists
ls -la ~/personal

# Test fzf
echo -e "test1\ntest2\ntest3" | fzf
```

</details>

<details>
<summary><strong>⚡ Performance Issues</strong></summary>

**Neovim Slow Startup:**

```bash
# Profile startup time
nvim --startuptime startup.log
less startup.log

# Temporarily disable plugins
mv ~/.config/nvim ~/.config/nvim.backup
nvim  # test if it's faster

# Restore config
mv ~/.config/nvim.backup ~/.config/nvim
```

**Large File Handling:**

```bash
# Disable features for large files
:set syntax=off
:set relativenumber!
:set foldmethod=manual

# Or edit options.lua to set file size limits
```

**Tmux Performance:**

```bash
# Reduce tmux history
set-option -g history-limit 1000

# Disable automatic window renaming
set-option -g automatic-rename off
```

</details>

<details>
<summary><strong>🔄 Reset Configuration</strong></summary>

**Complete Reset:**

```bash
# Backup current config
mv ~/.config/nvim ~/.config/nvim.backup
mv ~/.local/share/nvim ~/.local/share/nvim.backup
mv ~/.tmux ~/.tmux.backup

# Reinstall from dotfiles
cd ~/dotfiles
./dev-env

# If still issues, clean install Neovim
# macOS:
brew uninstall neovim
brew install neovim

# Ubuntu:
sudo apt remove neovim
# Then reinstall latest version
```

**Partial Reset:**

```bash
# Reset only Neovim plugins
rm -rf ~/.local/share/nvim
nvim  # Will reinstall all plugins

# Reset only Neovim config
cd ~/dotfiles
./dev-env  # Will copy fresh config
```

</details>

<details>
<summary><strong>🆘 Getting Help</strong></summary>

**Neovim Built-in Help:**

```bash
:help keyword          # Get help on any topic
:help index            # List all commands
:Telescope help_tags   # Search help with telescope
:help nvim-treesitter  # Plugin-specific help
:help lsp              # LSP help
```

**Check Configuration:**

```bash
# Check current settings
:set                   # Show all options
:map                   # Show all keymappings
:lua print(vim.inspect(vim.g))  # Show global variables

# Check loaded plugins
:Lazy

# Check LSP clients
:LspInfo
```

**Debug Mode:**

```bash
# Start Neovim with verbose logging
nvim -V9nvim.log

# Check log file
tail -f nvim.log
```

</details>

---

## 🎉 Congratulations!

You now have a powerful development environment set up!

### 🎯 Quick Start Checklist:

1. ✅ **Tmux Basics**: Create session, split panes, detach/attach
2. ✅ **Neovim Modes**: Normal (ESC), Insert (i), Visual (v), Command (:)
3. ✅ **Essential Keys**: `Space + ff` (find files), `Space + fs` (search text), `gd` (go to definition)
4. ✅ **File Explorer**: `Space + ee` to toggle NvimTree
5. ✅ **Git Integration**: `Space + lg` for LazyGit

### 🚀 Next Steps:

1. **Practice Daily**: Use the essential commands every day
2. **Learn Gradually**: Add one new command per day
3. **Customize**: Modify configs in `~/.config/nvim/lua/sabir/`
4. **Explore**: Try `:Telescope` and see all available features

### 📚 Remember:

- **Tmux Prefix**: `Ctrl+a` then your command
- **Neovim Leader**: `Space` then your command
- **Get Help**: `:help topic` in Neovim
- **Practice**: Muscle memory takes time - be patient!

**The key to mastering this setup is daily practice and gradual learning. Start with file navigation and basic editing, then add advanced features as you become comfortable.**

Happy coding! 🚀
