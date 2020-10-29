---
title: "XDG Base Directories"
excerpt_separator: "<!--more-->"
categories:
  - linux
  - macos
  - shell
tags:
  - shell
  - command line
  - zsh
  - Arch Linux
---

I decided to move all of my home directory "dot clutter" to use `$XDG_CONFIG_HOME` (.config) rather than just dumping everything into the home directory. [XDG directories](https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html) are a way for a user to specify where configuration files exist on the system.

I searched the man pages of the apps and programs I use and checked to see if they supported this feature. A lot did, but many do not. [Here is the best resource](https://wiki.archlinux.org/index.php/XDG_Base_Directory) I found for XDG and what level of support most apps have for the standard.

The main programs I was concerned with fixing were:
1. shells (bash & zsh)
2. vim
3. git
4. terminals (iterm2, alacritty, kitty)
5. tmux

Given the preference, if a program does support the XDG specification, I'd use it going forward.

Most apps were straightforward. The hardest to move was zsh (I stopped using bash long ago anyway). Zsh only has partial XDG support; to use XDG with zsh, you have to "bootstrap" it with the `.zshenv` file. This file resides in your normal home directory and tells zsh how to find the rest of its normal configuration files. My `.zshenv` file looks like this:

```
# this is the bare bones setup to move everything to XDG dir
ZDOTDIR=$HOME/.config/zsh

# Other XDG paths
export XDG_DATA_HOME=${XDG_DATA_HOME:="$HOME/.local/share"}
export XDG_CACHE_HOME=${XDG_CACHE_HOME:="$HOME/.cache"}
export XDG_CONFIG_HOME=${XDG_CONFIG_HOME:="$HOME/.config"}

# Default Apps
export EDITOR="nvim"
export VISUAL="code -n"
export TERMINAL="iterm"
export BROWSER="safari"
export PAGER="less"
```

The important part is defining `ZDOTDIR`, which is where your `.zshrc` and other zsh config files reside.

Additionally, I define the `$XDG_DATA_HOME`, `$XDG_CACHE_HOME`, and `$XDG_CONFIG_HOME` but using their defaults. This is mainly for my own reference, so I don't have to look them up lest I forget.

Lastly, I define standard variables used by the system such as my editors, pagers, etc. This is optional but I find it handy in many situations.

You can see all of this in action in my [dotfiles](https://github.com/curtisbridges/dotfiles) repo on GitHub.
