---
layout: docs
title: Programs
permalink: /docs/programs/
doc-order: 10
---

As well as the main executable, penguinTrace also provides some other helper
programs for testing. Passing `-h/--help` to the programs will show usage and
full options.

## `penguintrace`

This is the main executable of penguinTrace. It starts the webserver and
handles creating, running and controlling debugging sessions.

## `dwarf-info`

This parses the debugging information in a binary and prints it to stdout.

## `compile`

This compiles a binary in the same way as code in the web interface. This
produces a binary that can be uploaded in the web interface by including
source code information. The language to use is determined by the extension
of the input file.

| **Extension**  | **Language** |
|   .asm, .s     |   Assembly   |
|   .c           |   C          |
|   .cpp, .cxx   |   C++        |

## `step-elf`

This runs a binary on the command line, stepping each instruction. By default
it will continue stepping automatically until the end of the program. If the
`AUTO_STEP` option is set to false, it will only advance after pressing Enter.

## `run-elf`

This is similar to `step-elf` but continues until hitting a breakpoint. This
can be useful to 'skip' to a particular point in a program. A breakpoint can
be added with an `int3` instruction in an assembly program, or using inline
assembly in a C/C++ program:

```c
   __asm("int3");
```

In AArch64, a breakpoint is provided by the `bkpt` instruction in place of
`int3`.

> Note: currently `run-elf` doesn't have any functionality to convert the
> breakpoint into a `nop` and continue execution.

## `session-id-gen`

This generates session IDs in the same way as the user interface. It is called
with a single integer argument which is the number of IDs to generate.
