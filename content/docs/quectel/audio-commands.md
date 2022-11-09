---
title: Audio Commands
weight: 12
---

## `AT+QTONEDET` DTMF Detection {#atqtonedet}

The command is used to enable or disable _DTMF_ detection.

When this function is enabled, _DTMF_ tones sent by other side will be detected, and it will be reported on the assigned serial port.

- Test Command: `AT+QTONEDET=?`

  Response:

  ```at
  +QTONEDET: (0,1)

  OK
  ```

- Read Command: `AT+QTONEDET?`

  Response:

  ```at
  +QTONEDET: <enable>

  OK
  ```

- Write Command:

  ```at
  AT+QTONEDET=<enable>

  OK // ERROR
  ```

Parameter:

- **\<enable>** - Enable or disable DTMF detection

  ```csv
  Value,Meaning
  0,Disable (By default)
  1,Enable
  ```

{{< hint info >}}

1. This setting will take effect immediately.

   And it will revert to the default values after resetting the module.

1. DTMF characters - ASCII:

   ```csv
   DTMF,ASCII Code
   0,48
   1,49
   2,50
   3,51
   4,52
   5,53
   6,54
   7,55
   8,56
   9,57
   A,65
   B,66
   C,67
   D,68
   \*,42
   \#,35
   ```

{{< /hint >}}
