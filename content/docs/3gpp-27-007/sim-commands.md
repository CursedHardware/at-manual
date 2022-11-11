---
title: (U)SIM Related Commands
weight: 3
---

<!-- cspell:ignore BAIC BAOC BOIC FSIM NETSUB -->

## `AT+CIMI` Request IMSI {#atcimi}

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

## `AT+CLCK` Facility Lock {#atclck}

The command is used to lock, unlock or interrogate a MT or a network facility **\<fac>**.

It can be aborted when network facilities are being set or interrogated.

The factory default password of **PF**, **PN**, **PU**, **PP** and **PC** lock is `"12341234"`.

{{< hint warning >}}Maximum Response Time: 5s{{< /hint >}}

- Test Command: `AT+CLCK=?`

  Response:

  ```at
  +CLCK: (list of supported <fac>s)

  OK
  ```

- Write Command: `AT+CLCK=<fac>,<mode>[,<password>[,<class>]]`

  This command is used to lock, unlock or interrogate the ME or network facility **\<fac>**.

  Password is normally needed to do such actions. When querying the status of network service (**\<mode>**=2)

  The response line for "not active" case (**\<status>**=0) should be returned only

  If service is not active for any **\<class>**.

  If **\<mode>** is not equal to 2 and the command is set successfully:

  Response:

  ```at
  OK
  ```

  If **\<mode>**=2 and the command is set successfully:

  Response:

  ```at
  +CLCK: <status>[,<class>]
  +CLCK: <status>[,<class>]
  ...

  OK
  ```

Parameter:

- **\<fac>** - Facility

  - `"SC"` - (U)SIM lock SIM/UICC card installed in the currently selected card slot

    SIM/UICC asks password in MT power-up and when this lock command issued.

  - `"AO"` - BAOC (Bar All Outgoing Calls)

    Refer to [3GPP TS 22.088][22.088] clause 1.

  - `"OI"` - BOIC (Bar Outgoing International Calls)

    Refer to [3GPP TS 22.088][22.088] clause 1

  - `"OX"` - BOIC-exHC (Bar Outgoing International Calls except to Home Country)

    Refer to [3GPP TS 22.088][22.088] clause 1

  - `"AI"` - BAIC (Bar All Incoming Calls)

    Refer to [3GPP TS 22.088][22.088] clause 2

  - `"IR"` - BIC-Roam (Bar Incoming Calls when Roaming outside the home country)

    Refer to [3GPP TS 22.088][22.088] clause 2

  - `"AB"` - All Barring services (applicable only for **\<mode>**=0).

    Refer to [3GPP TS 22.030][22.030]

  - `"AG"` - All outgoing barring services (applicable only for **\<mode>**=0).

    Refer to [3GPP TS 22.030][22.030]

  - `"AC"` - All incoming barring services (applicable only for **\<mode>**=0).

    Refer to [3GPP TS 22.030][22.030]

  - `"FD"` - SIM card or active application in the UICC (GSM or USIM) fixed dialing memory feature

    If _PIN2_ authentication has not been done during the current session,
    _PIN2_ is required as **\<password>**.

  - `"PF"` - Lock Phone to the very first inserted SIM/UICC card

    Also referred in the present document as PH-FSIM

    MT asks password when other SIM/UICC cards are inserted.

  - `"PN"` - Network Personalization

    Refer to [3GPP TS 22.022][22.022]

  - `"PU"` - Network Subset Personalization

    Refer to [3GPP TS 22.022][22.022]

  - `"PP"` - Service Provider Personalization

    Refer to [3GPP TS 22.022][22.022]

  - `"PC"` - Corporate Personalization

    Refer to [3GPP TS 22.022][22.022]

- **\<mode>** - Mode

  ```csv
  Value,Meaning
  0,Unlock
  1,Lock
  2,Query status
  ```

- **\<password>** - Password (PIN code)

- **\<class>** - Class

  ```csv
  Value,Meaning
  1,Voice
  2,Data
  4,FAX
  7,All telephony except SMS (Default)
  8,Short message service
  16,Data circuit synchronization
  32,Data circuit asynchronous
  ```

- **\<status>** - Status

  ```csv
  Value,Meaning
  0,OFF
  1,ON
  ```

Example:

```at
AT+CLCK="SC",2        // Query the status of (U)SIM card
+CLCK: 0              // The (U)SIM card is unlocked (OFF)

OK
AT+CLCK="SC",1,"1234" // Lock (U)SIM card, and the password is 1234

OK
AT+CLCK="SC",2        // Query the status of (U)SIM card
+CLCK: 1              // The (U)SIM card is locked (ON)

OK
AT+CLCK="SC",0,"1234" // Unlock (U)SIM card
OK
```

