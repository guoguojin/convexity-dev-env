# Nix flake for creating a basic development environment

## What is this?

Nix development shells allow you spin up custom development environments without affecting your installed system, like Python virtual environments,
but for any coding environment. Here we are leveraging Nix flakes to ensure that we can create consistent and reproducable development environments.

## Why?

1.  You want to test new versions of Go, or Go tools as part of your development workflow without breaking your development environment.
2.  You work in a team and you want an easy way for everyone to use the save development environment.
3.  You have different projects that require different toolchains.

## Pre-requisites

To use make sure you have the Nix package manager installed and have the `nix-command` and `flakes` experimental features enabled
as described [here](https://nixos.wiki/wiki/Flakes).

Install [direnv](https://direnv.net/) and make sure it is hooked into your shell.

## Usage

### Using this environment directly

1.  Make sure you have the pre-requisites installed.
2.  In the root of your Go project create an `.envrc` pointing to this flake:
    
    ```bash
    echo "use flake github:guoguojin/convexity-dev-env" > .envrc
    ```

3.  If you have `direnv` correctly hooked into your shell you should see a warning:

    ```text
    direnv: error /path/to/your/project/.envrc is blocked. Run `direnv allow` to approve its content
    ```

4.  Run `direnv allow` as instructed and you should see logs detailing what is being installed and your environment being initialised:

    ```text
    Setting XDG_CACHE to /home/tanq/.cache
    Found go.mod, running tidy
    ...
    Go development shell
    go version go1.20.5 linux/amd64
    GOROOT=/nix/store/i3ab37h47xmd0zh75708gj57hah7v7f4-go-1.20.5/share/go
    GOPATH=/home/tanq/.cache/dev-shell//home/tanq/code/personal/projects/signal-generator/go
    direnv: export <list of your environment variables available in your development shell>
    ```

Your development environment shell is ready to use. 

> Note: 
  If you are using GoLand or IntelliJ IDEA with the Go plugin, you will need to change the GOROOT and GOPATH
  for the project to the paths specified by the shell. 
  If you are using VS Code, starting `code` from the terminal while you're inside the development shell it should
  pick up the GOROOT and GOPATH from the environment variables. Otherwise you will need to set them accordingly in
  the settings.json

