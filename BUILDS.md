# Building ProtonMail Bridge and Import-Export app

## Prerequisites
* Go 1.13
* Bash with basic build utils: make, gcc, sed, find, grep, ...
* For Windows it is recommended to use MinGW 64bit shell from [MSYS2](https://www.msys2.org/)
* GCC (linux, windows) or Xcode (macOS)
* Windres (windows)
* libglvnd and libsecret development files (linux)

To enable the sending of crash reports using Sentry please set the
`main.DSNSentry` value with the client key of your sentry project before build.
Otherwise, the sending of crash reports will be disabled.

## Build
In order to build Bridge or Import-Export app with Qt interface we are using
[Qt Go Binding](https://github.com/therecipe/qt).  The dependencies and
installation of this tool is part of `make build` target.  If you have issues
with installation of therecipe/qt we recommend to follow [this
wiki](https://github.com/therecipe/qt/wiki/Installation-on-Linux)

Please note that `$(go env GOPATH)/bin` must be in your `PATH` to ensure
binaries installed by `therecipe/qt` (such as `qtdeploy`) are found. Also,
before you start build **on Windows**, please unset the `MSYSTEM` variable


```bash
export MSYSTEM=
```

### Build Bridge
* in project root run

```bash
make build
```

* The result will be stored in `./cmd/Destop-Bridge/deploy/${GOOS}/`
    * for `linux`, the binary will have the name of the project directory (e.g `proton-bridge`)
    * for `windows`, the binary will have the file extension `.exe` (e.g `proton-bridge.exe`)
    * for `darwin`, the application will be created with name of the project directory (e.g `proton-bridge.app`)

### Build Import-Export
* in project root run

```bash
make build-ie
```

* The result will be stored in `./cmd/Import-Export/deploy/${GOOS}/`
    * for `linux`, the binary will have the name of the project directory (e.g `proton-bridge`)
    * for `windows`, the binary will have the file extension `.exe` (e.g `proton-bridge.exe`)
    * for `darwin`, the application will be created with name of the project directory (e.g `proton-bridge.app`)

### Tags
Note that repository contains both Bridge and Import-Export apps and they are
not released together. Therefore, each app has own tag prefix. Bridge tags
starts with `br-` and Import-Export tags starts with `ie-`. Both tags continue
with semantic versioning `MAJOR.MINOR.PATCH`. An example of full tag is
`br-1.4.4` or `ie-1.1.2` (current versions in October 2020).

## Useful tests, lints and checks
In order to be able to run following commands please install the development dependencies: 
`make install-dev-dependencies`

* `make test` will run all unit tests
* `make lint` will lint the whole project
* `make -C ./test test` will run the integration tests
* `make run` will build Bridge without a GUI and start it in CLI mode
