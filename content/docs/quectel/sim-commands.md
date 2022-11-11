---
title: (U)SIM Related Commands
weight: 4
---

## `AT+QCCID` Show ICCID {#atqccid}

The command returns the ICCID (Integrated Circuit Card Identifier) number of the (U)SIM card.

- Test Command: `AT+QCCID=?`

  Response: `OK`

- Execution Command: `AT+QCCID`

  Response:

  ```at
  +QCCID: <iccid>

  OK // ERROR
  ```

Parameter:

- **\<iccid>** - ICCID (Integrated Circuit Card Identifier) number of the (U)SIM card

Example:

```at
AT+QCCID // Query ICCID of the (U)SIM card
+QCCID: 89860025128306012474

OK
```

## `AT+QPINC` Display PIN Remainder Counter {#atqpinc}

The command can query the number of attempts left to enter the password of (U)SIM PIN/PUK.

- Test Command: `AT+QPINC=?`

  Response:

  ```at
  +QPINC: ("SC","P2")

  OK
  ```

- Read Command: `AT+QPINC?`

  Response:

  ```at
  +QPINC: "SC",<pincounter>,<pukcounter>
  +QPINC: "P2",<pincounter>,<pukcounter>

  OK
  ```

- Write Command: `AT+QPINC=<facility>`

  Response:

  ```at
  +QPINC: <facility>,<pincounter>,<pukcounter>

  OK // ERROR
  ```

  If there is any error related to ME functionality:

  ```at
  +CME ERROR: <err>
  ```

Parameter:

- **\<facility>**

  - `"SC"` - (U)SIM PIN
  - `"P2"` - (U)SIM PIN2

- **\<pincounter>** - Number of attempts left to enter the password of PIN

- **\<pukcounter>** - Number of attempts left to enter the password of PUK

## `AT+QINISTAT` Query Initialization Status of (U)SIM Card {#atqinistat}

The command is used to query the initialization status of (U)SIM card.

- Test Command: `AT+QINISTAT=?`

  Response:

  ```at
  +QINISTAT: (0-7)

  OK
  ```

- Execution Command: `AT+QINISTAT`

  Response:

  ```at
  +QINISTAT: <status>

  OK
  ```

Parameter:

- **\<status>** - Initialization status of (U)SIM card.

  Actual value is the sum of several of the following four kinds

  e.g. 7=1+2+4 means _CPIN READY_ & _SMS DONE_ & _PB DONE_.

  ```csv
  Value,Meaning
  0,Initial state
  1,CPIN READY. Operation like lock/unlock PIN is allowed
  2,SMS initialization completed
  4,Phonebook initialization completed
  ```

## `AT+QSIMDET` (U)SIM Card Detection {#atqsimdet}

The command enables (U)SIM card hot-swap function. (U)SIM card is detected by GPIO interrupt.

The level of (U)SIM card detection pin should also be set when the (U)SIM card is inserted.

{{< hint info >}}

1. Hot-swap function is invalid if the configured value of **\<insertlevel>** is inconsistent with hardware design.
1. Hot-swap function takes effect after the module is restarted.

{{< /hint >}}

- Test Command: `AT+QSIMDET=?`

  Response:

  ```at
  +QSIMDET: (0,1),(0,1)

  OK
  ```

- Read Command: `AT+QSIMDET?`

  Response:

  ```at
  +QSIMDET: <enable>,<insertlevel>

  OK
  ```

- Write Command: `AT+QSIMDET=<enable>,<insertlevel>`

  Response: `OK` or `ERROR`

Parameter:

- **\<enable>** - (U)SIM card detection

  ```csv
  Value,Meaning
  0,Disable (U)SIM card detection (By default)
  1,Enable (U)SIM card detection
  ```

- **\<insertlevel>** - The level of (U)SIM detection pin when a (U)SIM card is inserted

  ```csv
  Value,Meaning
  0,Low level (By default)
  1,High level
  ```

Example:

```at
// Set (U)SIM card detection pin level as low when (U)SIM card is inserted
AT+QSIMDET=1,0
OK
// <Remove (U)SIM card>
+CPIN: NOT READY
// <Insert (U)SIM card>
+CPIN: READY // If PIN1 of the (U)SIM card is unlocked
```

## `AT+QSIMSTAT` (U)SIM Card Insertion Status Report {#atqsimstat}

The command queries (U)SIM card insertion status or determines whether (U)SIM card insertion status report is enabled.

The configuration of this command can be saved by **AT&W**.

- Test Command: `AT+QSIMSTAT=?`

  Response:

  ```at
  +QSIMSTAT: (0,1)

  OK
  ```

- Read Command: `AT+QSIMSTAT?`

  Response:

  ```at
  +QSIMSTAT: <enable>,<insertedstatus>

  OK
  ```

- Write Command: `AT+QSIMSTAT=<enable>`

  Response: `OK` or `ERROR`

Parameter:

- **\<enable>** - Enable or disable (U)SIM card insertion status report.

  If it is enabled, when (U)SIM card is removed or inserted,
  the URC `+QSIMSTAT: <enable>,<insertedstatus>` will be reported.

  ```csv
  Value,Meaning
  0,Disable (U)SIM card insertion status report (By default)
  1,Enable (U)SIM card insertion status report
  ```

- **\<insertedstatus>** - (U)SIM card is inserted or removed.

  This argument is not allowed to be set.

  ```csv
  Value,Meaning
  0,Removed
  1,Inserted
  2,"Unknown, before (U)SIM initialization"
  ```

Example:

```at
AT+QSIMSTAT? // Query (U)SIM card insertion status
+QSIMSTAT: 0,1

OK
AT+QSIMDET=1,0
OK
AT+QSIMSTAT=1
OK
AT+QSIMSTAT?
+QSIMSTAT: 1,1

OK
// <Remove (U)SIM card>
+QSIMSTAT: 1,0
+CPIN: NOT READY
AT+QSIMSTAT?
+QSIMSTAT: 1,0

OK
// <Insert (U)SIM card>
+QSIMSTAT: 1,1 // Report of (U)SIM card insertion status, inserted
+CPIN: READY
```
