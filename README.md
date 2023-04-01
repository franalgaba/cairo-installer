# Cairo 1.0 installer

This tool installs [Cairo 1.0](https://github.com/starkware-libs/cairo). It is inspired by [pyenv-installer](https://github.com/pyenv/pyenv-installer).

## Prerequisites

[Git](https://git-scm.com/) installed.

[Rust](https://www.rust-lang.org/) installed. You can easilly install it running:

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

## Installation / Update / Uninstallation

Once prerequisites have been installed correctly:

### Install

If you wish to install a specific release of Cairo rather than the latest head, set the CAIRO_GIT_TAG environment variable (e.g. export CAIRO_GIT_TAG=v1.0.0-alpha.6).

```bash 
curl -L https://github.com/franalgaba/cairo-installer/raw/main/bin/cairo-installer | bash
```

After installing, follow these instructions to set up your shell environment.

You can now begin using pyenv.