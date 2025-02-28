# Overview

This repository contains assignment starter code for buildroot based assignments for the course Advanced Embedded Software Design, ECEN 5713

It also contains instructions related to modifying your buildroot project to use with supported hardware platforms.  See [this wiki page](https://github.com/cu-ecen-5013/buildroot-assignments-base/wiki/Supported-Hardware) for details.

## [build dependencies reference](https://github.com/cu-ecen-aeld/aesd-autotest-docker/blob/master/docker/Dockerfile)

## Installing Dependencies

Run `./install_ubuntu.sh` to install any dependencies.  This should work on Ubuntu or on the
vagrant container referenced on the [Buildroot Manual](https://buildroot.org/downloads/manual/manual.html) startup
page.

## Buildroot documentation, including:

- https://buildroot.org/downloads/manual/manual.html#requirement-mandatory
- https://buildroot.org/downloads/manual/manual.html#customize
- https://buildroot.org/downloads/manual/manual.html#generic-package-tutorial
- [QEMU Documentation and network options](https://qemu.readthedocs.io/en/v9.2.0/system/invocation.html#invocation)

## Building

Run `./build.sh` to build the image.  This script is currently hard-coded to use an x86_64 default
build target config.  The config will only be updated when the .config file does not exist.  When pulling
in configuration changes, delete the buildroot/.config file before running the build script.  This will require
a complete rebuild.

## Starting Qemu

Typically you will want to open a new [screen](https://www.gnu.org/software/screen/). session using `screen -S qemu` or similar before starting
QEMU. Then from this screen session, run `./start_qemu.sh`.
To detach, use Ctrl-a d.
You can reconnect to this screen later using `screen -r qemu`.
When you want to stop the qemu target, use `pkill qemu`

## Saving Configs
When you make changes to buildroot configuration files, run `./save_configs.sh` to export these configurations to
the br2-external tree for commit.

## Assignments Grading Criteria


### [assignment-1-instructions](https://www.coursera.org/learn/linux-system-programming-introduction-to-buildroot/supplement/bnixD/assignment-1-instructions)

### [assignment-2-instructions](https://www.coursera.org/learn/linux-system-programming-introduction-to-buildroot/supplement/U1Beh/assignment-2-instructions)

### [assignment-3-part-1-instructions](https://www.coursera.org/learn/linux-system-programming-introduction-to-buildroot/supplement/Nh4LM/assignment-3-part-1-instructions)

### [assignment-3-part-2-instructions](https://www.coursera.org/learn/linux-system-programming-introduction-to-buildroot/supplement/YGf42/assignment-3-part-2-instructions)

### [assignment-4-part-1-instructions](https://www.coursera.org/learn/linux-system-programming-introduction-to-buildroot/supplement/GT0Ld/assignment-4-part-1-instructions)

### [assignment-4-part-2-instructions](https://www.coursera.org/learn/linux-system-programming-introduction-to-buildroot/supplement/fdk6R/assignment-4-part-2-instructions)
