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
