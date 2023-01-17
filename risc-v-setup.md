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

### Windows
1. Install Ubuntu for Windows Subsystem for Linux (WSL) using the instructions at [microsoft.com](https://docs.microsoft.com/en-us/windows/wsl/install)
    1. Don't change the default distribution - Ubuntu is fine
    1. *Optional but recommended:* Review the [Best Practices](https://docs.microsoft.com/en-us/windows/wsl/setup/environment) suggested by Microsoft
1. Install QEMU for Ubuntu 
    ```sh
    sudo apt install qemu-misc qemu-system qemu-system-misc
    ```

## 2. Install Debian/riscv64 as a Guest OS

1. Go to this Google drive [folder]() and download debian-riscv64.zip to your laptop
1. `unzip debian-riscv64.zip` to create the directory `debian-riscv64/` and `cd` into it
1. Make an overlay image for the OS, just in case you mess it up
    ```sh
    qemu-img create -o backing_file=image.qcow2,backing_fmt=qcow2 -f qcow2 overlay.qcow2
    ```
1. Boot the guest OS using QEMU
    ```sh
    cd debian-riscv64
    ./start.sh
    ```
1. You should see a lot of OS boot messages go by as the OS takes 1-2 minutes to boot
1. The default account and password are `debian/debian`. 
1. You should change the default password using `passwd`

## 3. Install OS software on the Guest

1. Give yourself root access 
    ```sh
    su root
    ```
    the default password is `root`. The `#` prompt means you're root
1. As root, upgrade the OS to the latest. This will take some time.
    ```sh
    apt update && apt upgrade
    ```
1. As root, install development tools. This will take some time.
    ```sh
    apt install build-essential gdb git python3-pip
    ```
1. As root, change the time zone from UTC to US/Pacific time
    ```sh
    ln -sf /usr/share/zoneinfo/America/Los_Angeles /etc/localtime
    ```

## 4. Configure `ssh` access to the Guest OS

1. Although it's possible to log in directly from the guest OS you booted, we recommend you `ssh` to it in a new terminal window.
1. **Important:** The guest OS must be running for these steps, but run these steps on your laptop.
1. Edit `~/.ssh/config` to add these lines:
    ```
    Host riscv
        HostName localhost
        ForwardAgent yes
        AddKeysToAgent yes
        IdentityFile ~/.ssh/ed25519_key
        User debian
        Port 2222
    ```
1. To copy your public key from your host OS to the `authorized_keys` file on the guest OS
    ```sh
    ssh-copy-id riscv
    ```
1. If you want to use the [micro editor](https://micro-editor.github.io/) we have provided a RISC-V binary in the zip file. To use it on the guest, you can `scp` it from your host OS to the home directory (`~`) for the `debian` user
    ```sh
    cd debian-riscv64
    scp micro riscv:~
    ```
1. Copy gdb syntax highlighting to the `debian` home directory
    ```sh
    scp asm.lang riscv:~
    ```
1. You can now 
    ```sh
    ssh riscv
    ``` 
    when the guest OS is running 

## 5. Install tools as `root`

**You must `su root` before doing these steps**

### vim
1. If you're a `vim` user, you can install it
    ```sh
    apt install vim
    ```

### micro
1. If you're a `micro` user, you should ensure that `micro` is executable and move it to `/usr/local/bin`
    ```sh
    chmod 0755 micro
    mv micro /usr/local/bin/
    ```

### gdb
1. To configure RISC-V syntax highlighting in `gdb` move `asm.lang` into `source-highlight`
    ```sh
    cd /usr/share/source-highlight/
    mv asm.lang asm.lang.orig
    mv /home/debian/asm.lang .
    ```

## 6. Install tools as `debian` (not `root`)

If you are `root` here, you can use ^D (CTRL-D) to become the `debian` user again

### git
1. To configure git
    ```sh
    git config --global user.email "you@dons.usfca.edu"
    git config --global user.name "Your Name"
    ```

### micro
1. We have developed a syntax highlighter for RISC-V assembly language
    ```sh
    cd ~
    mkdir .config
    cd .config
    git clone git@github.com:/phpeterson-usf/micro
    ```

### vim
1. There are `vim` syntax highlighters for RISC-V assembly language. [kylelaker/riscv.vim](https://github.com/kylelaker/riscv.vim) worked for me.

### autograder
1. To install the grading script
    ```sh
    cd ~
    git clone git@github.com:/phpeterson-usf/autograder
    ```
1. To install the test cases for the grading script
    ```sh
    cd ~
    git clone git@github.com:/cs315-s23/tests
    ```

## 7. Stopping the guest OS

1. If you don't stop the guest OS, it will continue to use about 2 GB of RAM on your laptop.
1. When your host OS sleeps, the guest OS generates some gross kernel error messages (which may or may not indicate a real problem)
1. To shut down the guest OS, first make yourself `root` as described above, then
    ```sh
    systemctl poweroff
    ```
