# Kina CLI

Kina CLI is the main tool that you will interact with. The CLI contains everything, including package manager, compiler, project creator and more. CLI can have different versions that you can switch and manage using the [Kina Version Manager](../kina-vm/readme.md), which is often handy for compatibility reasons.

## Installation

You have a few options on how to install kina (see below). The official way is to install via the kina-vm locally, but it is currently a pretty huge pain on most systems because of [dependency hell](https://en.wikipedia.org/wiki/Dependency_hell). If you don't want to deal with those problems, we recommend sticking to the docker approach for now. We will work hard to make the official way much more simple, intuitive and viable.

### Kina-vm (Official way)

#### Prerequisites

- LLVM 22 + devel/lib
- NodeJS 22 + node-gyp dependencies
- Clang, Gcc + gcc-c++, cmake + make, zlib, libxml devel

#### Steps

1. Install kina-vm: [See this](../kina-vm/readme.md#installation)
2. Check the latest version:

```sh
kina-vm list --latest
```

3. Install the latest version (replace VERSION with the version from step 2)

```sh
kina-vm install VERSION
```

4. Activate the latest version (replace VERSION with the version from step 2)

```sh
kina-vm use VERSION
```

### Docker image

We provide the `ghcr.io/kina-lang/kina:VERSION` docker image, which contains the kina toolchain and all of it's dependencies preinstalled according to the official way. This has a range of uses, including multistage docker files for your projects or just as a way to use the kina toolchain without needing to install all of the dependencies.

#### Usage as a CLI

You can use the kina CLI via docker. Don't forget to replace VERSION with your desired kina version ([this is the latest one](https://github.com/Kina-lang/Release/releases/latest)).

```sh
docker run --rm -it --workdir /app -v `pwd`:/app ghcr.io/kina-lang/kina:VERSION kina <subcommand>
```

This mounts your current working directory into the docker image, don't forget that the path and filesystem is different from your local one.

#### Usage in multi-stage docker files

[See this](../guides/docker/multistage.md)

## Usage

### Creating a new project

You can create a new project using the following command:

```sh
kina create <name>
```

This will create a new directory inside of your current working one with the same name as the project. This will also create a new [kina.toml](../../language/project/kina-toml.md) file, the `Hello World` example file in `src/main.kin` and it will also use kina package manager to install our stdlib.

### Running a project

You can compile and run your current project using the command below. Be aware that this command is required to be run inside the same directory in which your [kina.toml](../../language/project/kina-toml.md) file is.

```sh
kina run [target]
```

The `target` parameter is optional, default will be used if no target is provided. Learn more [here](../../language/project/targets.md).

This will essentialy [compile](#compile-a-project) the project and it will then spawn the built binary as a new process and pipe it's stdio to the CLIs stdio.

### Hot reload

NOTE: This is not supported on some [targets](../../language/project/targets.md) due to it's architectural/toolchain/distribution limitations (reflashing ESP32 on each file change would probably not be a really fun thing to do)!

Kina also supports hot reload, thanks to its pretty fast compilation. The command watches you project directory and recompiles and restarts your program every time a file changes. Be aware that this command is required to be run inside the same directory in which your [kina.toml](../../language/project/kina-toml.md) file is.

```sh
kina watch [target]
```

The `target` parameter is optional, default will be used if no target is provided. Learn more [here](../../language/project/targets.md).

This will essentialy do the same things as [running your project](#running-a-project), with the difference that it restarts the run every time that your project files change.

### Compile a project

This will compile your project into an executable binary file. Be aware that this command is required to be run inside the same directory in which your [kina.toml](../../language/project/kina-toml.md) file is.

```sh
kina compile [target]
```

The `target` parameter is optional, default will be used if no target is provided. Learn more [here](../../language/project/targets.md).

The built binary will be located in `PROJECT DIRECTORY/build/PROJECT NAME/PROJECT VERSION/BUILD TARGET/output(.exe/...)`.

### Package manager

[See this](./pm.md)