## `AT+CPIN` Enter PIN {#atcpin}

The command is used to enter a password or query whether or not the module requires a password which is necessary before it can be operated.

The password may be **(U)SIM PIN**, **(U)SIM PUK**, **PH-SIM PIN**, etc.

{{< hint warning >}}Maximum Response Time: 5s{{< /hint >}}

- Test Command: `AT+CPIN=?`

  Response: `OK`

- Read Command: `AT+CPIN?`

  TA returns an alphanumeric string indicating whether or not some password is required.

  Response:

  ```at
  +CPIN: <code>

  OK
  ```

- Write Command: `AT+CPIN=<pin>[,<new pin>]`

  TA stores a password, such as (U)SIM PIN, (U)SIM PUK, etc., which is necessary before it can be operated.

  If the PIN is to be entered twice, the TA shall automatically repeat the PIN.

  If no PIN request is pending, no action is taken and an error message **+CME ERROR** is returned to TE.

  If the PIN required is (U)SIM PUK or (U)SIM PUK2, the second pin is required.

  This second pin **\<new pin>** is used to replace the old pin in the (U)SIM.

  Response: `OK`

Parameter:

- **\<pin>** - String type. Password.

  If the requested password was a PUK, such as (U)SIM PUK1, PH-FSIM PUK or other passwords,
  then **\<pin>** must be followed by **\<new pin>**.

- **\<new pin>** - String type. New password.

  New password required if the requested code was a PUK.

- **\<code>**

  ```csv
  Code,Meaning
  READY,MT is not pending for any password
  SIM PIN,MT is waiting for (U)SIM PIN to be given
  SIM PUK,MT is waiting for (U)SIM PUK to be given
  SIM PIN2,MT is waiting for (U)SIM PIN2 to be given
  SIM PUK2,MT is waiting for (U)SIM PUK2 to be given
  PH-NET PIN,MT is waiting for network personalization password to be given
  PH-NET PUK,MT is waiting for network personalization unblocking password to be given
  PH-NETSUB PIN,MT is waiting for network subset personalization password to be given
  PH-NETSUB PUK,MT is waiting for network subset personalization unblocking password to be given
  PH-SP PIN,MT is waiting for service provider personalization password to be given
  PH-SP PUK,MT is waiting for service provider personalization unblocking password to be given
  PH-CORP PIN,MT is waiting for corporate personalization password to be given
  PH-CORP PUK,MT is waiting for corporate personalization unblocking password to be given
  ```

Example:

```at
AT+CPIN?        // Queried PIN code is locked
+CPIN: SIM PIN

OK
AT+CPIN=1234     // Enter PIN
OK

+CPIN: READY
AT+CPIN?         // PIN has already been entered
+CPIN: READY

OK

AT+CPIN?
+CPIN: SIM PUK
OK
AT+CPIN="26601934","1234" // Enter PUK and PIN
OK

+CPIN: READY
AT+CPIN?
+CPIN: READY

OK
```

## `AT+CPWD` Change Password {#atcpwd}

The command sets a new password for the facility lock function defined by **AT+CLCK**.

{{< hint warning >}}Maximum Response Time: 5s{{< /hint >}}

- Test Command: `AT+CPWD=?`

  TA returns a list of pairs which present the available facilities and the maximum length of their password.

  Response:

  ```at
  +CPWD: (list of supported <fac>s),(<pwdlength>s)

  OK
  ```

- Write Command: `AT+CPWD=<fac>,<oldpwd>,<newpwd>`

  TA sets a new password for the facility lock function.

  Response: `OK`

Parameter:

- **\<fac>** - Facility

  - `"SC"` - (U)SIM (lock SIM/UICC card)

    SIM/UICC asks password in MT power-up and when this lock command is issued

  - `"AO"` - BAOC (Bar All Outgoing Calls)

    Refer to [3GPP TS 22.088][22.088] clause 1

  - `"OI"` - BOIC (Bar Outgoing International Calls)

    Refer to [3GPP TS 22.088][22.088] clause 1

  - `"OX"` - BOIC-exHC (Bar Outgoing International Calls except to Home Country)

    Refer to [3GPP TS 22.088][22.088] clause 1

  - `"AI"` - BAIC (Bar All Incoming Calls)

    Refer to [3GPP TS 22.088][22.088] clause 2

  - `"IR"` - BIC-Roam (Bar Incoming Calls when Roaming outside the home country)

    Refer to [3GPP TS 22.088][22.088] clause 2

  - `"AB"` - All Barring services (applicable only for **\<mode>**=0).

    Refer to [3GPP TS 22.030][22.030]

  - `"AG"` - All outgoing barring services (applicable only for **\<mode>**=0).

    Refer to [3GPP TS 22.030][22.030]

  - `"AC"` - All incoming barring services (applicable only for **\<mode>**=0).

    Refer to [3GPP TS 22.030][22.030]

  - `"P2"` - (U)SIM PIN2

