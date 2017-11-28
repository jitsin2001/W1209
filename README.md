# W1209 Data-Logging Thermostat

[![Travis-CI](https://travis-ci.org/TG9541/W1209.svg?branch=master)](https://travis-ci.org/TG9541/W1209)

This project uses [STM8EF](https://github.com/TG9541/stm8ef) to turn an off-the-shelf [W1209][] into a data logging thermostat. It provides [source code](https://github.com/TG9541/W1209), a ready-to-use [firmware](https://github.com/TG9541/W1209/releases), and [documentation](https://github.com/TG9541/W1209/wiki).

Features are:

* heating thermostat, e.g. for building a chicken egg incubator
* basic sensor failure detection
* parameters for set-point, hysteresis, and trip-delay
* easy to use parameters menu (no need to search for a manual!)
* temperature logger with 0.1h to 10h intervall, and a 288 entry ring-buffer
* logger access throug a serial console
* fully programmable in Forth, even while it's running!

Although it's feature-complete, this is work in progress:

* Beta-grade "bleeding edge"
* not even an "endurance run" yet

Planned features:

* Improved logger with min/max temperature, and heating duty cycle
* Field-bus feature for thermostats
* more fail-safe features (parameter integrity, maybe a buzzer)

Please check out the [HACKADAY.IO project][HAD1]!

## Getting Started

The GitHub releases page contains a

## Building the Source code

The Makefile provides a dependency resolution feature that downloads an STM8 eForth binary release, and adds the required folders, files, and symlinks to the base folder.

For [programming the W1209 binary](https://github.com/TG9541/W1209/blob/master/out/W1209-FD/W1209-FD.ihx) please follow the instructions in the [STM8EF Wiki page for board W1209](
https://github.com/TG9541/stm8ef/wiki/Board-W1209#flashing-the-stm8ef-binary), or just type `make flash`.

Interactive scripting through the serial console is supported once the base STM8 eForth system has been flashed to the board. Please refer to the [instructions for getting a serial console](https://github.com/TG9541/stm8ef/wiki/Board-W1209#serial-communication-through-the-key-pins).

The recommended terminal emulator is [e4thcom](https://wiki.forth-ev.de/doku.php/en:projects:e4thcom): it supports line editing, and upload of source files with `#include`, and using a library with `#require`. Just type `#i main.fs` to load the complete source code!

For Continuous Integration, `make simload` uses ucSim to create an STM8 binary file that contains the full thermostat script, including the W1209-FD base image. The Docker image [tg9541/docker-sdcc](https://hub.docker.com/r/tg9541/docker-sdcc/) contains tool dependencies for Continuous Integration (refer to `.travis.yml`).

## Using this repository

* clone the repository
* install [stm8flash](https://github.com/vdudouyt/stm8flash)
* [connect a ST-LINK-V2 dongle to a W1209][W1209]
* run `make defaults` to wipe the stock firmware
  * warning: there is no known public source for the stock firmware, and after erasing it there is no way back!
* run `make` to flash the STM8EF binary
* for interactive scripting install [e4thcom](
https://wiki.forth-ev.de/doku.php/en:projects:e4thcom)
* optionally install the development version of ucSim (or use the Docker image) to take advantage of off-line image creation

## About the STM8EF Base System

The code is based on the [STM8EF binary release](https://github.com/TG9541/stm8ef/releases). The Makefile automatically retrieves, and resolves the version specified by `STM8EF_VER`.

Please refer to the [STM8EF Wiki](https://github.com/TG9541/stm8ef/wiki) for more information.

## Contributing

File an issue, post a comment in the [HACKADAY.IO project][HAD1], or contribute docs, code, or new use-cases and requirements.

And above all: please write about it in forums, blogs, or on Twitter (please use #W1209 and #STM8EF hashtags).

[HAD1]: https://hackaday.io/project/26258-w1209-data-logging-thermostat
[W1209]: https://github.com/TG9541/stm8ef/wiki/Board-W1209
