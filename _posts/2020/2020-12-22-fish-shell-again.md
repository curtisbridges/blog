---
title: "Fish shell via Homebrew on macOS"
layout: article
excerpt_separator: "<!--more-->"
categories:
  - homebrew
  - macos
tags:
  - homebrew
  - shell
---

# How to install and configure [fish](https://fishshell.com) shell on macOS via homebrew.

This is mostly for my future self to reference, but just in case anyone else finds it useful, here is how I setup fish shell on macOS.


1. `brew install fish`
2. Add `/usr/local/bin/fish` to `/etc/shells`
3. `chsh -s /usr/local/bin/fish`
4. [Recommended] Create config directories and files:
   1. Create `mkdir -p ~/.config/fish` and `touch ~/.config/fish/config.fish`. This config file will be used for other optional installs such as Starship, below.
   2. Create `mkdir -p ~/config/fish/conf.d`. Any files placed in this directory will automatically be sourced by fish on startup. I have my abbreviations (abbr) and oh-my-fish files here.
5. Remove intro to fish message: `set fish_greeting`
6. [Optional] Enable vi keybinds `fish_vi_key_bindings`
7. [Recommended] Install [oh-my-fish](https://github.com/oh-my-fish/oh-my-fish)
   1. [Optional] Install [git plugin](https://github.com/jhillyerd/plugin-git) `omf install https://github.com/jhillyerd/plugin-git`
   2. [Optional] Install [fasd plugin](https://github.com/fishgretel/fasd) `omf install fasd`
   3. [Optional] Install [osx plugin](https://github.com/oh-my-fish/plugin-osx) `omf install osx`
   4. [Optional] Install [tab plugin](https://github.com/oh-my-fish/plugin-tab) `omf install tab`
8. [Recommended] Install [Starship prompt](https://starship.rs)


## Likes:
1. text-replacement style aliases (abbr)
2. rich autocomplete via man page parsing
3. It's something new and different. I've used (in order): csh, tcsh, bash, zsh. Those all feel like the same family. Fish feels like something totally different. A little less UNIX-y and a little more... python-y?

## Dislikes:
1. Terminal.app spawns bash shells on every command for some unknown reason. Use [iTerm2](https://iterm2.com) instead. I'll eventually have to solve this one. I prefer the built-in apps unless there is a very large feature gap to third party solutions. (iTerm2 arguably is exactly that)
2. Fish is not POSIX compliant; this was known before installing. It is just something to be aware of. Use `/bin/sh` for most scripts anyway.
3. Does not support escaping commands. I have a few commands that I like more modern, feature-rich versions of (cat --> bat, top --> htop, vim --> nvim) but there are times where you want the plain old version executed. In zsh, I can escape the command by prepending backslash: `\cat .zshrc`. Fish won't recognize that syntax so I have to edit my abbreviation replacement.

## Follow-Up 1
1. All terminals (not just Terminal.app) were spawning zombie bash shells (on macOS) and sh (on Pop! OS)
2. Tracking down the cullprit: omf plugin for fasd. Removing it fixed the per-command-zombie process!

## Follow-Up 2
1. Dotfiles - I like to maintain all my settings in a dotfiles repository for easy deployment and versioning. Fish and Oh-My-Fish are no exceptions. All of the fish settings are in `~/.config/fish` and omf reside in `~/.config/omf`. Make sure those are versioned for easy deployment.
2. I've added the following omf plugins:
```bash
❯ omf list
Plugins
bang-bang	fzf.fish	git-flow	osx		xcode
fish-spec	git		omf		tab
```
