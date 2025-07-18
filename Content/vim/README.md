# Vim - Text Editor

## Table of Contents

- [Vim - Text Editor](#vim-text-editor)
  - [1. Introduction](#1-introduction)
    - [Key Features:](#key-features)
  - [2. Installation](#2-installation)
    - [Unix/Linux](#unixlinux)
- [Debian/Ubuntu](#debianubuntu)
- [Red Hat/CentOS](#red-hatcentos)
- [macOS (using Homebrew)](#macos-using-homebrew)
  - [3. Basic Vim Modes](#3-basic-vim-modes)
  - [4. Essential Commands](#4-essential-commands)
    - [Navigation](#navigation)
    - [Editing](#editing)
    - [Saving and Quitting](#saving-and-quitting)
  - [5. Resources](#5-resources)


<div align="center">
  <img src="../../resources/images/logos/logos_vim.svg" alt="Vim Logo" width="200">
</div>

---

<!-- omit in toc -->
---

## 1. Introduction

Vim is a highly configurable text editor built to enable efficient text editing. It's an improved version of the vi editor distributed with most UNIX systems. Vim is so useful for programming that many consider it an entire IDE.

### Key Features:
- Extensive plugin ecosystem
- Highly customizable
- Available on almost all platforms
- Efficient text manipulation

---

## 2. Installation

### Unix/Linux
```bash
# Debian/Ubuntu
sudo apt-get install vim

# Red Hat/CentOS
sudo yum install vim

# macOS (using Homebrew)
brew install vim
```

---

## 3. Basic Vim Modes

1. **Normal Mode** (Default)
   - Command and navigation mode
   - Press `Esc` to return to this mode

2. **Insert Mode**
   - For typing text
   - Enter with `i`, `a`, `o`, etc.

3. **Visual Mode**
   - For selecting text
   - Enter with `v`, `V`, or `Ctrl-v`

4. **Command Mode**
   - For executing commands
   - Enter with `:`

---

## 4. Essential Commands

### Navigation
- `h`, `j`, `k`, `l` - Left, down, up, right
- `w` - Next word
- `b` - Previous word
- `0` - Start of line
- `$` - End of line
- `gg` - Start of file
- `G` - End of file
- `e` - Moves cursor forwards per word end

**Tip:** You can add a number before a navigation command to move the cursor by that number of steps.  
For example, `5j` moves down 5 lines, and `3k` moves up 3 lines.


### Editing
- `i` - Insert before cursor
- `a` - Insert after cursor
- `o` - Insert new line below
- `O` - Insert new line above
- `dd` - Delete line
- `yy` - Copy line
- `p` - Paste after cursor
- `P` - Paste before cursor
- `u` - Undo
- `d` - Delete visual selection

### Saving and Quitting
- `:w` - Save
- `:q` - Quit
- `:wq` - Save and quit
- `:q!` - Quit without saving

---

## 5. Resources

- [Vim Official Documentation](https://www.vim.org/docs.php)
- [Vim Awesome](https://vimawesome.com/) - Plugins directory
- [Vim Cheat Sheet](https://vim.rtorr.com/)

