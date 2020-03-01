# python-ide

## Description

Python development environment with Visual Studio Code IDE.

The following software is installed:

- Python 3
- PyLint
- Visual Studio Code with Python extension

## Usage

```bash
docker run --rm -it -v /tmp/.X11-unix:/tmp/.X11-unix \
                    -v /dev/shm:/dev/shm \
                    -v $(pwd):/src \
                    -v python-ide-ext-volume:/extensions \
                    -v python-ide-settings-volume:/home/vscode/.config/Code/User \
                    ${evar} \
                    --cap-add=SYS_PTRACE \
                    --security-opt apparmor=unconfined \
                    --security-opt seccomp=unconfined \
                    vvinch/python-ide:debian
```

The --cap-add and --security-opt options are mandatory for running a debugger inside the container.

### Volumes

- /extensions

  This folder gathers the installed extension files. Can be used to persist the manually installed extensions.

- /tmp/.X11-unix

   This location must be mapped to the Docker host X11 socket. Typically at the same location.

- /src

   This folder is the root path for C++ projects. This should be mapped to an external volume containing the sources in order to backing up the data and the build results.

- /dev/shm

   This specific volume maps shared memory to the host's one.

### Environment

- DISPLAY=:0.0

   This environment variable is defined by default.

- VS_OPTIONS

   Additionnal command line parameters for Visual Studio Code (eg: ```--ignore-certificate-errors```)
