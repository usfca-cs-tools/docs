# RISC-V setup

These are instructions for setting up the RISC-V emulator using QEMU and Ubuntu/riscv64. 

## 1. Install QEMU

We will use the [QEMU](https://www.qemu.org/) emulation environment to execute the RISC-V version of Ubuntu on your computer

### macOS
1. *Optional but recommended*: [iTerm2](https://iterm2.com/) is better than Apple Terminal
1. Install Homebrew using the instructions at [brew.sh](https://brew.sh/)
1. Add `brew` to your `PATH` environment variable
    ```
    cd
    nano .zprofile
    ```
    add this text
    ```
    export PATH=/opt/homebrew/bin:$PATH
    ```
    1. `CTRL-O` and return to write the file
    1. `CTRL-X` to exit `nano`
    1. `CTRL-D` to exit your terminal
    1. Open a new terminal which will include your change to the `PATH` environment variable
1. Install QEMU from your terminal app
    ```sh
    brew install qemu
    ```

### Windows

1. Install Ubuntu for Windows Subsystem for Linux (WSL) using the instructions at [microsoft.com](https://docs.microsoft.com/en-us/windows/wsl/install)
    1. Use the Ubuntu distribution
    1. Choose your Ubuntu name and password
    1. Once your Ubuntu terminal is running, get the latest Ubuntu software for your laptop
        ```
        sudo apt update && sudo apt upgrade
        ```
1. Install QEMU for Ubuntu 
    ```sh
    sudo apt install qemu-misc qemu-system qemu-system-misc
    ```

## 2. Install Ubuntu/riscv64 as a Guest OS

In your terminal window

1. Create a directory for this course and `cd` into it
    ```
    mkdir cs315
    cd cs315
    ```
1. Download the RISC-V build of Ubuntu
    ```
    curl https://www.cs.usfca.edu/~benson/cs315/files/ubuntu-22.04-riscv.zip --output ubuntu-22.04-riscv.zip
    ```
1. Uncompress the zip file and `cd` into the resulting directory
    ```
    unzip ubuntu-22.04-riscv.zip
    cd ubuntu-22.04-riscv
    ```
1. Run the Ubuntu guest OS
    ```
    ./start.sh
    ```
1. You should see a bunch of boot messages go by. Once the OS has booted you can log in using 
    - username: ubuntu
    - password: goldengate

## 3. Set up ssh and git

1. **Prerequisites**: Before beginning these steps, you should have an public/private keypair set up on your computer and on github.com
1. Open a new terminal window on your computer (leaving the Ubuntu guest running in the first terminal)
1. Edit your ssh config file
    ```
    cd ~/.ssh
    nano config
    ```
1. Add the following lines
    ```
    Host riscv
    HostName 127.0.0.1
    Port 4444
    AddKeysToAgent yes
    ForwardAgent yes
    User ubuntu
    ```
1. Copy your public key to the running guest OS
    ```
    ssh-copy-id riscv
    ```
1. Test ssh access to the running guest OS
    ```
    ssh riscv
    ```
    You should be logged in to the guest OS
1. From the guest, test access to github
    ```
    ssh git@github.com
    ```
1. You should see this
    ```
    Hi phpeterson-usf! You've successfully authenticated, but GitHub does not provide shell access.
    Connection to github.com closed.
    ```
    If github gives you a publickey error, that probably means you don't have SSH set up correctly to github.
1. Tell git who you are
    ```
    git config --global user.email "you@example.com"
    git config --global user.name "Your Name"
    ```
## 4. Set up an editor

1. When learning a new language, such as RISC-V assembly language, syntax highlighting can be very helpful. Here are two options:
    1. If you're a `vim` user, syntax highlighting for RISC-V is [available](https://github.com/kylelaker/riscv.vim)
    1. [micro](https://micro-editor.github.io/) is a helpful text editor, and we have included a RISC-V build in the Ubuntu guest OS image. 
        1. Although micro does not include RISC-V syntax highlighting by default, we have developed tools you can use. Do this on your running guest
            ```
            cd ~/.config
            git clone git@github.com:/phpeterson-usf/micro
            ```

## 5. Set the time zone

1. In order for your code pushes to github to have the correct time stamp
you should set the time zone:
    ```sh
    sudo timedatectl set-timezone America/Los_Angeles
    ```