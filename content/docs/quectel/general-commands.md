---
title: General Commands
weight: 1
---

## AT+QURCCFG (Configure URC Indication Option)

The command is used to configure the output port of URC.

- Test Command: `AT+QURCCFG=?`

  Response:

  ```at
  +QURCCFG: "urcport",("usbat","usbmodem","uart1")

  OK
  ```

- Write Command: `AT+QURCCFG="urcport"[,<urcportvalue>]`

  If the configuration parameter `<urcportvalue>` is omitted, return current configuration:

  Resposne:

  ```at
  +QURCCFG: "urcport",<urcportvalue>

  OK
  ```

  If the configuration parameter `<urcportvalue>` is not omitted, response:

  Resposne: `OK` or `ERROR`

Parameter:

```csv
Name,Note
`<urcportvalue>`,Set URC output port
```

```csv
urcportvalue,Note
"usbat",USB AT port
"usbmodem",USB modem port
"uart1",Main UART
```
