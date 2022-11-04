---
title: General Commands
weight: 1
---

## `AT+CFUN` Set Phone Functionality {#atcfun}

The command controls the functionality level. It can also be used to reset the UE.

{{< hint warning >}}

- Maximum Response Time: 15s, determined by network.

{{< /hint >}}

- Test Command: `AT+CFUN=?`

  Response:

  ```at
  +CFUN: (list of supported <fun>s),(list of supported <rst>s)

  OK
  ```

- Read Command: `AT+CFUN?`

  Response:

  ```at
  +CFUN: <fun>

  OK
  ```

- Write Command: `AT+CFUN=<fun>[,<rst>]`

  Response: `OK`

  If there is any error related to ME functionality: `+CME ERROR: <err>`

Example:

```at
AT+CFUN=0
OK
AT+COPS?
+COPS: 0

OK
AT+CPIN?
+CME ERROR: 13
AT+CFUN=1
OK

+CPIN: SIM PIN
AT+CPIN=1234
OK

+CPIN: READY
+QUSIM: 1
+QIND: PB DONE
+QIND: SMS DONE

AT+CPIN?
+CPIN: READY

OK
AT+COPS?
+COPS: 0,0,"CHINA MOBILE",7

OK
```

## `AT+CMEE` Error Message Format {#atcmee}

The command controls the format of error result codes: **ERROR**,
error numbers or verbose messages as **+CME ERROR: \<err>** and **+CMS ERROR: \<err>**.

- Test Command: `AT+CMEE=?`

  Response:

  ```at
  +CMEE: (list of supported <n>s)

  OK
  ```

- Read Command: `AT+CMEE?`

  Resposne:

  ```at
  +CMEE: <n>

  OK
  ```

- Write Command: `AT+CMEE=<n>`

  TA disables or enables the use of result code **+CME ERROR: \<err>**
  as an indication of an error related to the functionality of the ME.

  Response: `OK`

  ```csv
  Name,Value,Meaning
  `<n>`,0,Disable result code
  ,1,Enable result code and use numeric values
  ,2,Enable result code and use verbose values
  ```

Example:

```at
AT+CMEE=0
OK
AT+CPIN?
ERROR
AT+CMEE=1
OK
AT+CPIN?
+CME ERROR: 10
AT+CMEE=2

OK
AT+CPIN?
+CME ERROR: SIM not inserted
```

## `AT+CSCS` Select TE Character Set {#atcscs}

The Write Command informs the module which character set is used by the TE.

This enables the UE to convert character strings correctly between TE and UE character sets.

- Test Command: `AT+CSCS=?`

  Response:

  ```at
  +CSCS: (list of supported <chset>s)

  OK
  ```

- Read Command: `AT+CSCS?`

  Response:

  ```at
  +CSCS: <chset>

  OK
  ```

- Write Command: `AT+CSCS=<chset>`

  Set character set **\<chset>** which is used by the TE. The TA can then convert character strings correctly between the TE and ME character sets.

  Response: `OK`

  ```csv
  Name,Value,Meaning
  `<chset>`,GSM,GSM default alphabet
  ,IRA,International reference alphabet
  ,UCS2,UCS2 alphabet
  ```

Example:

```at
AT+CSCS?
+CSCS: "GSM"

OK
AT+CSCS="UCS2"
OK
AT+CSCS?
+CSCS: "UCS2"

OK
```
