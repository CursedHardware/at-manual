---
title: Unspecific Commands
weight: 1000
---

## `AT+EGMR` Modem Revision {#ategmr}

{{< hint warning >}}The command available **unknown**{{< /hint >}}

- Test Command: `AT+EGMR=?`

  Response:

  ```at
  +EGMR: (list of supported <mode>s),(list of supported <format>s)

  OK
  ```

- Read Command: `AT+EGMR=<mode>,<format>`

  Response:

  ```at
  +EGMR: <mode>,<format>,<data>

  OK
  ```

- Write Command: `AT+EGMR=<mode>,<format>,<data>`

  Response: `OK` or `ERROR`

Parameter:

```csv
Name,Value,Meaning
\<mode>,0,[Unknown]
,1,Write
,2,Read
\<format>,5,[Unknown]
,7,SIM 1 slot IMEI
,9,[Unknown]
,10,SIM 2 slot IMEI
```

Example:

```at
AT+GSN
+GSN: "111111111111111"

OK
AT+EGMR=1,7,"000000000000000"
OK
AT+GSN
+GSN: "000000000000000"

OK
```

see <https://github.com/the-modem-distro/pinephone_modem_sdk/issues/39>

see <https://docs.ai-thinker.com/_media/b_and_t/nb-iot/n92/kaifazhidaowendang/rda8908a_at_commandmanual9.0.pdf>
