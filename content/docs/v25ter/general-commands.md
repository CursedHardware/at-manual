---
title: General Commands
weight: 1
---

{{< hint info >}}Maximum Response Time: 300ms{{</ hint >}}

## ATI (Display Product Identification Information) {#ati}

The command delivers a product information text.

- Execution Command: `ATI`

  Response: TA issues product information text.

  ```at
  Quectel
  EC20F
  Revision: <revision>

  OK
  ```

  Parameter:

  - `<revision>` - Identification text of product software version

Example:

```at
ATI
Quectel
EC20F
Revision: EC20CEFDR01A01M4G

OK
```

## AT+GMI (Request Manufacturer Identification) {#at-gmi}

The command returns a manufacturer identification text.

See also `AT+CGMI`.

- Test Command: `AT+GMI=?`

  Response: `OK`

- Execution Command: `AT+GMI`

  TA reports one or more lines of information text which permits the user to identify the manufacturer.

  Response:

  ```at
  Quectel

  OK
  ```

## AT+GMM (Request TA Model Identification) {#at-gmm}

The command returns a product model identification text.

It is identical with `AT+CGMM`.

- Test Command: `AT+GMM=?`

  Response: `OK`

- Execution Command: `AT+GMM`

  TA returns a product model identification text.

  Response:

  ```at
  EC20F

  OK
  ```

## AT+GMR (Request TA Revision Identification of Software Release) {#at-gmr}

The command delivers a product firmware version identification text.

It is identical with `AT+CGMR`.

- Test Command: `AT+GMR=?`

  Response: `OK`

- Execution Command: `AT+GMR`

  TA reports one or more lines of information text which permits the user to identify the revision of software release.

  Response:

  ```at
  <revision>

  OK
  ```

  Parameter:

  - `<revision>` - Identification text of product software version

Example:

```at
AT+GMR
EC20CEFDR01A01M4G

OK
```

## AT+GSN (IMEI - Request International Mobile Equipment Identity) {#at-gsn}

The command returns the International Mobile Equipment Identity (IMEI) number of ME.

It is identical with `AT+CGSN`.

- Test Command: `AT+GSN=?`

  Response: `OK`

- Execution Command: `AT+GSN`

  TA reports the IMEI (International Mobile Equipment Identity) number in information text which permits the user to identify the individual ME device.

  Response:

  ```at
  <IMEI>

  OK
  ```

## AT&F (Set all Current Parameters to Manufacturer Defaults) {#at-f}

The command resets AT command settings to their factory default values.

- Execution Command: `AT&F[<value>]`

  TA sets all current parameters to the manufacturer defined profile. See Table 8.

  Response: `OK`

Parameter:

- `<value>` (Default: `0`) - Set all TA parameters to manufacturer defaults

## AT&V (Display Current Configuration) {#at-v}

The command displays the current settings of several AT command parameters,
including the single-letter AT command parameters which are not readable otherwise.

- Execution Command: `AT&V`

  TA returns the current parameter settings. See Example.

  Response: `OK`

Parameter:

- `<value>` (Default: `0`) - Set all TA parameters to manufacturer defaults

Example:

```at
AT&V
&C: 1
&D: 2
&F: 0
&W: 0
E: 1
Q: 0
V: 1
X: 4
Z: 0
S0: 0
S3: 13
S4: 10
S5: 8
S6: 2
S7: 0
S8: 2
S10: 15

OK
```

## AT&W (Store Current Parameters to User Defined Profile) {#at-w}

The command stores the current AT command settings to a user defined profile in non-volatile memory.

- Execution Command: `AT&W[<n>]`

  TA stores the current parameter settings in the user defined profile. See Table 9.

  Response: `OK`

## ATZ (Set all Current Parameters to User Defined Profile) {#at-z}

The command restores the current AT command settings to the user defined profile in non-volatile memory,
if they were stored with [AT&W]({{< ref "#at-w" >}}) before.

Any additional AT command on the same command line may be ignored.

- Execution Command: `ATZ[<value>]`

  TA sets all current parameters to the user defined profile. See Table 10.

  Response: `OK`

## ATQ (Set Result Code Presentation Mode) {#atq}

The command controls whether the result code is transmitted to the TE.

Other information text transmitted as response is not affected.

- Execution Command: `ATQ<n>`

  This parameter setting determines whether or not the TA transmits any result code to the TE.

  Information text transmitted in response is not affected by this setting.

  Response:

  When `<n>=0`: `OK`

  When `<n>=1`: (none)

  ```csv
  Name,Value,Note
  `<n>`,0,TA transmits result code
  ,1,Result codes are suppressed and not transmitted
  ```

## ATV (TA Response Format) {#atv}

The command determines the contents of header and trailer transmitted with AT command result codes and information responses.

The result codes, their numeric equivalents and brief descriptions of the use of each are listed in the following [table]({{< ref "#table-3" >}}).

