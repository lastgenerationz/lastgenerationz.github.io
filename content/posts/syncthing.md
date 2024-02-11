---
title: guide - use syncthing to sync files between computers (with git for version control)
categories:
  - by sublime
  - guide
description: 
summary: how to install syncthing and use it to sync files, and also use git to do version control
tags: 
keywords: 
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
lastmod: 2024-02-04T17:25:07
publishdate: 2024-02-03T16:04:00
---

i needed to sync files between my computers so i used syncthing and git to sync and also used git for version control.

## syncthing

[syncthing](https://github.com/syncthing/syncthing) is the most used open source file syncing utility.


### install syncthing

you should use brew. i made a guide to [installing brew on your mac](/posts/install-brew)

brew works on linux too
to install it with brew, you just run the command `brew install syncthing`

after the installation completes, you should run 
```
brew services start syncthing
```
to make the syncthing service start 

here's how to [install syncthing on windows](https://www.geeksforgeeks.org/how-to-download-and-install-syncthing-on-windows/).

and here's [how to install syncthing on ubuntu linux](https://computingforgeeks.com/how-to-install-and-use-syncthing-on-ubuntu/)

if you need help installing syncthing, i suggest searching for guides on youtube.

### autostart syncthing

now you need to make sure syncthing can run every time you boot your computer.

if you used brew to install syncthing you run 
```
brew services start syncthing
```

if you did not use brew to install syncthing, the syncthing docs, <https://docs.syncthing.net/users/autostart.html,> can help you.


### use syncthing

to use syncthing, you use the webui at <http://localhost:8384> to see the syncthing user interface.

syncthing has created a default sync folder in your home directory but you should ignore that. 

to sync one of your folders, press the "add folder" button at the bottom and give it an id and also input the directory where you folder is.

when you have multiple devices that have syncthing installed, you can find other device ids and you can connect devices together to start syncing.

if you create a file named `.stignore` in one of your syncthing folders, you can add one ignore pattern per line, to make syncthing ignore some files and folders and not to sync them. see <https://docs.syncthing.net/users/ignoring.html> for more information on how to use ignore patterms.


with syncthing, you now have reliable and useful file syncing. congrats!


## git

git is used for version control and is useful for managing commits (changes) to files and provides options to rollback any commits.

git can be used alongside with syncthing to sync the history versions of your files, in addition to the files themselves.

if you use a terminal to navigate to one of your syncthing folders, you can initialize a git repository to put commits to your folder with

```
git init
```

now edit `.stignore` file to my sync the active git branch by adding the ignore pattern `.git/HEAD`

then stage all files to the repo's first commit

```
git add *
```

you can edit the git author information with these commands, you can set the name and email to just a single letter because it doesn't really matter; authoring information is only useful for published repos on github.

```
git config user.name "example"
git config user.email "i@example.com"
```

and commit the initial commit

```
git commit -m "initial commit"
```

the git repo should be set up, and you can use some other git app like [sublime merge](https://www.sublimemerge.com/) to open the repo and you can commit new commits and see your files history and differences.


in case you forgot, you can edit a `.gitignore` file at the base directory of your repo and you can choose what patterns to ignore and not get tracked by git. you can find some help on ignore patterns at <https://www.atlassian.com/git/tutorials/saving-changes/gitignore>


