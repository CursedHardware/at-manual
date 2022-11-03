---
title: Status Control Commands
weight: 3
---

## AT+CEER (Extended Error Report) {#atceer}

The command is used to query an extended error and report the cause of the last failed operation, such as:

- The failure to release a call
- The failure to set up a call (both mobile originated or terminated)
- The failure to modify a call by using supplementary services
- The failure to activate, register, query, deactivate or deregister a supplementary service
- The failure to attach GPRS or the failure to activate PDP context
- The failure to detach GPRS or the failure to deactivate PDP context

The release cause **\<text>** is a text to describe the cause information given by the network.

- Test Command: `AT+CEER=?`

  Response: `OK`

- Execution Command: `AT+CEER`

  Response:

  ```at
  +CEER: <text>

  OK // ERROR
  ```

  If there is any error related to ME functionality:

  ```at
  +CME ERROR: <err>
  ```

Parameter:

- **\<text>** - Release cause text.

  Reason for the last call failure to [setup or release]({{< ref "at+ceer" >}})

  Both CS and PS domain call types are reported.

  Cause data is captured from Call Manager events and cached locally to later use by this command.

## AT+QCFG (Extended Configuration Settings) {#atqcfg}

## AT+QINDCFG (URC Indication Configuration) {#atqindcfg}

The command is used to control URC indication.

- Test Command: `AT+QINDCFG=?`

  Response:

  ```at
  +QINDCFG: "all",(0,1),(0,1)
  +QINDCFG: "csq",(0,1),(0,1)
  +QINDCFG: "smsfull",(0,1),(0,1)
  +QINDCFG: "ring",(0,1),(0,1)
  +QINDCFG: "smsincoming",(0,1),(0,1)

  OK
  ```

- Write Command: `AT+QINDCFG=<urctype>[,<enable>[,< savetonvram>]]`

  Response:

  If **\<enable>** and **\<savetonvram>** are omitted, the current configuration will be returned:

  ```at
  +QINDCFG: <urctype>,<enable>

  OK
  ```

  If **\<enable>** and **\<savetonvram>** are not omitted, set the URC indication configurations:

  `OK` or `ERROR`

  If there is any error related to ME functionality:

  ```at
  +CME ERROR: <err>
  ```

Parameter:

- **\<urctype>** - URC type

  - `"all"` (Default is ON)

    Main switch of all URCs.

  - `"csq"` (Default is OFF)

    Indication of signal strength and channel bit error rate change (similar to **AT+CSQ**).

    If this configuration is ON, present: **+QIND: ""csq"",<rssi>,<ber>**"

  - `"smsfull"` (Default is OFF)

    SMS storage full indication.

    If this configuration is ON, present: +QIND: "smsfull",\<storage>

  - `"ring"` (Default is ON)

    **RING** indication.

  - `"smsincoming"` (Default is ON)

    Incoming message indication.

    Related URCs list: **+CMTI**, **+CMT**, **+CDS**

- **\<enable>** - URC indication is ON or OFF

  ```csv
  Value,Note
  0,OFF
  1,ON
  ```

- **\<savetonvram>** - Whether to save configuration into NV.

  ```csv
  Value,Note
  0,Not save (by default)
  1,Save
  ```
