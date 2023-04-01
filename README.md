# Cairo 1.0 installer

This tool installs [Cairo 1.0](https://github.com/starkware-libs/cairo).

## Prerequisites

[Git](https://git-scm.com/) installed.

[Rust](https://www.rust-lang.org/) installed. You can easilly install it running:

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

## Installation / Update / Uninstallation

Once prerequisites have been installed correctly:

### Install

If you wish to install a specific release of Cairo rather than the latest head, set the `CAIRO_GIT_TAG` environment variable (e.g. `export CAIRO_GIT_TAG=v1.0.0-alpha.6`).

```bash 
curl -L https://github.com/franalgaba/cairo-installer/raw/main/bin/cairo-installer | bash
```

After installing, follow [these instructions](#set-up-your-shell-environment-for-cairo) to set up your shell environment.

### Update

```
rm -fr ~/.cairo
curl -L https://github.com/franalgaba/cairo-installer/raw/main/bin/cairo-installer | bash
```

### Uninstall

Cairo is installed within `$CAIRO_ROOT` (default: ~/.cairo). To uninstall, just remove it:

```bash
rm -fr ~/.cairo
```

then remove these three lines from .bashrc:

```bash
export PATH="$HOME/.cairo/target/release:$PATH"
```

and finally, restart your shell:

```bash
exec $SHELL
```

## Set up your shell environment for Cairo

* Define environment variable `CAIRO_ROOT` to point to the path where
  Cairo will store its data. `$HOME/.cairo` is the default.
  If you installed Cairo via Git checkout, we recommend
  to set it to the same location as where you cloned it.
* Add the `cairo-*` executables to your `PATH` if it's not already there

The below setup should work for the vast majority of users for common use cases.

  - For **bash**:

    Stock Bash startup files vary widely between distributions in which of them source
    which, under what circumstances, in what order and what additional configuration they perform.
    As such, the most reliable way to get Cairo in all environments is to append Cairo
    configuration commands to both `.bashrc` (for interactive shells)
    and the profile file that Bash would use (for login shells).

    First, add the commands to `~/.bashrc` by running the following in your terminal:

    ~~~ bash
    echo 'export CAIRO_ROOT="$HOME/.cairo"' >> ~/.bashrc
    echo 'command -v cairo-compile >/dev/null || export PATH="$CAIRO_ROOT/target/release:$PATH"' >> ~/.bashrc
    ~~~

    Then, if you have `~/.profile`, `~/.bash_profile` or `~/.bash_login`, add the commands there as well.
    If you have none of these, add them to `~/.profile`.

    * to add to `~/.profile`:
      ~~~ bash
      echo 'export CAIRO_ROOT="$HOME/.cairo"' >> ~/.profile
      echo 'command -v cairo-compile >/dev/null || export PATH="$CAIRO_ROOT/target/release:$PATH"' >> ~/.profile
      ~~~

    * to add to `~/.bash_profile`:
      ~~~ bash
      echo 'export CAIRO_ROOT="$HOME/.cairo"' >> ~/.bash_profile
      echo 'command -v cairo-compile >/dev/null || export PATH="$CAIRO_ROOT/target/release:$PATH"' >> ~/.bash_profile
      ~~~

  - For **Zsh**:
    ~~~ zsh
    echo 'export CAIRO_ROOT="$HOME/.cairo"' >> ~/.zshrc
    echo 'command -v cairo-compile >/dev/null || export PATH="$CAIRO_ROOT/target/release:$PATH"' >> ~/.zshrc
    ~~~

    If you wish to get Cairo in noninteractive login shells as well, also add the commands to `~/.zprofile` or `~/.zlogin`.

  - For **Fish shell**:

    If you have Fish 3.2.0 or newer, execute this interactively:

    ~~~ fish
    set -Ux CAIRO_ROOT $HOME/.cairo
    fish_add_path $CAIRO_ROOT/target/release
    ~~~

    Otherwise, execute the snippet below:

    ~~~ fish
    set -Ux CAIRO_ROOT $HOME/.cairo
    set -U fish_user_paths $CAIRO_ROOT/target/release $fish_user_paths
    ~~~

   In MacOS, you might also want to install [Fig](https://fig.io/) which
provides alternative shell completions for many command line tools with an
IDE-like popup interface in the terminal window.
(Note that their completions are independent from Cairo's codebase
so they might be slightly out of sync for bleeding-edge interface changes.)

### Restart your shell

  for the `PATH` changes to take effect.

  ```sh
  exec "$SHELL"
  ```