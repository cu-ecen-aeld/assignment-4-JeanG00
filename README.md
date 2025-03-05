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

```bash
# Step 1: Repository Setup
# find Github Classroom Links to create repo
git clone git@github.com:cu-ecen-aeld/assignment-4-JeanG00.git
cd assignment-4-JeanG00
git remote add buildroot-assignments-base  https://github.com/cu-ecen-aeld/buildroot-assignments-base.git
git fetch buildroot-assignments-base
git merge buildroot-assignments-base/master
git submodule update --init --recursive

git submodule add  https://gitlab.com/buildroot.org/buildroot/
cd buildroot && git checkout 2024.02.x && cd ..
git commit -am 'feat: submodule added'
git push -u origin main
# Step 2: edit file & Install buildroot dependencies
# update `finder-test.sh` in repo `assignments-3-and-later-JeanG00`
vim base_external/package/aesd-assignments/aesd-assignments.mk
sudo apt-get install libncurses5-dev openssh-client expect sshpass netcat iputils-ping

# Step 3: This will generate a default buildroot/.config using qemu_aarch64_virt_defconfig
./build.sh

# Step 4: save this configuration to your project specific defconfig file
# `base_external/configs/aesd_qemu_defconfig` vs `buildroot/configs/qemu_aarch64_virt_defconfig`
./save-config.sh

# Setp 5:
cd buildroot
make menuconfig
# select `aesd-assignments` package you added in your buildroot configuration
# use `/` at main menuconfig interface to search 'aesd' conf location

./save-config.sh

# Step 6: build your system (will take hours to complete)
# use `screen` in case of long process run dies
# `BR2_DL_DIR` allows you to specify a package download directory outside your buildroot tree which is not removed with distclean
echo "export BR2_DL_DIR=${HOME}/.dl" >> ~/.bashrc
source ~/.bashrc
./build.sh

# Step 7:
./runqemu.sh

# Step: 8:
./clean.sh

# Step 9:
# select `dropbear` package to support ssh
# Set the default root password to “root” using buildroot menuconfig
cd buildroot && make menuconfig

# single package rebuild
make aesd-assignments-rebuild
make aesd-assignments-reconfigure

# Local builds
make AESD_ASSIGNMENTS_OVERRIDE_SRCDIR=${HOME}/Documents/assignments-3-and-later-JeanG00

# Step 10:
cd ..
./save-config.sh
./build.sh

# Step 11: Verify you can use ssh to login to your host using port 10022 and the root user/password
# Use scp to transfer your /tmp/assignment4-result.txt file from your qemu instance to your assignment-3-and-later repository in an assignments/assignment4 folder.
./runqemu.sh

# in a new termail, verify qemu-system is working
netstat -plntu
# outputs:  tcp        0      0 0.0.0.0:10022           0.0.0.0:*               LISTEN      1129661/qemu-system
ssh -p 10022 root@localhost -vvv

# run `finder-test.sh` to generate `/tmp/assignment4-result.txt`
finder-test.sh

exit

scp -P 10022 root@localhost:/tmp/assignment4-result.txt ~/Documents/assignments-3-and-later-JeanG00/assignments/assignment4/
```


### [assignment-1-instructions](https://www.coursera.org/learn/linux-system-programming-introduction-to-buildroot/supplement/bnixD/assignment-1-instructions)

### [assignment-2-instructions](https://www.coursera.org/learn/linux-system-programming-introduction-to-buildroot/supplement/U1Beh/assignment-2-instructions)

### [assignment-3-part-1-instructions](https://www.coursera.org/learn/linux-system-programming-introduction-to-buildroot/supplement/Nh4LM/assignment-3-part-1-instructions)

### [assignment-3-part-2-instructions](https://www.coursera.org/learn/linux-system-programming-introduction-to-buildroot/supplement/YGf42/assignment-3-part-2-instructions)

### [assignment-4-part-1-instructions](https://www.coursera.org/learn/linux-system-programming-introduction-to-buildroot/supplement/GT0Ld/assignment-4-part-1-instructions)

### [assignment-4-part-2-instructions](https://www.coursera.org/learn/linux-system-programming-introduction-to-buildroot/supplement/fdk6R/assignment-4-part-2-instructions)
