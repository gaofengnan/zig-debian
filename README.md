![GitHub Downloads (all assets, all releases)](https://img.shields.io/github/downloads/gaofengnan/zig-debian/total)
![GitHub Downloads (all assets, latest release)](https://img.shields.io/github/downloads/gaofengnan/zig-debian/latest/total)
![GitHub Release](https://img.shields.io/github/v/release/gaofengnan/zig-debian)
![GitHub Release Date](https://img.shields.io/github/release-date/gaofengnan/zig-debian)

<h1>
   <p align="center">
     <a href="https://github.com/ziglang/zig/"><img src="https://github.com/gaofengnan/zig-debian/blob/main/zig-logo.png" alt="Zig Logo" width="128" style="margin-right: 20px"></a>
     <a href="https://www.debian.org/"><img src="https://github.com/gaofengnan/zig-debian/blob/main/debian-logo.png" alt="Debian Logo" width="104" style="margin-left: 20px"></a>
     <br>Zig for Debian
   </p>
</h1>
<p align="center">
 👻 Zig is a general-purpose programming language and toolchain for maintaining robust, optimal, and reusable software.
</p>

## Package Changes

The repository is powered by [reprepro](https://salsa.debian.org/brlink/reprepro), which is
configured to keep only the **latest version** of each package. This means older builds are
automatically replaced when a new release is published — you cannot `apt install zig=0.15.2`
after 0.16.0 has shipped.

To let users keep a previous release installed alongside the current one, the packages are named
by stability tier rather than by version number:

The package structure has been updated to track Zig releases more clearly:

| Package | Description | Installs |
|---|---|---|
| `zig` | Meta-package, always points to the current stable release | `zig-stable` |
| `zig-stable` | Current stable release (e.g. 0.16.0) | `/usr/lib/zig/<version>/zig` |
| `zig-oldstable` | Previous stable release (e.g. 0.15.2) | `/usr/lib/zig/<version>/zig` |
| `zig-0` | **Deprecated.** Install `zig-stable` instead. | — |

`zig-stable` and `zig-oldstable` can be installed **side by side**. When both are present,
`/usr/bin/zig` defaults to the stable version. Use `update-alternatives` to switch:

```sh
sudo update-alternatives --config zig
```

As new Zig releases ship, `zig-stable` advances to the new version and the previous stable
becomes `zig-oldstable`. Installing `zig` (the meta-package) always keeps you on the current
stable.

# Zig for Debian

> Fork of [dariogriffo/zig-debian](https://github.com/dariogriffo/zig-debian) (MIT); the original packaging is by Dario Griffo. Served at [deb.gaofn.xyz](https://deb.gaofn.xyz) for Debian 12 (bookworm) and 13 (trixie).

This repository contains build scripts to produce the _unofficial_ Debian packages
(.deb) for [Zig](https://github.com/ziglang/zig) hosted at [deb.gaofn.xyz](https://deb.gaofn.xyz)

Currently supported debian distros are:
- Bookworm
- Trixie
- Sid

This is an unofficial community project to provide a package that's easy to
install on Debian. If you're looking for the Zig source code, see
[ziglang/zig](https://github.com/ziglang/zig).

## Install/Update

### The Debian way

```sh
sudo install -d -m 0755 /etc/apt/keyrings
sudo curl -fsSL https://deb.gaofn.xyz/deb.gaofn.xyz.gpg -o /etc/apt/keyrings/deb.gaofn.xyz.gpg
sudo curl -fsSL https://deb.gaofn.xyz/deb.gaofn.xyz.sources -o /etc/apt/sources.list.d/deb.gaofn.xyz.sources
# Debian 12 (bookworm): fetch deb.gaofn.xyz-bookworm.sources instead
sudo apt update
sudo apt install zig           # current stable
sudo apt install zig-oldstable # previous stable (optional, installs alongside zig-stable)
```

### Manual Installation

1. Download the .deb package for your Debian version available on
   the [Releases](https://github.com/gaofengnan/zig-debian/releases) page.
2. Install the downloaded .deb package.

```sh
sudo dpkg -i <filename>.deb
```
## Updating

To update to a new version, just follow any of the installation methods above. There's no need to uninstall the old version; it will be updated correctly.

## Contributing

I want to have an easy-to-install Zig package for Debian, so I'm doing what
I can to make it happen.
If you want to test locally, you should be able to run
[build_zig_debian.sh](https://github.com/gaofengnan/zig-debian/blob/main/build_zig_debian.sh)
on your own Debian system, only requirement is docker.

## Roadmap

- [x] Produce a .deb package on GitHub Releases
- [x] Set up a debian mirror for easier updates

## Disclaimer

- This repo is not open for issues related to zig. This repo is only for _unofficial_ Debian packaging.
- This repository is based on the amazing work of [Mike Kasberg](https://github.com/mkasberg) and his [Zig Ubuntu](https://github.com/mkasberg/ghostty-ubuntu) packages
