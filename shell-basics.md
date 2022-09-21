# Navigating the Unix/Linux shell

1. The command-line interface to Unix-like operating systems (like Linux or macOS) is a program called the shell, which takes your typed commands and executes the programs you specify.
1. There are several common shell programs:
    1. On our CS Labs systems, we use Red Hat Linux, which provides the `bash` shell. `bash` uses a `$` as the command prompt. 
    1. macOS provides the `zsh` shell, which has a `%` as the command prompt


## Navigating Directories

1. The filesystem is organized into a tree of directories (aka folders) and files. Therefore a directory may contain other directories or files.
1. You navigate the tree using these commands
    to print the working directory
    ```
    $ pwd
    ```
    to list the contents of a the current directory
    ```
    $ ls
    ```
    to list the contents of a subdirectory
    ```
    $ ls dirname
    ```
    to change the working directory
    ```
    $ cd dirname
    ```
    to return to a parent directory
    ```
    $ cd ..
    ```
1. The special name `'.'` means "here, the directory I'm in". Therefore `$ ./myprogram` means run `myprogram` which lives in the current directory.
1. The special name `'~'` means "my home directory". Therefore 
    ```
    $ nano ~/.bashrc
    ``` 
    means run the `nano` editor on the file `.bashrc`, which lives in my home directory.
1. File names which begin with the character `'.'` are hidden in `ls` output. To see all files, use `ls -a` (`-a` means "all")

## Creating and Deleting Files and Directories

1. To create files in a text editor
    ```
    $ nano test.c
    ```
1. To remove files from the filesystem (be careful, there is no Trash, and no Undo)
    ```
    $ rm test.c
    ```
1. To create a directory
    ```
    $ mkdir subdir
    ```
1. To remove a non-empty directory  (`rm -rf` means remove contents recursively, forcibly. Think twice before doing this)
    ```
    $ rm -rf subdir
    ```

## Using a Text Editor in a Terminal app

1. To create text files (like source code) using a text editor, like [nano](https://www.nano-editor.org/), [vi/vim](https://www.vim.org/), or [micro](https://micro-editor.github.io/) (Phil uses micro in lecture).
    ```
    $ micro test.c
    ```
1. Keyboard shortcuts are available for [nano](https://www.nano-editor.org/dist/latest/cheatsheet.html), [vim](https://vim.rtorr.com/), [micro](https://github.com/zyedidia/micro/blob/master/runtime/help/keybindings.md). Micro is most like Mac/Windows, using CTRL-S for Save, CTRL-O for Open, etc.

## Copying files and directories

1. To make a copy of a file
    ```
    $ cp test.c test.bak
    ```
1. To make a copy of a directory, including its contents (`-r` means recursive)
    ```
    $ cp -r subdir subdir.bak
    ```
1. To copy the contents of a directory to the current directory
    ```
    $ cp -r subdir/* .
    ```