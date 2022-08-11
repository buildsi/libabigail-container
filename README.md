# Libabigail Container

This is a simple repository to provide an automated build for a libabigail
container. You can update the version via a pull request and changing [VERSION](VERSION).

## Build

If you want to build locally (for an example)

```bash
$ docker build --build-arg ubuntu_version=22.04 --build-arg LIBRARY_VERSION=2.0 -f docker/ubuntu/Dockerfile -t ghcr.io/buildsi/libabigail-ubuntu:ubuntu-22.04 .
```