- **\<pwdlength>** - Integer type. Maximum length of password

- **\<oldpwd>** - Password specified for the facility from the user interface or with command.

- **\<newpwd>** - New password

Example:

```at
AT+CPIN?
+CPIN: READY

OK
AT+CPWD="SC","1234","4321" // Change (U)SIM card password to “4321”
OK

// Restart module or re-activate the SIM card
AT+CPIN? // Query PIN code is locked
+CPIN: SIM PIN

OK
AT+CPIN="4321" // PIN must be entered to define a new password "4321"

OK
+CPIN: READY
```

## `AT+CSIM` Generic (U)SIM Access {#atcsim}

The command allows a direct control of the (U)SIM that is installed in the currently selected card slot by a distant application on the TE.

The TE shall then keep the processing of (U)SIM information within the frame specified by GSM/UMTS.

- Test Command: `AT+CSIM=?`

  Response: `OK`

- Write Command: `AT+CSIM=<length>,<command>`

  Response:

  ```at
  +CSIM: <length>,<response>

  OK // or ERROR
  ```

  If there is any error related to ME functionality:

  ```at
  +CME ERROR: <err>
  ```

Parameter:

- **\<length>** - Integer type.

  Length of **\<command>** or **\<response>** string.

- **\<command>**

  Command transferred
  by the _MT_
  to the _(U)SIM_ in
  the format as described in [3GPP TS 51.011][51.011].

- **\<response>**

  Response to the command transferred
  by the _(U)SIM_
  to the _MT_ in
  the format as described in [3GPP TS 51.011][51.011].

## `AT+CRSM` Restricted (U)SIM Access {#atcrsm}

The command offers easy and limited access to the (U)SIM database.

It transmits the (U)SIM command number **\<command>** and its required parameters to the MT.

- Test Command: `AT+CRSM=?`

  Response: `OK`

- Write Command: `AT+CRSM=<command>[,<fileld>[,<P1>,<P2>,<P3>[,<data>][,<pathld>]]]`

  Response:

  ```at
  +CRSM: <sw1>,<sw2>[,<response>]

  OK // ERROR
  ```

  If there is any error related to ME functionality:

  ```at
  +CME ERROR: <err>
  ```

Parameter:

- **\<command>** - (U)SIM command number

  ```csv
  Command,Meaning
  176,READ BINARY
  178,READ RECORD
  192,GET RESPONSE
  214,UPDATE BINARY
  220,UPDATE RECORD
  242,STATUS
  ```

- **\<fileId>** - Integer type.

  Identifier for an elementary data file on (U)SIM, if used by **\<command>**.

- **\<P1>**, **\<P2>**, **\<P3>** - Integer type.

  Parameters transferred by the MT to the (U)SIM.

  These parameters are mandatory for every command, except _GET RESPONSE_ and _STATUS_.

  The values are described in [3GPP TS 51.011][51.011].

- **\<data>** - Information which shall be written to the (U)SIM

  hexadecimal character format; refer to [AT+CSCS]({{< ref "general-commands#atcscs" >}})

- **\<pathId>** - The directory path of an elementary file on a SIM/UICC in hexadecimal format.

- **\<sw1>**, **\<sw2>** - Integer type.

  Information from the (U)SIM about the execution of the actual command.

  These parameters are delivered to the TE in both cases, on successful or failed execution of the command.

- **\<response>** - Response of a successful completion of the command previously issued

  (hexadecimal character format; refer to [AT+CSCS]({{< ref "general-commands#atcscs" >}})).

  _STATUS_ and _GET RESPONSE_ return data, which gives information about the current elementary data field.

  The information includes the type of file and its size (refer to [3GPP TS 51.011][51.011]).

  After _READ BINARY_, _READ RECORD_ or _RETRIEVE DATA_ command, the requested data will be returned.

  **\<response>** is not returned after a successful _UPDATE BINARY_, _UPDATE RECORD_ or _SET DATA_ command.

[22.022]: https://www.3gpp.org/DynaReport/22022.htm
[22.030]: https://www.3gpp.org/DynaReport/22030.htm
[22.088]: https://www.3gpp.org/DynaReport/22088.htm
[51.011]: https://www.3gpp.org/DynaReport/51011.htm
