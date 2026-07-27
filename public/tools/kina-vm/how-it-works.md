# Kina Version Manager - How it works

In this chapter, you will learn how kina-vm works under the hood.

## Kina-vm installation

The installation does the following:

- Creates a kina folder
  - Linux: `~/.local/share/kina`
- Installs `@kina-lang/vm` using npm globally (which adds kina-vm binary into your PATH)
- Guides you to add kina folder into the PATH

## First kina-vm command usage

After first running the kina-vm command, the following happens:

- Checks if the kina folder exists, creates it otherwise
- Checks if the kina folder/bin/kina file exists
  - This file is the file that you execute via the `kina` command

## Kina version installation

When you install new version of kina:

- kina-vm does several checks (version exists, ...)
- Creates a new folder `kina folder/versions/VERSION`
- Downloads `release.zip` from the github Kina-lang/releases with the correct version tag
- Extracts `release.zip`
- Runs `npm install` to build the node-gyp dependencies
- Creates `kina folder/versions/VERSION/kina` wrapper script
  - This file just correctly executes the kina cli in the same folder

## Kina version `use`

When you "use" a specific version of kina:

- kina-vm does several checks (version is installed, ...)
- Writes the version into `kina folder/active_version`

## When you execute `kina` command

When you execute the kina command:

- Your shell checks the PATH variable
- Your shell checks all the paths in it until finding the `kina folder/bin/kina` wrapper script
- Your shell executes the `bin/kina` wrapper script
- `bin/kina` checks if the `active_version` file exists and reads the version
- `bin/kina` executes the `kina folder/versions/VERSION/kina` wrapper script and forwards the cli args to it
- `versions/VERSION/kina` wrapper scripts calls the CLI and forwards the cli args to it
  - This is version dependent, which is why the wrapper script exists in the first place
  - Currently, it just executes the index.cjs file via node in the cwd and forwards the cli args to it
