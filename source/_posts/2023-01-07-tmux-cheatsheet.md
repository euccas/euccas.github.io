---
layout: post
title: "Tmux Cheatsheet"
date: 2023-01-07 20:37:11 -0800
comments: true
categories: linux tools
keywords: Tmux Screen
description: Tmux common usages, Tmux vs. Screen
---
_Note: This post is written with the help of [ChatGPT](https://chat.openai.com/chat) (Dec 15 version)._

# What is Tmux

[Tmux](https://github.com/tmux/tmux/wiki) is a terminal multiplexer for Unix-like systems. Similar to [Linux Screen](https://linux.die.net/man/1/screen), Tmux allows you to create, manage, and easily switch between multiple terminal sessions within one single terminal window or console. It also has features such as the ability to detach and reattach sessions, split terminal windows into panes, and more. It is useful for managing multiple terminal sessions and for running long-running commands in the background while you do other work in the same terminal window.

# Tmux vs. Screen

One difference between the Tmux and Screen is that Tmux is more modern and has a more user-friendly interface, with support for mouse operations and better window and pane management. Screen, on the other hand, is an older tool that is more lightweight and simple, and does not have as many features as Tmux.

Another difference is that Tmux is more configurable and extensible, with support for custom scripts and plugins, while Screen is more bare-bones and does not have as much support for customization.

Ultimately, the choice between Tmux and Screen depends on your personal preferences and needs. Both are powerful tools that can be useful in different situations.

To learn more about the usage of Screen, please read another post in this blog: [The Element of Linux Screen](https://euccas.github.io/blog/20140531/the-elements-of-linux-screen.html).


# Tmux common usages

### Install tmux on Mac

- `brew install tmux`

### Start a new session

- `tmux new`: start a session, the session gets an automatically generated name.
- `tmux new -s <session name>`: start a session with specified name.

### List tmux sessions

- `tmux ls`

### Kill a tmux session

- `tmux kill-session`: kill the last session.
- `tmux kill-session -t <session name>`: kill the session with specified name.

### Attach to session

- `tmux attach-session`: attach to the last session.
- `tmux attach-session -t <session name>`: kill the session with specified name.
- `tmux a`: shortcut of tmux attach-session

### Working with tmux windows

When you start a new Tmux session, by default, it creates a single window with a shell in it. You can create more windows and switch between them.

- `Ctrl+b c`: Create a new window
- `Ctrl+b w`: Show window list and choose from it
- `Ctrl+b n`: Move to the next window
- `Ctrl+b p`: Move to the previous window
- `Ctrl+b 0`: Switch to window 0
- `Ctrl+b ,`: Rename the current window
- `Ctrl+b &`; Kill the current window
