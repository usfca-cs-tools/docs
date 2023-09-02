# `git` - next steps

### Background

This document is a follow-up to my [git basics](git-basics.md) document, intended to be used after learning the add/commit/push workflow.

## One feature/fix per commit

1. Students sometimes collect a lot of changes into one commit and commit them all together. This approach seems to consider github as the way to "turn in" solutions for programming assignments, but professionals use `git` remote repos in a different way.
1. You should work on one thing (a bug fix or a feature) at a time, and commit only the changes for that task.
1. The reason for this is that some commits turn out to cause problems or disagreement once the change is visible. DevOps engineers want to revert only one change without losing a pile of other valuable changes.

## Write good commit messages

1. Commit messages like "works", "yay", or "finally" are not helpful for colleagues to understand your work.
1. Organizations frequently use prefixes [like these](https://dev.to/varbsan/a-simplified-convention-for-naming-branches-and-commits-in-git-il4) to explain your intention. Think of them like "turn signals" for your car, communicating with those around you.

## Use `.gitignore`

1. You should not commit build products to `git`
1. In C, we want to ignore `.o` files and executables. In Go, temporary executable files have the prefix `__debug_bin`
1. To make `git` ignore a file, create a file in your repo called `.gitignore` and add a line for the type of files you want to ignore, e.g.
    ```
    *.o
    __debug_bin*
    ```
1. To be extra clever, you could name files you never want to ignore, e.g.
    ```
    !*.c
    !*.go
    ```

## Branching

### Background

1. You might want to commit "work in progress" (WIP) which leaves the code in an non-working state. If your laptop were lost/stolen/damaged with a lot of uncommitted work, you would be very sad.
1. Since you don't want to disrupt your colleagues by pushing non-working code to the remote repo, you should create a branch (like on a tree)
1. A branch is separate stream of commits which continues until it is ready to be "merged" to the `main` branch.
1. Organizations frequently require developers to do new features or bug fixes on a branch, until they can be code-reviewed and merged.

### Creating branches

1. To see the branches in your local repo
    ```
    $ git branch
    * main
    ```

1. To create a branch in your local repo (This does NOT switch your local code to the new branch)
    ```
    $ git branch new_feature
    ```
    
1. To switch your local code to the new branch
    ```
    $ git checkout new_feature
    ```

1. To check that you're on the new branch
    ```
    $ git branch
    main
    * new_feature
    ```

1. Shortcut to create a new local branch and switch to it
    ```
    $ git checkout -b new_feature
    ```

### Pushing commits to the remote

1. When you have committed changes to the local repo, you'll need to create the new branch on github.com
    ```
    git push -u origin new_feature
    ```
1. You may be used to using `git push` by iteself. That's a shortcut for 
    ```
    $ git push -u origin HEAD
    ```
    where HEAD means the tip of the current branch

### Deleting a branch

1. Please don't delete branches because you will be asked to show them during code reviews

### Merging to `main`

1. When you're done with the feature or fix on a branch, you can merge it to the `main` branch
1. Make sure your tree is clean with no modifications or untracked files. This is **critical!** Do not checkout on top of modified files or you will lose the changes
    ```
    $ git status
    On branch new_feature
    Your branch is up to date with 'origin/new_feature'.

    nothing to commit, working tree clean
    ```
1. Overwrite your local tree with the contents of main
    ```
    $ git checkout main
    $ git merge new_feature
    ```
1. Push the merged code to the remote
    ```
    $ git push
    ```