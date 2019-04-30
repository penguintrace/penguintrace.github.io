---
layout: post
title:  "Welcome and Background"
date:   2019-04-29 20:00:00 +0100
#categories: jekyll update
excerpt_separator: <!--more-->
---
Welcome to the penguinTrace project, a tool to allow you to write code and see
how the instructions that make it up get executed. The hope is that it can help
people to understand how programs execute, or improve understanding of assembly.

This post gives a few details about the background, intentions and status of the project.
<!--more-->

### Background

When writing C programs it's possible to get the compiler to output the generated
assembly, or disassemble a binary to see the instructions. However, seeing the
instructions in a static form doesn't show the flow through the program. Using
a debugger you can step through the program but debuggers provide a lot of
functionality and so it can be complicated to just show the instructions being
executed.

The intention of penguinTrace is to provide a simple interface to compile and
step through a program. It is also intended to support different architectures,
for example running on a Raspberry Pi (AArch64), as well as x86_64. For this
reason, penguinTrace runs as a web server that can be connected to from a
browser. This is more lightweight than running a graphical editor/debugger
and means that it can be run without needing a monitor.

Some technical information about how penguinTrace is put together is available
on the [More Details](/details/) page.

### Status

This project is a personal project, developed with the hope that it will be
useful to someone to explore how programs are executed. It was also used as a
way to learn more about how executables, binaries and debuggers work.

Most of the functionality is implemented, although there are some elements of
the DWARF specification that are not fully implemented. This may mean that some
programs will give an error if the debug information for that program contains
an unsupported feature. Also, stepping through C++ programs should work, but
not all C++ types can be represented properly in the web interface.
`std::string`, `std::list`, `std::vector` and `std::map` should all be
displayed in a more readable format.

If you find something not working, or want to give any feedback, create an
[issue](https://github.com/penguintrace/penguintrace/issues/new/choose) on
GitHub.

To get started running penguinTrace, head to the [Introduction](/intro/) or
follow the instructions in the
[repository](https://github.com/penguintrace/penguintrace).
