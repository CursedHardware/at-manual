---
title: AT Commands
weight: 1
---

## `AT+QGPSCFG` Configure GNSS

## `AT+QGPSDEL` Delete Assistance Data

## `AT+QGPS` Operate GPS Session

## `AT+QGPSEND` Terminate GNSS Session

## `AT+QGPSLOC` Obtain Position

## `AT+QGPSGNMEA` Obtain NMEA Sentences

## `AT+QGPSXTRA` Enable gpsOneXTRA Functionality

## `AT+QGPSXTRATIME` Inject gpsOneXTRA Time

This command can be used to inject time to GNSS engine.

Before using it, you must turn off the GNSS engine and configure **\<xtraenable>** by **AT+QGPSXTRA**.

After activating gpsOneXTRA functionality, GNSS engine will ask for gpsOneXTRA time and gpsOneXTRA data.

Meanwhile, before injecting gpsOneXTRA data, gpsOneXTRA time must be injected first by this command.

- Test Command: `AT+QGPSXTRATIME=?`

  Response:

  ```at
  +QGPSXTRATIME: 0,<xtratime>,(0,1),(0,1),<uncrtn>

  OK
  ```

- Read Command: `AT+QGPSXTRATIME?`

  Response:

  ```at
  OK
  ```

- Execution Command: `AT+QGPSXTRATIME=<op>,<xtratime>[,<utc>[,<force>,<uncrtn>]]`

  Inject XTRA time manually

  Response:

  ```at
  OK
  ```

  If error is related to ME functionality:

  ```at
  +CME ERROR: <errcode>
  ```

- **\<op>** - Operation type

  0 - Inject gpsOneXTRA time

- **\<xtratime>** - Current UTC/GPS time

  The format of time: `yyyy/MM/dd,hh:mm:ss`, e.g: `2015/01/03,15:34:50`.

- **\<utc>** - The type of time

  0 - GPS time

  1 - UTC time

- **\<force>** - Force or allow GPS subsystem to accept the time entered.

  0 - Allow acceptances

  1 - Force acceptances

- **\<uncrtn>** - Uncertainty of time.

  Unit: ms, default value: _3500ms_.

  It indicates the time difference between sending a request to the SNTP server and receiving a response from the SNTP server.

  If the set time is less than 3.5s, it will be counted as 3.5s.

- **\<errcode>** - Integer type, indicate the error code of the operation.

  If it is not 0, it is the type of error.

  Please refer to the [Summary of Error Codes]({{< ref "#error-codes" >}})

## `AT+QGPSXTRADATA` Inject gpsOneXTRA Data Manually

This command can be used to inject gpsOneXTRA data to GNSS engine.

Before using it, you must turn off the GNSS engine and enable XTRA by **AT+QGPSXTRA**.

Meanwhile, before injecting gpsOneXTRA data, gpsOneXTRA time must be injected first by **AT+QGPSXTRATIME**.

Before operating **AT+QGPSXTRADATA** command, you should store the valid gpsOneXTRA data into RAM or UFS of the module (recommended to save it to RAM).

After operating this command successfully, gpsOneXTRA data can be deleted.

At this moment, you can query the validity of gpsOneXTRA data by **AT+QGPSXTRADATA?**.

- Test Command: `AT+QGPSXTRADATA=?`

  Response:

  ```at
  +QGPSXTRADATA: <xtradatafilename>

  OK
  ```

- Read Command: `AT+QGPSXTRADATA?`

  Query the validity of the current gpsOneXTRA data

  Response:

  ```at
  +QGPSXTRADATA: <xtradatadurtime>,<injecteddatatime>

  OK
  ```

  If error is related to ME functionality:

  ```at
  +CME ERROR: <errcode>
  ```

- Execution Command: `AT+QGPSXTRADATA=<xtradatafilename>`

  Inject gpsOneXTRA data manually

  Response:

  ```at
  OK
  ```

  If error is related to ME functionality:

  ```at
  +CME ERROR: <errcode>
  ```

Parameter:

- **\<xtradatafilename>** - Filename of gpsOneXTRA data file, e.g: "xtra.bin" or "xtra2.bin"

- **\<xtradatadurtime>** - Valid time of injected gpsOneXTRA data, unit: minute.

  ```csv
  Value,Meaning
  0,No gpsOneXTRA file or gpsOneXTRA file is overdue
  1 - 10080,Valid time of gpsOneXTRA file
  ```

- **\<injecteddatatime>** - Starting time of the valid time of XTRA data

  Format: `yyyy/MM/dd,hh:mm:ss`, e.g: `2015/01/03,15:34:50`

- **\<errcode>** - Integer type, indicates the error code of the operation.

  If it is not 0, it is the type of error.

  Please refer to the [Summary of Error Codes]({{< ref "#error-codes" >}})

## `+QGPSURC` Expired XTRA Data (URC)

```at
// XTRA data is expired, and need to be updated.
+QGPSURC: "xtradataexpire",<xtradatadurtime>,<injecteddatatime>
```

Parameter:

- **\<xtradatadurtime>** - Valid time of injected XTRA data

  unit: minute.

  special value: `0`, No XTRA file or XTRA file is expired

- **\<injecteddatatime>** - Starting time of the valid time of XTRA data

  Format: `yyyy/MM/dd,hh:mm:ss`, e.g: `2015/01/03,15:34:50`
