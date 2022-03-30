# Building your own Docker static package

Static packages can be built from this directory with the following syntax

```console
make TARGETPLATFORM=${TARGETOS}/${TARGETARCH}/${TARGETVARIANT} build
```

Format of `TARGETOS`, `TARGETARCH`, `TARGETVARIANT` is the same as the [platform ARGs in the global scope](https://docs.docker.com/engine/reference/builder/#automatic-platform-args-in-the-global-scope)
for a Dockerfile like `linux/arm/v7`.

Artifacts will be located in `build` under the following directory structure:
`build/$os/$arch/$variant/` or `build/$os/$arch/` if there is no variant being
used.

### Building from local source

Specify the location of the source repositories for the engine and cli when
building packages

* `ENGINE_DIR` -> Specifies the directory where the engine code is located, eg: `$GOPATH/src/github.com/docker/docker`
* `CLI_DIR` -> Specifies the directory where the cli code is located, eg: `$GOPATH/src/github.com/docker/cli`

```shell
make ENGINE_DIR=/path/to/engine CLI_DIR=/path/to/cli TARGETPLATFORM=linux/amd64 build
```

## Supported platforms

Here is a list of platforms that are currently supported:

```console
make TARGETPLATFORM=linux/amd64 build
make TARGETPLATFORM=linux/arm/v6 build
make TARGETPLATFORM=linux/arm/v7 build
make TARGETPLATFORM=linux/arm64 build
make TARGETPLATFORM=darwin/amd64 build
make TARGETPLATFORM=darwin/arm64 build
make TARGETPLATFORM=windows/amd64 build
```

> note: `darwin` only packages the docker cli and plugins.

But you can test building against whatever platform you want like:

```console
make TARGETPLATFORM=linux/riscv64 build
make TARGETPLATFORM=linux/s390x build
```
