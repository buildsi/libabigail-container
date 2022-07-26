# Libabigail Container

This is a simple repository to provide an automated build for a libabigail
container. You can update the version via a pull request and changing [VERSION](VERSION).

## Build

If you want to build locally:

```bash
$ docker build --build-arg LIBRARY_VERSION=2.0 -t ghcr.io/buildsi/libabigail:2.0 .
```
