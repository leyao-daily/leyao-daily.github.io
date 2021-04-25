---
layout: post
title: Build Your Custom OpenWrt Image
categories: OpenWrt
description: A step by step guide to build your own OpenWrt application and integrate it with OpenWrt build system.
excerpt_separator: <!-- excerpt-end -->
keywords: OpenWrt, C/C++, Docker, Sdewan, Guide
---

This guides to build your OpenWrt Image integrated with custom application step by step.
<!-- excerpt-end -->
---

* [Setup OpenWrt](#setup-openwrt)
    * [Pre-requisites](#pre-requisites)
    * [Build OpenWrt form source code](#build-openwrt-form-source-code)
* [Create your own application](#create-your-own-application)
    * [Locate your application](#locate-your-application)
	* [Compile and test](#compile-and-test)
* [Generate the application package](#generate-the-application-package)
    * [Create package and configure it](#create-package-and-configure-it)
	* [Integrate the package to build system](#integrate-the-package-to-build-system)
	* [Updating and installing feeds](#updating-and-installing-feeds)
* [Build image and test](#build-image-and-test)
    * [Build image with custom application](build-image-with-custom-application)
	* [Import image and test](#import-image-and-test)
* [Patch your application](#patch-your-application)
    * [Prepare](#prepare)
    * [Create a simple patch](#create-a-simple-patch)
    * [Include the patch](#include-the-patch)

---

## Setup OpenWrt

### Pre-requisites

#### Debian / Ubuntu

```shell
sudo apt update
sudo apt install build-essential ccache ecj fastjar file g++ gawk \
gettext git java-propose-classpath libelf-dev libncurses5-dev \
libncursesw5-dev libssl-dev python python2.7-dev python3 unzip wget \
python3-distutils python3-setuptools rsync subversion swig time \
xsltproc zlib1g-dev 
```

#### CentOS / Fedora

```shell
sudo dnf --skip-broken install bash-completion bzip2 gcc gcc-c++ git \
make ncurses-devel patch perl-Data-Dumper perl-Thread-Queue python2 \
python3 rsync tar unzip wget perl-base perl-File-Compare \
perl-File-Copy perl-FindBin diffutils which
```

For other Linux distributions, you can take [this](https://openwrt.org/docs/guide-developer/build-system/install-buildsystem#examples_of_package_installations) for reference.

### Build OpenWrt form source code

You need leave the `sudo` privileged mode to get better cross-compile by `ctrl + d` or `exit`.

1. Get the `OpenWrt` source code

   ```shell
   git clone https://git.openwrt.org/openwrt/openwrt.git
   cd openwrt
   ```

2. Build from main branch or stable release branch

   ```shell
   # To build from a specific version
   git branch
   git checkout <branch name>
   # Or just skip to 3 to build from main branch
   ```

3. Update and install feeds

   ```shell
   ./scripts/feeds update -a
   ./scripts/feeds install -a
   ```

4. Configure

   ```shell
   make menuconfig
   ```

   E.g. for target “[TL-WR841N v11](https://openwrt.org/toh/tp-link/tl-wr841n)” Wi-Fi router do following:

   - “Target System” ⇒ “Select” ⇒ “Atheros AR7xxx/AR9xxx” ⇒ “Select”
   - “Subtarget” ⇒ “Select” ⇒ “Devices with small flash” ⇒ “Select”
   - “Target Profile” ⇒ “Select” ⇒ “TP-LINK TL-WR841N/ND v11” ⇒ “Select”

   To exit `OpenWrt` configuration and save target with options settings do following:

   - “Exit” ⇒ “Yes”

5. Tool Chain

   ```shell
   make toolchain/install
   ```

   The target-independent tools and the toolchain are deployed to the `staging_dir/host/` and `staging_dir/toolchain/` directories. This applies to the executables built in the above section as well the pre-built executables available in the SDK. We can adjust the `PATH` variable:

   ```shell
   export PATH=/home/icn/openwrt/staging_dir/host/bin:$PATH
   ```

6. Build image

   ```shell
   make
   # For faster compiling, use `make -j N`, where N is the number of CPU cores + 1.
   ```

   And the target image will be generated into `./bin/target/...`

---

## Create your own application

### Locate your application

Suppose we create a project named `hellosdewan`.

```shell
mkdir hellosdewan
cd hellosdewan
pwd
# /home/icn/hellosdewan
```

We create the sole source code file named `hellosdewan.c`.

```shell
touch hellosdewan.c
```

And input the following content:

```c
#include <stdio.h>
 
int main(void)
{
    printf("\nHello, sdewan!\n\n");
    return 0;
}
```

### Compile and test

Our example application is a `c` application.

```shell
gcc -c -o hellosdewan.o hellosdewan.c -Wall
gcc -o hellosdewan hellosdewan.o
```

And then, run the `hellosdewan` binary 

```shell
./hellosdewan
# Hello, sdewan!
```

---

## Generate the application package

### Create package and configure it

Firstly create a directory to store your own application, like the `openwrt`,

```shell
mkdir -p myapps/test/hellosdewan
cd myapps/test/hellosdewan
pwd
# /home/icn/myapps/test/hellosdewan
```

Then we need deliver a package manifest file for `hellosdwan` application, which is responsible for describing the package, what it does and provide instructions on where to obtain the source code, how to build it and which should be contained in the final installable package.

In current directory, create a `Makefile`:

```makefile
include $(TOPDIR)/rules.mk

# Name, version and release number
# The name and version of your package are used to define the variable to point to the build directory of your package: $(PKG_BUILD_DIR)
PKG_NAME:=hellosdewan
PKG_VERSION:=1.0
PKG_RELEASE:=1

# Source settings (i.e. where to find the source codes)
# This is a custom variable, used below
SOURCE_DIR:=/home/icn/myapps/test/hellosdewan

include $(INCLUDE_DIR)/package.mk

# Package definition; instructs on how and where our package will appear in the overall configuration menu ('make menuconfig')
define Package/hellosdewan
        SECTION:=test
        CATEGORY:=MyApps
        TITLE:=Hello, sdewan!
endef

# Package description; a more verbose description on what our package does
define Package/hellosdewan/description
        A simple "Hello, sdewan!" -application.
endef

# Package preparation instructions; create the build directory and copy the source code.
# The last command is necessary to ensure our preparation instructions remain compatible with the patching system.
define Build/Prepare
        mkdir -p $(PKG_BUILD_DIR)
        cp $(SOURCE_DIR)/* $(PKG_BUILD_DIR)
        $(Build/Patch)
endef

# Package build instructions; invoke the target-specific compiler to first compile the source file, and then to link the file into the final executable
define Build/Compile
        $(TARGET_CC) $(TARGET_CFLAGS) -o $(PKG_BUILD_DIR)/hellosdewan.o -c $(PKG_BUILD_DIR)/hellosdewan.c
        $(TARGET_CC) $(TARGET_LDFLAGS) -o $(PKG_BUILD_DIR)/$1 $(PKG_BUILD_DIR)/hellosdewan.o
endef

# Package install instructions; create a directory inside the package to hold our executable, and then copy the executable we built previously into the folder
define Package/hellosdewan/install
        $(INSTALL_DIR) $(1)/usr/bin
        $(INSTALL_BIN) $(PKG_BUILD_DIR)/hellosdewan $(1)/usr/bin
endef

# This command is always the last, it uses the definitions and variables we give above in order to get the job done
$(eval $(call BuildPackage,hellosdewan))
```

### Integrate the package to build system

`OpenWrt` build system uses a file named `feeds.conf.default` which indicates the package feeds that will be made available during the firmware configuration stage.

```shell
pwd
# /home/icn/openwrt
cat feed.conf.default
`
src-git packages https://git.openwrt.org/feed/packages.git
src-git luci https://git.openwrt.org/project/luci.git
src-git routing https://git.openwrt.org/feed/routing.git
src-git telephony https://git.openwrt.org/feed/telephony.git
#src-git video https://github.com/openwrt/video.git
#src-git targets https://github.com/openwrt/targets.git
#src-git management https://github.com/openwrt-management/packages.git
#src-git oldpackages http://git.openwrt.org/packages.git
#src-link custom /usr/src/openwrt/custom-feed
`
```

Modify the file to link to `myapps` package feed with `vim` or other editor in `feeds.conf.default`:

```shell
src-link myapps /home/icn/myapps
```

#### Updating and installing feeds

The new feed is defined, so update the build system

```shell
pwd
# /home/icn/openwrt
./scripts/feeds update myapps
./scripts/feeds install -a -p myapps
```

---

## Build image and test

### Build image with custom application

Re-configure your `openwrt` build system

```shell
pwd
# /home/icn/openwrt
make menuconfig
```

In the menu list, we could find the category named `MyApps` and enter into this category and choose the application we deployed named `hellosdewan` here. Save the configuration and exit.

The changes will be stored to `.config`, then start to build the image

```shell
make -j 70
# To locate the error, you can run `make -j1 V=sc`
```
### Import image and test

After finishing the image build, we can find the `rootfs` of the image in the `./bin` directory

```shell
pwd
# /home/icn/openwrt
# Dive into the target to find the `rootfs` image
cd ./bin/targets/x86/64
ls openwrt-x86-64-generic-rootfs.tar.gz
```

Import the image to docker as a docker container

```shell
sudo docker import openwrt-x86-64-generic-rootfs.tar.gz myapps:hellosdewan
```

Then the image is imported into docker as `myapps` and tag is `hellosdewan`. We can run the docker image and test the application `hellosdewan`

```shell
sudo docker run -ti myapps:hellosdewan hellosdewan
# Hello, sdewan!
```

Note you can build the `opkg` package solely

```shell
pwd
# /home/icn/openwrt
make package/hellosdewan/compile
# The `hellosdewan_1.0-1_x86_64.ipk` will be on `./bin/packages/x86_64/myapps`
# And you can use `opkg` to directly install it
opkg install <path-to-package>/hellosdewan_1.0-1_x86_64.ipk
# Or you can remove the installation
opkg remove hellosdewan
```

---

## Patch your application

### Prepare

Check the tool for patch is ready

```shell
pwd
# /home/icn/openwrt
quilt --version
# the path of tools like quilt in under `./staging_dir/host/bin/`
```

Prepare the source code and navigate into the build directory.

```shell
make package/hellosdewan/{clean,prepare} QUILT=1
cd build_dir/target-x86_64_musl/hellosdewan-1.0
quilt push -a
```

### Create a simple patch

```shell
quilt new 000-add.patch
# If editing existing files
quilt edit hellosdewan.c
# If adding new fiels
quilt add function.c
quilt add function.h
touch function.c
touch function.h
quilt edit function.c
quilt edit function.h
```

`function.c`

```c++
int add(int a, int b)
{
    return a + b;
}
```

`function.h`

```c++
int add(int, int);
```

And we can review the change and accept changes as content of patch

```shell
quilt diff
quilt refresh
```

### Include the patch

Migrate the patch data into package

```shell
pwd
# /home/icn/openwrt
make package/hellosdewan/update
```

We now can review the package feed folder and see the changes

```shell
ls -la /home/icn/myapps/test/hellosdewan
ls -la /home/icn/hellosdewan
```

`OpenWrt` build system have migrated the patch to the package manifest folder.

Then build and check the new files and changes are present in the build directory

```shell
pwd
# /home/icn/openwrt
make package/hellosdewan/{clean,prepare}
ls -la build_dir/target-x86_64_musl/hellosdewan-1.0
```

