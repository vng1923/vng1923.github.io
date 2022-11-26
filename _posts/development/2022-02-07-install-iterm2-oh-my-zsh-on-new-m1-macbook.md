---
layout: post
title:  "Install iTerm2 and config oh-my-zsh on M1 MacOS 12 Monterey"
date:   2022-02-07 21:01:05 -0700
categories: [Development]
path: "development"
tags: [ "General" ]
---

### What is iTerm2

iTerm2 is a replacement for Terminal that can do amazing things.

To install iTerm2, it's very easy

```sh
# Terminal: Development
brew install iterm2
```
If you did not install Homebrew yet, please follow my post [here](https://bennguyen.us/2022/02/02/how-to-install-homebrew-on-m1-macos-12-monterey.html){:target="_blank"} to install it.

### After iTerm2 installed. Now let's go with Oh My Zsh

```sh
# Terminal: Development
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

### Install autosuggestions and syntax-highlighting

```sh
# Terminal: Development
brew install zsh-autosuggestions

brew install zsh-syntax-highlighting
```

You can change the theme of Oh My Zsh

```sh
#Terminal: Development
vim ~/.zshrc
ZSH_THEME = "theunraveler"
# theunraveler is a nice time. Sometimes I'm switching between this theme and default theme.
```
*If you guys had any cool theme or plugin, please let me know by leave it in the comment bellow. Thanks all!!!*