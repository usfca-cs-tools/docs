# RISC-V setup

## Background

1. These are instructions for connecting to the debian/riscv64 environment running on griffin. Griffin is a host inside the CS Labs network
1. I originally intended to have everyone run QEMU and the emulated OS on your own laptops, but the Debian distribution seems to have package version problems that I can't resolve.
1. Therefore, as a plan B, I've copied a working QEMU+debian/riscv64 build onto that machine that cs315-s23 students can use.

## 1. Configure `ssh` access to stargate

1. If you don't already have ssh keys set up for stargate, please follow [these instructions](ssh-setup.md)
1. From your laptop, connect to stargate
    ```
    ssh stargate
    ```

## 2. Configure `ssh` access to griffin

1. From stargate, connect to griffin
    ```
    ssh griffin
    ```
1. On griffin, edit `~/.ssh/config` to add these lines:
    ```
    Host *
        ForwardAgent yes
    Host riscv
        HostName localhost
        ForwardAgent yes
        AddKeysToAgent yes
        User your_usf_username
        Port 2222
    ```
1. On griffin, copy your public key from your laptop to the `authorized_keys` file on the debian/riscv64 OS
    ```sh
    ssh-copy-id riscv
    ```
1. On griffin 
    ```sh
    ssh riscv
    ``` 

## 3. Install tools

### Syntax highlighting for micro
1. If you use the micro editor, we have developed a syntax highlighter for RISC-V assembly language
    ```sh
    cd ~
    mkdir .config
    cd .config
    git clone git@github.com:/phpeterson-usf/micro
    ```

### Syntax highlighting for vim
1. If you use the vim editor, there are `vim` syntax highlighters for RISC-V assembly language. [kylelaker/riscv.vim](https://github.com/kylelaker/riscv.vim) worked for me.

### autograder
1. To install the grading script
    ```sh
    cd ~
    git clone git@github.com:/phpeterson-usf/autograder
    cd autograder
    pip3 install -r requirements.txt
    ```
1. Add autograder to your path
    ```
    cd ~
    nano .bashrc
    ```
    Add the line
    ```
    export PATH=~/autograder/$PATH
    ```
    Save and quit. Now reload the shell environment
    ```
    source ~/.bashrc
    ```
1. To install the test cases for the grading script
    ```sh
    cd ~
    git clone git@github.com:/cs315-s23/tests
    ```

## 4. Test that git and autograder work

1. You should be able to clone your lab repo
    ```
    git clone git@github.com:/cs315-s23/lab01-yourgithub
    ```
1. You should be able to grade your lab repo
    ```
    cd lab01-yourgithub
    grade test -p lab01
    ```