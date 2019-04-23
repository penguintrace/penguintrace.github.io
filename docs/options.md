---
layout: docs
title: Options
permalink: /docs/options/
doc-order: 20
---

The table below lists the configuration options for penguinTrace. These can be
passed on the command-line in the format `-c OPTION VALUE`, or in a
configuration file which contains options in the format `OPTION = VALUE`, for
example:

    SERVER_GLOBAL = true
    SERVER_IPV6   = true
    SERVER_PORT   = 8080

The configuration file can be specified via the `-f FILE` command line option,
or '~/penguintrace.cfg' and './penguintrace.cfg' will be used if they exist.

The full set of options can also be listed by passing ``-o/--options`` on the
command-line.

|    **Option**       | **Type** | **Description**                            |
| `C_COMPILER_BIN`    | String   | Path to the C compiler                     |
| `CXX_COMPILER_BIN`  | String   | Path to the C++ compiler                   |
| `CLANG_BIN`         | String   | Path to clang (for libclang)               |
| `OBJCOPY_BIN`       | String   | Path to objcopy                            |
| `SERVER_PORT`       | Integer  | Port to listen on                          |
| `DELETE_TEMP_FILES` | Boolean  | Delete temporary files when a session ends |
| `SERVER_GLOBAL`     | Boolean  | Listen on all addresses, rather than just loopback |
| `SERVER_IPV6`       | Boolean  | Use IPv6                                   |
| `SINGLE_SESSION`    | Boolean  | Only one session exists per instance       |
| `USE_PTY`           | Boolean  | Use a pseudo-terminal to communicate with child processes, reduces effect of buffering |
| `TEMP_FILE_TPL_BINARIES` | String | Template for filenames for compiled executables |
| `TEMP_DIR_TPL`      | String   | Template for directories for isolated processes |
| `AUTO_STEP`         | Boolean  | Step without user input, for CLI tools     |
| `EXEC_NAME`         | String   | Executable name, passed to argv[0]         |
| `ARGC_MAX`          | Integer  | Maximum number of values to try and extrace from argc/argv |
| `CSTR_MAX_CHAR`     | Integer  | Maximum number of characters to try and print from a C style string |
| `LOG_COLOUR`        | Boolean  | Print log messages in colour               |
| `LOG_STDERR`        | Boolean  | Print log messages to STDERR               |
| `LOG_FILE`          | String   | File to save log messages to               |
| `LOG_CFG_FILE`      | String   | Log level configuration file               |
| `LOG_TIME`          | Boolean  | Include timestamp in log messages          |
| `STEP_AFTER_MAIN`   | Boolean  | Step again after reaching main/start symbol |
| `PTR_DEPTH`         | Integer  | Maximum number of pointer to follow        |
| `PRETTY_PRINT`      | Boolean  | Try to print C++ classes in a more readable way |
| `HIDE_NON_PRETTY_PRINT` | Boolean | Hide default representation if a pretty printer exists |
| `ISOLATE_TRACEE`    | Boolean  | Provide a limited amount of sandboxing of child processes |
| `STRICT_MODE`       | Boolean  | Enable `-Wall -Werror` when compiling      |
| `FILE_ARG`          | String   | Argument for command line tools            |

## Logging

A log file configuration can be specified through the `LOG_FILE` option, or
'~/penguintrace.cfg.log' and './penguintrace.cfg.log' will be used if they
exist.

In order of increasing severity log levels are TRACE, DBG, INFO, WARN and
ERROR. The levels are specified by component, for example:

    *                         = TRACE
    SERVER                    = INFO
    SERVER.API.route          = INFO
    SERVER.API.compile        = DBG
    SERVER.SESSION            = INFO
    SERVER.API.compile.PARSER = DBG

`*` is used to specify the base level if a level is not specified for a given
component.
