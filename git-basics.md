# git - The Happy Path

## Introduction

1. `Git` is a widely-used system for *distributed version control*. That means multiple people can contribute code to their own local repository (*repo*) and collaborate with other people who are also making changes to their local repos.
1. `Github.com` provides *remote repos* which we will use for turning in work to be graded
1. `Git` is a powerful tool and you can find a lot of documentation on the Internet. My goal is not to comprehensively document everything `git` can do. My goal is to document the happy path for students learning to use `git` on the Unix command line.

## Getting Started

1. If you do not already have an account on [github.com](https://github.com) you should create one
1. If you're using a Windows computer, I recommend you install [Git Bash](https://gitforwindows.org/). If you already have Windows Subsystem for Linux, that's fine too.
1. The `git` client is typically pre-installed on Unix systems such as Apple's MacOS and the Linux systems in the CS Labs network (stargate)

## `ssh` Setup

1. If you do not already have `ssh` keys, you should [create them](ssh-setup.md). `ssh` keys are the typical way to authenticate your `git` changes to `github.com`

## `git` Setup

1. When you run `git` for the first time, you should
    ```
    git config --global user.name "Your Name"
    git config --global user.email your_usf_id@dons.usfca.edu
    ```
1. `git` may need to run an editor for you. To set your preferred editor, edit `~/.bashrc` and add add a line like this if you prefer the `micro` editor (you may prefer `nano`, `vim`, or `emacs`)
    ```
    EDITOR=micro
    ```
    Save the file and quit

## Typical Workflow

1. Your professor will provide a link for you to accept a new assignment in GitHub Classroom. When you accept an assignment (say, `lab01`) GitHub Classroom will create a new repo using the assignment name and your GitHub username, e.g. `lab01-phpeterson`
1. Once you have an assignment repo, you should *clone* the repo onto your computer (or lab host) by copying the repo path to the clipboard and pasting it into the terminal
    ```
    git clone git@github.com:/cs221/lab01-phpeterson
    ```
1. That command will create a directory called `lab01-phpeterson` on your local computer. You should `cd` into that directory and develop your code in that directory.
1. After you create new files in your editor, you should add them to your local repo
    ```
    git add lab01.c
    ```
    If you want to add all of the new (*untracked*) files, you can
    ```
    git add -A
    ```
1. When you want to commit changes to your local repo
    ```
    git commit -m"fix bugs" lab01.c
    ```
    If you want to commit changes in all modified files, you can
    ```
    git commit -am"fix bugs"
    ```
1. When you want to push all changes from your local repo to `github.com`, you can
    ```
    git push
    ```
1. Before an assignment deadline, you should check to make sure your local repo is *clean*, which means no untracked or modified files that you forgot to add/commit/push
    ```
    git status
    ```

## Tips

1. You should commit and push frequently. This creates a version history on `github.com` which is very helpful if you accidentally delete code you meant to keep. There is no Trash folder on the Linux command line -- deleted files are not recoverable.
1. When you're learning `git`, you should make all of your changes in your terminal, rather than on the `github.com` web site. Making changes in multiple places means you have to *merge* remote changes before you can push local changes.

## Merging Changes

1. If you push changes to the remote repo from multiple places (multiple computers, or a computer and then the `github.com` web site), then you can not `git push` new changes until you have merged all remote changes into your local repo. To merge changes into your local repo
    ```
    git pull
    ```
    Git may run your `EDITOR` to prompt you for a merge comment. You can save your comment and quit the editor
1. After pulling remote changes into your local repo, you will be able to `git push` to the remote.

