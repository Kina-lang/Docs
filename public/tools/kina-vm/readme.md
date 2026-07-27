# Kina Version Manager

## What is it?

Kina Version Manager (kina-vm) is a small tool used for managing and installing different versions of the kina cli, compiler and toolchain.

## Installation

Kina-vm is distributed as a small cli via npm and is installed globally.

### Prerequisites

You need to have NodeJS and npm installed.

### Linux

You can install the kina-vm package using our one-line command:

```sh
curl -o- https://raw.githubusercontent.com/Kina-lang/VersionManager/refs/heads/main/install.sh | bash
```

Or you can install it manually using npm:

```sh
npm install -g @kina-lang/vm@$kvm_version
# Don't forget to add this into your shells rc file: export PATH="$HOME/.local/share/kina/bin:$PATH"
```

### Windows

Currently unsupported

### MacOS

Currently unsupported

## Usage

After successfuly installing the kina-vm, you can use it by executing the `kina-vm` command.

### Listing available versions

```sh
kina-vm list
```

### Getting the latest version tag

```sh
kina-vm list --latest
```

### Installing version

```sh
kina-vm install <version>
```

For example:

```sh
kina-vm install 0.1.1
```

### Setting currently used version

```sh
kina-vm use <version>
```

For example:

```sh
kina-vm use 0.1.1
```

## Also see

- [How it works](./how-it-works.md)
