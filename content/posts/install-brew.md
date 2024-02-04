---
title: guide - install brew on your mac
categories:
  - by sublime
  - guide
description: 
summary: "this is a clear guide on how to install brew on your mac. bonus: list of useful packages and apps you can install with brew!"
tags: 
keywords: install brew mac locally homebrew terminal
draft: false
weight: 0
aliases: 
showToc: false
cover:
  image: 
  alt: ""
  caption: ""
  relative: false
date: 2023-11-25T11:47
lastmod: 2024-02-04T13:27:02
publishdate: 2222-02-22T02:02:00
---

if you use a mac, the best way to install packages and apps would be to use [brew](https://brew.sh).

to prepare to install brew on your mac, firstly you open up the "Terminal.app"

make sure you have the command line tools installed by running the command 
```xcode-select --install```

this could take a few minutes.


## installing globally

when you install brew globally, this means that you install brew for all users of the mac.
this requires admin permissions so the password of an admin user will be required.

if your user is not an admin, scroll down to see how to install brew locally.

you have two wats of installing brew globally: running the installer or running the install script.

you can find and download the latest `.pkg` installer from  [brew releases](https://github.com/Homebrew/brew/releases), which you can double click to run the installer.

if you would like to use the install script, brew can be installed with this command

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## installing locally

you can still install brew if you are not an admin by installing brew in yout local path.

according to my precious experience, installing brew locally can take around 5 minutes :(
maybe brew needs to compile or something, i'm not sure. just keep in mind that some of these commands can take a long time.

to install brew locally, first navigate to the directory where you want homebrew to be installed, which preferably is your home directory.

and then you run these commands. the first one creates a folder named `homebrew` and the second command downloads and extracts the homebrew source code into the folder you just created.

```
mkdir homebrew
curl -L https://github.com/homebrew/brew/tarball/master | tar xz --strip 1 -C homebrew
```
now there should be a binary executable located at `./homebrew/bin/brew` 

better to be safe than sorry, you will need to make sure the brew executable can run with the command
```
chmod +x ./homebrew/bin/brew
```
the `bin` folder contains the packages you will install with brew, but it's not in your path, which means that if you try to use brew right now it will say the command is not found.

you need to add your brew bin path to your path by adding a line your `$HOME/.zprofile` file
```
echo "PATH=$PATH:$(cd "$(dirname "./homebrew/bin")" && pwd)/$(basename "./homebrew/bin")" >> $HOME/.zprofile
```
now that brew is added to your path, you can close your terminal window and open a new one. 

let's do one final command to make sure that brew is installed properly:
```
brew update-reset
```
now congrats, brew is installed!


## bonus: list of useful packages and apps

you can find some useful brew packages at <https://github.com/sublimeclemency/sublimeclemency/blob/main/mac-brew.sh>

and, brew can also install apps as well. here is a list of awesome recommended apps to install: <https://github.com/sublimeclemency/sublimeclemency/blob/main/mac-apps-brew.txt>



PS oh phew, writing this guide was tiring. i wrote this guide for my friends and i hope my guide was clear and concise enough :)