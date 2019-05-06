---
layout: docs
title: Configuration
permalink: /docs/config/
doc-order: 5
---

This gives a brief introduction on how to configure penguinTrace for a given environment.
The [options](/docs/options/) page gives more details on all of the available options
and how they can be set. Options can be passed on the command-line in the format 
`-c OPTION VALUE`.

## Compilers

By default, penguinTrace will use the `which` command to find the location of the
compilers on your system, as well as `objcopy` (and `clang` for using libclang).

This can be overriden with the following options:

- `C_COMPILER_BIN`, compiler used for C (`-xc`) and Assembly code (`-xassembler`)
- `CXX_COMPILER_BIN`, compiler used for C++ (`-xc++`) code

> **Note:** C and C++ compilers are specified separately as this is used by GCC
> and clang to determine which standard library to include, for assembly code
> the `-nostdlib` option is passed so that no library is linked.

- `CLANG_BIN`, path to pass to libclang when invoked for syntax checking
- `OBJCOPY_BIN`, path to objcopy to add sections to compiled binaries

> penguinTrace adds two sections to compiled binaries `PENGUINTRACE.SRC` and
> `PENGUINTRACE.CFG`. These are used to recreate a session when a binary is
> uploaded

When running in a sandbox (e.g. when `ISOLATE_TRACEE` is enabled) the
`LIB_DIRS` option is used to specify the directories that should be mounted in
the sandbox to provide shared libraries etc. This is specified as a colon
separated list of directories. By default it is set to `/lib:/lib64:/usr/lib`
as these are defined as the 'trusted' library directories by `ld`.

