---
title: Introduction
bookToC: false
---

The **Hayes command set** (also known as the **AT command set**) is a specific command language originally developed by Dennis Hayes for the Hayes SmartModem 300 baud modem in 1981.

- <https://en.wikipedia.org/wiki/Hayes_command_set>
- <https://en.wikipedia.org/wiki/Voice_modem_command_set>

## AT Command Syntax

The `AT` or `at` prefix must be set at the beginning of each command line.

To terminate a command line enter `<CR>`.

Commands are usually followed by a response that includes `<CR><LF><response><CR><LF>`.

Throughout this document, only the responses are presented, `<CR><LF>` are omitted intentionally.

- ITU-T V.25ter
- 3GPP TS 27.005
- 3GPP TS 27.007

They are listed as follows:

- Basic syntax

  These AT commands have the format of `AT<x><n>`,
  or `AT&<x><n>`,
  where `<x>` is the command,
  and `<n>` is/are the argument(s)
  for that command.

  An example of this is `ATE<n>`,
  which tells the _DCE_ whether received characters
  should be echoed back to the _DTE_ according
  to the value of `<n>`.

  `<n>` is optional and a default will be used if it is missing.

- _S_ parameter syntax

  These AT commands have the format of `ATS<n>=<m>`,
  where `<n>` is the index of the _S_ register to set,
  and `<m>` is the value to assign to it.

- Extended syntax

  These commands can be operated in several modes, as following table:

  Table 1: Types of AT Commands and Responses

  - Test Command:

    ```at
    AT+<x>=?
    ```

    This command returns the list of parameters and value ranges set by the corresponding Write Command or internal processes.

  - Read Command:

    ```at
    AT+<x>?
    ```

    This command returns the currently set value of the parameter or parameters.

  - Write Command:

    ```at
    AT+<x>=<...>
    ```

    This command sets the user-definable parameter values.

  - Execution Command:

    ```at
    AT+<x>
    ```

    This command reads non-variable parameters affected by internal processes in the _UE_.
