# Docker

The [docker image](https://hub.docker.com/r/masterofzen/av1an) is frequently updated and includes all supported encoders and all optional components. It is based on Arch Linux and provides recent versions of encoders and libraries.

The image provides three types of tags that you can use:
- `masterofzen/av1an:master` for the latest commit from `master`
- `masterofzen/av1an:sha-#######` for a specific git commit (short hash)

## Examples

The following examples assume the file you want to encode is in your current working directory.

Linux

```bash
docker run --privileged -v "$(pwd):/videos" --user $(id -u):$(id -g) -it --rm masterofzen/av1an:master -i S01E01.mkv {options}
```

Windows

```powershell
docker run --privileged -v "${PWD}:/videos" -it --rm masterofzen/av1an:master -i S01E01.mkv {options}
```

## Building the Docker Images

You can build the Docker images locally instead of pulling them from Docker Hub.

### Linux Image

The standard Docker image for Linux can be built by running the following command in the root directory of this repository:

```sh
docker build -t "av1an-linux" .
```

This will create a Docker image named `av1an-linux` which includes all dependencies.

### macOS Binary (via Cross-compilation)

You can cross-compile a binary for macOS (`x86_64`) using Docker. This is useful if you are on a non-macOS machine.

First, ensure you have Docker and Docker Compose installed. Then, run the following command in the root directory of this repository:

```sh
docker-compose up av1an-macos-builder
```

This process will compile the `av1an` binary and place it in a `bin/` directory on your host machine. Note that this binary is dynamically linked, so the target macOS system will need to have dependencies like FFmpeg and VapourSynth installed.

## Specifying a different directory

To specify a different directory to use you would replace $(pwd) with the directory

```bash
docker run --privileged -v "/c/Users/masterofzen/Videos":/videos --user $(id -u):$(id -g) -it --rm masterofzen/av1an:master -i S01E01.mkv {options}
```

The --user flag is required on linux to avoid permission issues with the docker container not being able to write to the location, if you get permission issues ensure your user has access to the folder that you are using to encode.