- Execution Command: `ATV<value>`

  This parameter setting determines the contents of the header and trailer transmitted with result codes and information responses.

  Response:

  When `<value>=0`: `0`

  When `<value>=1`: `OK`

  ```csv
  Name,Value,
  `<value>`,0,"Information response: `<text><CR><LF>`\nResult Code Format: `<numeric code><CR>` (short)"
  `<value>`,1,"Information response: `<CR><LF><text><CR><LF>`\nResult Code Format: `<CR><LF><verbose code><CR><LF>` (long)"
  ```

Example:

```at
ATV1 // Set <value>=1
OK
AT+CSQ
+CSQ: 30,99

OK // When <value>=1, the result code is OK.
ATV0
0  // Set <value>=0.
AT+CSQ
+CSQ: 30,99
0  // When <value>=0, the result code is 0.
```

## ATE (Set Command Echo Mode) {#ate}

The command controls whether or not the module echoes characters received from TE during AT command mode.

- Execution Command: `ATE<value>`

  This setting determines whether or not the TA echoes characters received from TE during command mode.

  Response: `OK`

  ```csv
  Name,Value,Note
  `<value>`,0,Echo mode OFF
  ,1,Echo mode ON
  ```

## A/ (Repeat Previous Command Line) {#repeat}

The command repeats previous AT command line, and `/` acts as the line terminating character.

- Execution Command: `A/`

  Response: Repeat the previous command

Example:

```at
ATI
Quectel
EC20F
Revision: EC20CEFDR01A01M4G

OK
A/ // Repeat the previous command
EC20F
Revision: EC20CEFDR01A01M4G

OK
```

## ATS3 (Set Command Line Termination Character) {#ats3}

The command determines the character recognized by the module to terminate an incoming command line.

It is also generated for result codes and information text, along with character value set via `ATS4`.

- Read Command: `ATS3?`

  Response:

  ```at
  <n>

  OK
  ```

- Write Command: `ATS3=<n>`

  This parameter setting determines the character recognized by TA to terminate an incoming command line. The TA also returns this character in output.

  Response: `OK`

  ```csv
  Name,Value,Note
  `<n>`,0-127,Command line termination character (Default 13=`<CR>`)
  ```

## ATS4 (Set Response Formatting Character) {#ats4}

The command determines the character generated by the module for result code and information text, along with the command line termination character set via [ATS3]({{< ref "#ats3" >}}).

- Read Command: `ATS4?`

  Response:

  ```at
  <n>

  OK
  ```

- Write Command: `ATS4=<n>`

  This parameter setting determines the character generated by the TA for result code and information text.

  Response: `OK`

  ```csv
  Name,Value,Note
  `<n>`,0-127,Response formatting character (Default 10=`<LF>`)
  ```

## ATS5 (Set Command Line Editing Character) {#ats5}

The command determines the character value used by the module to delete the immediately preceding character from the AT command line (i.e. equates to backspace key).

- Read Command: `ATS5?`

  Response:

  ```at
  <n>

  OK
  ```

- Write Command: `ATS5=<n>`

  This parameter setting determines the character recognized by TA as a request to delete the immediately preceding character from the command line.

  Response: `OK`

  ```csv
  Name,Value,Note
  `<n>`,0-127,Command line editing character (Default 8=`<Backspace>`)
  ```

## ATX (Set **CONNECT** Result Code Format and Monitor Call Progress) {#atx}

The command determines whether or not the module transmits particular result codes to the TE.

It also controls whether or not the module verifies the presence of a dial tone when it begins dialing,
and whether or not engaged tone (busy signal) detection is enabled.

- Execution Command: `ATX<value>`

  This parameter setting determines whether or not the TA detected the presence of dial tone and busy signal and whether or not TA transmits particular result codes.

  Response: `OK`

  ```csv
  Name,Value,Note
  `<value>`,0,"**CONNECT** result code returned only.\nDial tone and busy detection are both disabled"
  ,1,"**CONNECT\<text>** result code returned only.\nDial tone and busy detection are both disabled"
  ,2,"**CONNECT\<text>** result code returned.\nDial tone detection is enabled,\nwhile busy detection is disabled"
  ,3,"**CONNECT\<text>** result code returned.\nDial tone detection is disabled,\nwhile busy detection is enabled"
  ,4,"**CONNECT\<text>** result code returned.\nDial tone and busy detection are both enabled"
  ```

## Table: ATV0 & ATV1 Result Codes Numeric Equivalents and Brief Description {#table-3}

```csv
ATV1,ATV0,Description
`OK`,0,Acknowledges execution of a command.
`CONNECT`,1,A connection has been established;\n the DCE is moving from command mode to data mode.
`RING`,2,The DCE has detected an incoming call signal from network.
`NO CARRIER`,3,The connection has been terminated\n or the attempt to establish a connection failed.
`ERROR`,4,"Command not recognized,\ncommand line maximum length exceeded,\nparameter value invalid,\nor other problem with processing the command line."
`NO DIALTONE`,6,No dial tone detected.
`BUSY`,7,Engaged (busy) signal detected.
`NO ANSWER`,8,"'@' (Wait for Quiet Answer) dial modifier was used,\n but remote ringing followed\n by five seconds\n of silence was not detected before expiration\n of the connection timer (S7)."
```
