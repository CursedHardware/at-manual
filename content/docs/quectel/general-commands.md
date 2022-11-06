---
title: General Commands
weight: 1
---

## `AT+QURCCFG` (Configure URC Indication Option)

The command is used to configure the output port of URC.

- Test Command: `AT+QURCCFG=?`

  Response:

  ```at-command
  +QURCCFG: "urcport",("usbat","usbmodem","uart1")

  OK
  ```

- Write Command: `AT+QURCCFG="urcport"[,<urcportvalue>]`

  If the configuration parameter `<urcportvalue>` is omitted, return current configuration:

  Resposne:

  ```at-command
  +QURCCFG: "urcport",<urcportvalue>

  OK
  ```

  If the configuration parameter `<urcportvalue>` is not omitted, response:

  Resposne: `OK` or `ERROR`

Parameter:

```csv
Name,Meaning
`<urcportvalue>`,Set URC output port
```

```csv
urcportvalue,Meaning
"usbat",USB AT port
"usbmodem",USB modem port
"uart1",Main UART
```
