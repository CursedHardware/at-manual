---
title: (U)SIM Related Commands
weight: 3
---

## AT+CIMI (Request IMSI) {#atcimi}

The command requests the International Mobile Subscriber Identity (IMSI) which is intended to permit the TE to identify the individual SIM card or active application in the UICC (GSM or USIM) that is attached to MT.

- Test Command: `AT+CIMI=?`

  Response: `OK`

- Execution Command: `AT+CIMI`

  TA returns **\<IMSI>** for identifying the individual (U)SIM which is attached to ME.

  Response:

  ```at
  <IMSI>

  OK
  ```

  If there is any error related to ME functionality:

  ```at
  +CME ERROR: <err>
  ```

Parameter:

- **\<IMSI>** - International Mobile Subscriber Identity (string without double quotes)

Example:

```at
AT+CIMI
460023210226023 // Query IMSI number of (U)SIM which is attached to ME

OK
```
