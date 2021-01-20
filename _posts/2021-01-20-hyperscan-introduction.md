---
layout: post
title: HyperScan brief intro and samples
categories: SIMD
description: A brief introduction of HyperScan which is based on Intel SIMD and accelerated the regex matching.
keywords: Intel, C++, Regex-Matching, SIMD, Guide
---

# HyperScan

## Dependences

### Hardware

Hyperscan will run on x86 processors in 64-bit (Intel® 64 Architecture) and 32-bit (IA-32 Architecture) modes.

Hyperscan is a high performance software library that takes advantage of recent Intel architecture advances. At a minimum, support for Supplemental Streaming SIMD Extensions 3 (SSSE3) is required, which should be available on any modern x86 processor.

Additionally, Hyperscan can make use of:

> - Intel Streaming SIMD Extensions 4.2 (SSE4.2)
> - the POPCNT instruction
> - Bit Manipulation Instructions (BMI, BMI2)
> - Intel Advanced Vector Extensions 2 (Intel AVX2)

### Software

I am working on a ubuntu-18.04 server, and we need pre-install some dependency lib. I execute the following installation in root mode:

```shell
#Firstly we should install libpcre, and the required version>=8.44
#Install the pre-dependency lib
apt update
apt install build-essential cmake
apt install checkinstall automake libbz2-1.0 libbz2-dev libbz2-ocaml libbz2-ocaml-dev
apt install libreadline-dev

#Download the source from https://ftp.pcre.org/pub/pcre/, we choose 8.44 version here
wget https://ftp.pcre.org/pub/pcre/pcre-8.44.tar.gz
tar zxvf pcre-8.44.tar.gz
cd pcre-8.44

#Configure and complie the so, and install pcre lib
./configure --prefix=/usr \
  --docdir=/usr/share/doc/pcre-8.44 \
  --enable-utf \
  --enable-unicode-properties \
  --enable-pcre16 \
  --enable-pcre32 \
  --enable-pcregrep-libz \
  --enable-pcregrep-libbz2 \
  --enable-pcretest-libreadline \
  --disable-static
make
make check
make install
mv -v /usr/lib/libpcre.so.* /lib 
ln -sfv ../../lib/$(readlink /usr/lib/libpcre.so) /usr/lib/libpcre.so

#To have a full-featured HyperScan, we need pre-install the following libs
apt update
apt install -y libboost-all-dev ragel libpcap-dev doxygen sphinx-common libsqlite3-dev
```

## Quick Start

- Clone the source code

  ```shell
  git clone https://github.com/intel/hyperscan.git
  ```

- Configure the HyperScan features

  ```shell
  cd hyperscan
  mkdir build
  cd build
  #My server support the Intel AVX512 SIMD, but it is disabled defaultly
  cmake -DBUILD_AVX512=on ..
  ```

- Build and install HyperScan

  ```shell
  cmake --build .
  #Of course you can use makefiles in parallel by `make -j`
  ```

- Check the installation with unit tests

  ```shell
  bin/unit-hyperscan
  ```

- 



