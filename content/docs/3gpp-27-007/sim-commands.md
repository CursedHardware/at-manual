---
title: (U)SIM Related Commands
weight: 3
---

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

{{< hint warning >}}

- Maximum Response Time: 5s

{{< /hint >}}

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
  Value,Note
  0,Unlock
  1,Lock
  2,Query status
  ```

- **\<password>** - Password (PIN code)

- **\<class>** - Class

  ```csv
  Value,Note
  1,Voice
  2,Data
  4,FAX
  7,All telephony except SMS (Default)
  8,Short message service
  16,Data circuit synchronization
  32,Data circuit asynchronization
  ```

- **\<status>** - Status

  ```csv
  Value,Note
  0,OFF
  1,ON
  ```

[22.088]: https://www.3gpp.org/DynaReport/22088.htm
[22.030]: https://www.3gpp.org/DynaReport/22030.htm
[22.022]: https://www.3gpp.org/DynaReport/22022.htm

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

## `AT+CPWD` Change Password {#atcpwd}

The command sets a new password for the facility lock function defined by **AT+CLCK**.

## `AT+CSIM` Generic (U)SIM Access {#atcsim}

The command allows a direct control of the (U)SIM that is installed in the currently selected card slot by a distant application on the TE.

The TE shall then keep the processing of (U)SIM information within the frame specified by GSM/UMTS.

## `AT+CRSM` Restricted (U)SIM Access {#atcrsm}

The command offers easy and limited access to the (U)SIM database.

It transmits the (U)SIM command number **\<command>** and its required parameters to the MT.
