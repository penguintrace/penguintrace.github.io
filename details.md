---
layout: page
title: More Details
permalink: /details/
order: 40
---

This page provides some technical details of how penguinTrace is constructed.
The main intention of penguinTrace is helping to provide a way to better
understand how programs run at a low level. The development was also used as
an opportunity to better understand details of how programs run, interactions
with the Linux kernel and how debuggers work.

#### Web Interface

**Server**

penguinTrace starts a thread to listen to requests. When a request is received
the path is looked up in a table of routes which returns an object to construct
the response. Broadly there are three types of endpoints:

- File requests, returning a static file
- Commands, which enqueue the command requested
- State requests, which return the current program state

Commands and state requests are split so that requests for a command that could
take some time, e.g. compilation, do not block before returning a response.

**Client**

The Web UI is written with [jQuery][jquery] and [CodeMirror][codemirror]. Each
action makes a command request, which responds immediately whether the command
was successfully enqueued. If successful, the UI will make state requests until
all commands are complete and the UI can be updated with the new state.

#### Compiling

penguinTrace can use [Clang][clang] or [GCC][gcc] to compile programs. If using
Clang (and `libclang`) then a preliminary parsing stage occurs. This provides a
way to get information about compile errors and warning programatically in
order to show them more clearly in the UI.

Then the compiler binary is called directly with the provided source code. Once
the binary is compiled, the source code and configuration are added into new
sections in the binary to create a self-contained binary that can be used to
recreate the same session.

#### Tracing

penguinTrace creates another process using `fork`, and then executes the binary
that has been compiled. penguinTrace uses the [`ptrace`][ptrace] system call in
order to interact with the child process that has been created.

The Linux kernel (and the processor that it is running on) have the ability to
'single step' through instructions, and once the instruction has been stepped
the process is paused until the next step is requested. This is the mode in
which penguinTrace usually controls the child process.

The `ptrace` system call also allows the parent process (in this case
penguinTrace) to read both the registers and the memory of the traced process.
This is used to obtain the values of variables while executing.

#### Debug Information

When compiling, penguinTrace instructs the compiler to embed debugging
information (using the `-g` flag). This contains information such as:

- Mapping between addresses and line numbers
- Locations of variables in memory

This information is stored in [DWARF][dwarf] format, and this information is
parsed from the compiled binary. After each step the program counter/
instruction pointer is used to determine the current function.

By using the current function, the debug information can also be used to
determine the variables in the current scope and their location. Then `ptrace`
can be used to extract the value from the child process.

[jquery]: https://jquery.com/
[codemirror]: https://codemirror.net/
[gcc]: https://www.gnu.org/software/gcc/
[clang]: https://clang.llvm.org/
[ptrace]: https://en.wikipedia.org/wiki/Ptrace
[dwarf]: http://dwarfstd.org/
