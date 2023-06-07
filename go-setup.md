# How to set up your Go environment

## Prerequisites

1. Basic knowledge of the Unix shell ([tips](shell-basics.md))
1. Basic knowledge of version control using `git` ([tips](git-basics.md))
1. `ssh` keys already set up ([steps](ssh-setup.md))

## Steps

1. Install the [Go toolchain](https://go.dev/dl/). Be careful to choose the right build for your laptop
    1. Windows laptops need the `windows-amd64` build
    1. Newer Apple laptops with M1 or M2 processors need the `darwin-arm64` build
    1. Older Apple laptops with Intel processors need the `darwin-amd64` build
1. On MacOS the Go toolchain installs into `/usr/local/` and is automatically added to the `PATH` (by installing itself into `/etc/path.d/`)
    ```sh
    phil@Phils-MacBook-Pro:~ % which go
    /usr/local/go/bin/go

    phil@Phils-MacBook-Pro:~ % go version
    go version go1.20.4 darwin/arm64
    ```
1. On Windows 11 the Go toolchain installs into `C:\Program Files\Go` and is added to the `PATH` automatically
    ```sh
    phil@PHILPETERSO43DB MINGW64 /
    $ which go
    /c/Program Files/Go/bin/go

    phil@PHILPETERSO43DB MINGW64 /
    $ go version
    go version go1.20.4 windows/amd64
    ```
1. Install the `dlv` ([delve](https://github.com/go-delve/delve)) debugger.
    ```sh
    go install github.com/go-delve/delve/cmd/dlv@latest
    ```
    1. Edit your shell config file (MacOS: `~/.zshrc`, Git Bash: `~/.bashrc`) to add
        ```sh
        export PATH=~/go/bin:$PATH
        ```
    1. dlv hangs on Git Bash on Parallels. WSL doesn't work on Apple Silicon. Need to try on a real Windows machine.
1. Optional: If you want to use an Integrated Development Environment (IDE), you may use [VS Code](https://code.visualstudio.com/). 
    1. VS Code will offer to install extensions for `go` and `gopls`. You should accept both. 
1. Unsupported: There is a Go-specific IDE called [GoLand](https://www.jetbrains.com/go/) that you're welcome to try. I won't be supporting it.

## A word about `GOPATH`

1. Any software you `go install`, either manually, or using VS Code, will install into the directory specified by the `GOPATH` environment variable
1. I recommend you do not set `GOPATH`, but let it default to `~/go` (that is, the directory named "go" in your home directory)
1. If you want to tinker with changing `GOPATH` to something else, remember to change both the shell environment and VS Code settings
1. It won't work to make `GOPATH` point to `/usr/local/go` because those directories are only writable by the `root` user.