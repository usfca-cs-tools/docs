# RISC-V setup

These are instructions for setting up the RISC-V emulator using QEMU and Debian/riscv64. 

Footnote: I borrowed code and instructions from all over, but [Colin Atkinson's instructions](https://colatkinson.site/linux/riscv/2021/01/27/riscv-qemu/) were especially helpful.

## 1. Install QEMU

### macOS
1. *Optional but recommended*: [iTerm2](https://iterm2.com/) is better than Apple Terminal
1. Install Homebrew using the instructions at [brew.sh](https://brew.sh/)
1. Install QEMU from your terminal app
    ```sh
    brew install qemu
    ```
1. Test that you have QEMU correctly installed by running
    ```
    qemu-system-riscv64
    ```

### Windows
1. Install Ubuntu for Windows Subsystem for Linux (WSL) using the instructions at [microsoft.com](https://docs.microsoft.com/en-us/windows/wsl/install)
    1. Don't change the default distribution - Ubuntu is fine
    1. *Optional but recommended:* Review the [Best Practices](https://docs.microsoft.com/en-us/windows/wsl/setup/environment) suggested by Microsoft
1. Install QEMU for 64-bit Windows using the instructions at [qemu.org](https://www.qemu.org/download/#windows)
1. Add to your `PATH` in `~/.bashrc`
    ```sh
    export PATH="/mnt/c/Program Files/qemu":$PATH
    ```
1. Save the file and update your shell environment
    ```sh
    source ~/.bashrc
    ```
1. Test that you have QEMU correctly installed by running
    ```sh
    qemu-system-riscv64
    ```

## 2. Set up RISC-V software
1. Exit `qemu-system-riscv64` if it's running
1. `mkdir debian-riscv64` a directory to hold the Debian/riscv64 software, and `cd` into it. 
1. Download the Debian/riscv [OS image](https://people.debian.org/~gio/dqib/) and `unzip` it
1. `cd artifacts`
1. Go to this Google drive [folder](https://drive.google.com/drive/u/0/folders/1MpRQ2UFY9UpusGkEKQpkjkzhtFXgBCbT) 
1. Download `uboot.elf` and `fw_jump.elf` into the `artifacts/` folder
1. *Optional but recommended*
    1. `start.sh` is a shell script which launches QEMU with the Debian OS image
    1. [`micro`](https://micro-editor.github.io/) is a nice terminal-mode editor with modern keyboard and mouse interactions. I recompiled it for RISC-V since I prefer it to `vim`
    1. `asm.lang` is a hack for `gdb` to do syntax highlighting for RISC-V assembly code in the debugger
1. Make an overlay image for the OS, just in case you mess it up
    ```sh
    qemu-img create -o backing_file=image.qcow2,backing_fmt=qcow2 -f qcow2 overlay.qcow2
    ```

## 3. Boot the Guest OS using QEMU
1. If you're using my `start.sh` script, run it in your terminal:
    ```sh
    ./start.sh
    ```
1. You should see a lot of OS boot messages go by as the OS takes 1-2 minutes to boot
1. The default account and password are `debian/debian`. 
1. You should change the default password using `passwd`

## 4. Install software
1. Give yourself root access (the `#` prompt means you're root)
    ```sh
    su root
    ```
    the default password is `root`
1. Upgrade the OS to the latest (as root)
    ```sh
    apt update && apt upgrade
    ```
    If the OS upgrade leaves your terminal in a bad state, you may wish to shut down the guest (see below) and run the next step in a new terminal.
1. Install development tools (as root)
    ```sh
    apt install build-essential gdb git python3-pip
    ```

## 5. Choose an editor in the guest OS

### vim
1. If you're a `vim` user, you can install it (as root)
    ```sh
    apt install vim
    ```
1. There are `vim` syntax highlighters for RISC-V assembly language. [kylelaker/riscv.vim](https://github.com/kylelaker/riscv.vim) worked for me.

### micro
1. If you prefer to use `micro` you can `scp` it from your host OS onto the guest
    ```sh
    cd artifacts
    scp -P 2222 micro debian@localhost:~
    ```
1. Once back on the guest OS, you can move the `micro` executable to somewhere on your `PATH` (as root)
    ```sh
    mv micro /usr/local/bin/
    ```
1. I wrote a syntax highlighter for RISC-V assembly
    ```sh
    cd ~/.config
    git clone https://github.com/phpeterson-usf/micro
    ```

## 6. *Optional but recommended*: ssh access to the guest OS
1. Although you can log in directly from the guest OS you booted, you may find it convenient to `ssh` to it. Advantages:
    1. You can have multiple windows open to look at source code and the debugger at the same time
    1. You can use SSH forwarding to use `git` on the guest without copying your `ssh` keys to the guest (which is bad security practice)
    1. To set up `ssh` forwarding, edit `~/.ssh/config` to add these lines:
        ```sh
        Host localhost
          ForwardAgent yes
          AddKeysToAgent yes
        ```
1. If you're using my `start.sh` script, you can `ssh -p 2222 debian@localhost`

## 7. Stopping the guest OS
1. If you don't stop the guest OS, it will continue to use about 1 GB of RAM. 
1. When your host OS sleeps, the guest OS generates some gross kernel error messages (which may or may not indicate a real problem)
1. To shut down the guest OS (as root)
    ```sh
    systemctl poweroff
    ```
1. To reboot the guest OS (as root)
    ```sh
    systemctl reboot
    ```