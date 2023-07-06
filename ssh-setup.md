# How to set up `ssh`

1. Set up ssh access to github.com
    1. If you already have ssh keys which work with GitHub, you can skip this step
    1. Create ssh key pair
    1. copy public key to github
    1. `ssh git@github.com`. You should expect to see:
        ```sh
        $ ssh git@github.com
        Enter passphrase for key '/c/Users/phil/.ssh/id_rsa':
        PTY allocation request failed on channel 0
        Hi phpeterson-usf! You've successfully authenticated, but GitHub does not provide shell access.
        Connection to github.com closed.
        ```
    1. Windows: ssh agent

1. Terminal setup (<a onclick="toggle_display('terminal_mac')">Mac</a>, <a onclick="toggle_display('terminal_win')">Windows</a>)

    <div id="terminal_mac" class="div-toggle" style="display:none" markdown=1>
    For Mac:
    - Apple's Terminal app should work ok
    - I prefer [iTerm2](https://iterm2.com/) because it works well with my preferred terminal-mode editor, [micro](https://iterm2.com/)
    </div>

    <div id="terminal_win" class="div-toggle" style="display:none" markdown=1>
    For Windows:
    - I recommend using [Git For Windows](https://gitforwindows.org/). Git Bash offers a Unix-like shell environment.
    - If you already have [Windows Subsystem for Linux](https://learn.microsoft.com/en-us/windows/wsl/install), that's also fine
    </div>

<script>
    function toggle_display(id_name) {
        var e = document.getElementById(id_name);
        if (e.style.display === "none") {
            e.style.display = "block";
        } else {
            e.style.display = "none";
        }
    }
</script>
