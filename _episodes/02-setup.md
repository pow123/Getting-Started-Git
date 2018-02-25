---
title: Setting Up Git
teaching: 5
exercises: 0
questions:
- "How do I get set up to use Git?"
objectives:
- "Configure `git` the first time it is used on a computer."
- "Understand the meaning of the `--global` configuration flag."
keypoints:
-   "Use `git config` with the `--global` option to configure a user name, email address, editor, and other preferences once per machine."
---

Git should be already installed on your machines. If you are on Windows, Git came with your gitbash installation. If you are on Mac, Git has been preinstalled on your system.


When we use Git on a new computer for the first time, we need to configure a few things. Below are a few examples of configurations we will set as we get started with Git:

- our name and email address,
- to colorize our output,
- what our preferred text editor is,
- and that we want to use these settings globally (i.e., for every project)

On a command line, Git commands are written as `git verb`, where `verb` is what we actually want to do. The flag `--global` tells Git to use the setting for every project in your user account on this computer.

```shell
$ git config --global user.name "your username"
$ git config --global user.email "your email" 
$ git config --global color.ui "auto"
```
Next, choose from one of the following commands below to add a text editor of your choice.

```shell
#Mac: BBEdit
 $ git config --global core.editor "BBEdit -w"

#Mac: Sublime Text
$ git config --global core.editor "subl -n -w"

#Windows: notepad
$ git config --global core.editor "notepad"

#Windows: notepad++
$ git config --global core.editor "C:/Program Files (x86)/Notepad++/notepad++.exe"

#Linux
$ git config --global core.editor "gedit --wait --new-window"
```

You can check your settings at any time:
```shell
$ git config --list
```
`git config` command has other options. You can get help with this and other git commands by typing
```shell
$ "YourCommand" -h
$ git config -h
$ git config --help
```
So far we have only used `git config` command, but there are many more. You can get an idea about the functionality of Git by taking a look at the available commands.
```shell
$ git
```
We will explore some of them next.
