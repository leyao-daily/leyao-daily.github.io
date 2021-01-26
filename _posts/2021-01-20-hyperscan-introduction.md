---
layout: post
title: HyperScan brief intro and deployment
categories: SIMD
description: A brief introduction of HyperScan which is based on Intel SIMD and accelerated the regex matching.
keywords: Intel, C++, Regex-Matching, SIMD, Guide
---

# HyperScan

## Introduction

HyperScan is a software regular expression matching engine designed with high performance and flexibility in mind. It is implemented as a library that exposes a straightforward C API.

HyperScan is composed of two components:

### Compilation

These functions take a group of regular expressions, along with identifiers and option flags, and compile them into an immutable database that can be used by the HyperScan scanning API. This compilation process performs considerable analysis and optimization work in order to build a database that will match the given expressions efficiently.

Compiled databases can be serialized and relocated, so that they can be stored to disk or moved between hosts. They can also be targeted to particular platform features (the use of Intel® Advanced Vector Extensions (Intel® AVX2/AVX512) instructions).

### Scanning

Once a HyperScan database has been created, it can be used to scan data in memory. HyperScan provides several scanning modes, depending on whether the data to be scanned is available as a single contiguous block, whether it is distributed amongst several blocks in memory at the same time, or whether it is to be scanned as a sequence of blocks in a stream.

Matches are delivered to the application via a user-supplied callback function that is called synchronously for each match.

## Dependences

### Hardware

HyperScan will run on x86 processors in 64-bit (Intel® 64 Architecture) and 32-bit (IA-32 Architecture) modes.

HyperScan is a high performance software library that takes advantage of recent Intel architecture advances. At a minimum, support for Supplemental Streaming SIMD Extensions 3 (SSSE3) is required, which should be available on any modern x86 processor.

Additionally, HyperScan can make use of:

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
  git clone https://github.com/intel/HyperScan.git
  ```

- Configure the HyperScan features

  ```shell
  cd HyperScan
  mkdir build
  cd build
  #My server support the Intel AVX512 SIMD, but it is disabled defaultly
  cmake -DBUILD_AVX512=on ..
  ```

- Build and install HyperScan

  ```shell
  cmake --build .
  #Of course you can use makefiles in parallel by `make -j`
  make install
  ```

- Check the installation with unit tests

  ```shell
  bin/unit-HyperScan
  ```

- Testing

  After building, we can see the auto-compiled binary program in `hyperscan/build/bin`, the programs `simplegrep`, `pcapscan` and `patbench` are the target file for the source code in `hyperscan/examples`, and you can run them to do some testing.

  If you want to build the examples separately, there may be a brief guide in each source code, but for `simplegrep.c`, we need do following changes:

  ```shell
  diff --git a/examples/simplegrep.c b/examples/simplegrep.c
  index d6bd4b3..2b5fe94 100644
  --- a/examples/simplegrep.c
  +++ b/examples/simplegrep.c
  @@ -116,7 +116,7 @@ static char *readInputData(const char *inputFN, unsigned int *length) {
           return NULL;
       }
  
  -    char *inputData = malloc(dataLen);
  +    char *inputData = (char *)malloc(dataLen);
       if (!inputData) {
           fprintf(stderr, "ERROR: unable to malloc %ld bytes\n", dataLen);
           fclose(f);
  ```

   and compile with:

  ```shell
  g++ -o simplegrep simplegrep.c $(pkg-config --cflags --libs libhs)
  ```

  then you can test it, eg:

  ```shell
  root@ubuntu:~/hyperscan/examples# ./simplegrep malloc simplegrep.c
  Scanning 8041 bytes with Hyperscan
  Match for pattern "malloc" at offset 4471
  Match for pattern "malloc" at offset 4552
  ```

  ## Constructs support from PCRE Library

  ### Supported Constructs

  The following regex constructs are supported by Hyperscan:

  - Literal characters and strings, with all libpcre quoting and character escapes.

  - Character classes such as `.` (dot), `[abc]`, and `[^abc]`, as well as the predefined character classes `\s`, `\d`, `\w`, `\v`, and `\h` and their negated counterparts (`\S`, `\D`, `\W`, `\V`, and `\H`).

  - The POSIX named character classes `[[:xxx:]]` and negated named character classes `[[:^xxx:]]`.

  - Unicode character properties, such as `\p{L}`, `\P{Sc}`, `\p{Greek}`.

  - Quantifiers:

    - Quantifiers such as `?`, `*` and `+` are supported when applied to arbitrary supported sub-expressions.
    - Bounded repeat qualifiers such as `{n}`, `{m,n}`, `{n,}` are supported with limitations.
      - For arbitrary repeated sub-patterns: *n* and *m* should be either small or infinite, e.g. `(a|b){4}`, `(ab?c?d){4,10}` or `(ab(cd)*){6,}`.
      - For single-character width sub-patterns such as `[^\a]` or `.` or `x`, nearly all repeat counts are supported, except where repeats are extremely large (maximum bound greater than 32767). Stream states may be very large for large bounded repeats, e.g. `a.{2000}b`. Note: such sub-patterns may be considerably cheaper if at the beginning or end of patterns and especially if the [`HS_FLAG_SINGLEMATCH`](http://intel.github.io/hyperscan/dev-reference/api_constants.html#c.HS_FLAG_SINGLEMATCH) flag is on for that pattern.
    - Lazy modifiers (`?` appended to another quantifier, e.g. `\w+?`) are supported but ignored (as Hyperscan reports all matches).

  - Parenthesization, including the named and unnamed capturing and non-capturing forms. However, capturing is ignored.

  - Alternation with the `|` symbol, as in `foo|bar`.

  - The anchors `^`, `$`, `\A`, `\Z` and `\z`.

  - Option modifiers:

    These allow behaviour to be switched on (with `(?<option>)`) and off (with `(?-<option>)`) for a sub-pattern. The supported options are:

    > - `i`: Case-insensitive matching, as per [`HS_FLAG_CASELESS`](http://intel.github.io/hyperscan/dev-reference/api_constants.html#c.HS_FLAG_CASELESS).
    > - `m`: Multi-line matching, as per [`HS_FLAG_MULTILINE`](http://intel.github.io/hyperscan/dev-reference/api_constants.html#c.HS_FLAG_MULTILINE).
    > - `s`: Interpret `.` as “any character”, as per [`HS_FLAG_DOTALL`](http://intel.github.io/hyperscan/dev-reference/api_constants.html#c.HS_FLAG_DOTALL).
    > - `x`: Extended syntax, which will ignore most whitespace in the pattern for compatibility with libpcre’s `PCRE_EXTENDED` option.

    For example, the expression `foo(?i)bar(?-i)baz` will switch on case-insensitive matching *only* for the `bar` portion of the match.

  - The `\b` and `\B` zero-width assertions (word boundary and ‘not word boundary’, respectively).

  - Comments in `(?# comment)` syntax.

  - The `(*UTF8)` and `(*UCP)` control verbs at the beginning of a pattern, used to enable UTF-8 and UCP mode.

  ### Unsupported Constructs

  The following regex constructs are not supported by Hyperscan:

  - Backreferences and capturing sub-expressions.
  - Arbitrary zero-width assertions.
  - Subroutine references and recursive patterns.
  - Conditional patterns.
  - Backtracking control verbs.
  - The `\C` “single-byte” directive (which breaks UTF-8 sequences).
  - The `\R` newline match.
  - The `\K` start of match reset directive.
  - Callouts and embedded code.
  - Atomic grouping and possessive quantifiers.