# Tiny Rust libc

## Introduction

This is a _tiny_ libc implementation, mostly (but not entirely) written in the Rust programming language. It is useful for bare-metal embedded Rust applications that need a C library (maybe because of some third-party library written in C they want to use) but don't want to link against a full [newlib](https://sourceware.org/newlib), or who tried but had trouble with both newlib and [compiler_builtins](https://github.com/rust-lang-nursery/compiler-builtins) defining symbols like `memset`.

This crate basically came about so that the [nrfxlib](https://github.com/NordicPlayground/nrfxlib) binary interface library for the nRF9160 would work with Rust.

## Usage

You need to add a use statement to your code: 

```rust
use use tinyrlibc as _;
```

If you get linker errors regarding a missing `string.h` header file, you need to include the headers of the `arm-none-eabi` toolchain. [Download the toolchain](https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads) and add an environment variable to `.cargo/config.toml` in you project folder which contains the absolute path to the header files. For example:

```toml
[env]
C_INCLUDE_PATH = "/Applications/ArmGNUToolchain/13.3.rel1/arm-none-eabi/arm-none-eabi/include"
```

## Implemented so far

* abs
* strol
* atoi
* isspace
* isdigit
* isalpha
* isupper
* memchr
* strcmp
* strncmp
* strncasecmp
* strcat
* strcpy
* strncpy
* strlen
* strtol
* strtoll
* strtoul
* strtoull
* strtoimax
* strtoumax
* strstr
* strchr
* strrchr
* snprintf
* vsnprintf
* qsort
* rand
* alloc (optional)
    * malloc
    * calloc
    * realloc
    * free
* signal (optional)
    * signal
    * raise
    * abort

## Non-standard helper functions

* itoa
* utoa
* rand_r

## To Do

* Anything else nrfxlib needs
* Anything anyone is prepared to submit

## Licence

As this is going to be a bunch of bits taken from all over the place (some newlib, some relibc, etc), each function has its own file and each file has its own licence. Any new licences should be appended to the [LICENCE.md](./LICENCE.md) file.

