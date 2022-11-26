---
layout: post
title:  "How to install homebrew on M1 MacOS 12 Monterey"
date:   2022-02-01 21:01:05 -0700
categories: [Development]
path: "development"
tags: ["General"]
---

Today, I've just got new M1 Macbook Pro from my work. I have to re-setup my development envirnoment. So I noted my process here.

### What is Homebrew
Homebrew is a package installer that helps us install the stuff you need that MacOS didn't.

For example, you need PHP, you can install it using Homebrew.

### Install Homebrew
To install Homebrew, you can follow this [page](https://brew.sh/){:target="_blank"} or run this command in Terminal:

```sh
# Terminal: Development
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

After the installation completed, run these commands in your Terminal:
```sh
# Terminal: Development
export PATH="/opt/homebrew/bin:$PATH"
echo 'export PATH="/opt/homebrew/bin:$PATH"' >> $HOME/.zshrc
source ~/.zshrc
```

Final, use this command to check to make sure it works
```sh
# Terminal: Development
brew doctor
```