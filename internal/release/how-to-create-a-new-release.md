# How to create a new release

## Step 1: Edit, commit, push or pull

You need to ensure that your local repo and all of the submodules are on the version that you want to release

## Step 2: Release libraries

You need to ensure that the [Libraries](https://github.com/Kina-lang/Libraries) has a release with the same tag as your released kina version.

## Step 3: Build runtime

You need to build the runtime

```
# /repos/runtime
$ ./compile
```

## Step 4: Build kina

You need to build the release files

```
# /
$ ./build.cjs {VERSION}
```

## Step 5: Create new release

You need to write the release version into the release repository.

```
# repos/release
$ ./scripts/new-release.cjs {VERSION}
```

You then need to commit the new changes and create a new tag in the [release github repository](https://github.com/Kina-lang/Release) with the attached `release.zip` (DO NOT RENAME) file that was created in your local repo root folder.

## Step 6: Build docker images

You need to update the docker images to use the new version.

- Update version in `repos/docker/compiler/Dockerfile`
- Update version in `repos/docker/build-compiler`

```
# repos/docker
$ ./build-compiler
```

You then need to push to ghcr using the command given to you by the command execution above.

## Step 7: Tag the root repo

First, ensure that you have pushed everything, including the changes you made during the release process and that the submodule refs are updated!
