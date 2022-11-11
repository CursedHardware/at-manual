---
title: Status Control Commands
weight: 3
---

<!-- cspell:enableCompoundWords -->
<!-- cspell:words signal attach SGSN -->

## `AT+CEER` Extended Error Report {#atceer}

The command is used to query an extended error and report the cause of the last failed operation, such as:

- The failure to release a call
- The failure to set up a call (both mobile originated or terminated)
- The failure to modify a call by using supplementary services
- The failure to activate, register, query, deactivate or deregister a supplementary service
- The failure to attach GPRS or the failure to activate PDP context
- The failure to detach GPRS or the failure to deactivate PDP context

The [release cause]({{< ref "at+ceer-cause" >}}) **\<text>** is a text to describe the cause information given by the network.

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

- **\<text>** - [Release cause text]({{< ref "at+ceer-cause" >}}).

  Reason for the last call failure to setup or release

  Both CS and PS domain call types are reported.

  Cause data is captured from Call Manager events and cached locally to later use by this command.

## `AT+QCFG` Extended Configuration Settings {#atqcfg}

The command is used to query and configure various settings of UE.

- Test Command: `AT+QCFG=?`

  Response:

  ```at
  +QCFG: "gprsattach",(list of supported <attachmode>s)
  +QCFG: "nwscanmode",(list of supported <scanmode>s),(list of supported <effect>s)
  +QCFG: "nwscanseq",(list of supported <scanseq>s),(list of supported <effect>s)
  +QCFG: "roamservice",(list of supported <roammode>s),(list of supported <effect>s)
  +QCFG: "servicedomain",(list of supported <service>s),(list of supported <effect>s)
  +QCFG: "band",(list of supported <bandval>s),(list of supported <ltebandval>s),(list of supported <effect>s)
  +QCFG: "hsdpacat",(list of supported <cat>s)
  +QCFG: "hsupacat",(list of supported <cat>s)
  +QCFG: "rrc",(list of supported <rrcr>s)
  +QCFG: "sgsn",(list of supported <sgsnr>s)
  +QCFG: "msc",(list of supported <mscr>s)
  +QCFG: "pdp/duplicatechk",(list of supported <enable>s)
  +QCFG: "tdscsq",(list of supported <value>s)
  +QCFG: "urc/ri/ring",(list of supported <typeri>s),(list of supported <pulseduration>s),(list of supported <activeduration>s),(list of supported <inactiveduration>s),(list of supported <ringnodisturbing>s)
  +QCFG: "urc/ri/smsincoming",(list of supported <typeri>s),(list of supported <pulseduration>s)
  +QCFG: "urc/ri/other",(list of supported <typeri>s),(list of supported <pulseduration>s)
  +QCFG: "risignaltype",(list of supported <risignatype>s)
  +QCFG: "urc/cache",(list of supported <value>s)
  +QCFG: "tone/incoming",(list of supported <value>s)

  OK
  ```

### `AT+QCFG="gprsattach"` GPRS Attach Mode Configuration {#atqcfg-gprsattach}

The command specifies the mode to attach GPRS when UE is powered on.

This configuration is valid only after the module is restarted.

- Read Command: `AT+QCFG="gprsattach"`

  Response:

  ```at
  +QCFG: "gprsattach",<attachmode>

  OK
  ```

- Write Command: `AT+QCFG="gprsattach",<attachmode>`

  Response: `OK` or `ERROR`

  If there is any error related to ME functionality:

  ```at
  +CME ERROR: <err>
  ```

Parameter:

- **\<attachmode>** - Number format, the mode to attach GPRS when UE is powered on

  ```csv
  Value,Meaning
  0,Manual attach
  1,Auto attach (By default)
  ```

### `AT+QCFG="nwscanmode"` Network Search Mode Configuration {#atqcfg-nwscanmode}

The command specifies the network mode to be searched.

If **\<effect>** is omitted, the configuration will take effect immediately.

- Read Command: `AT+QCFG="nwscanmode"`

  Response:

  ```at
  +QCFG: "nwscanmode",<scanmode>

  OK
  ```

- Write Command: `AT+QCFG="nwscanmode",<scanmode>[,<effect>]`

  Response: `OK` or `ERROR`

  If there is any error related to ME functionality:

  ```at
  +CME ERROR: <err>
  ```

Parameter:

- **\<scanmode>** - Number format, network mode to be searched

  ```csv
  Value,Meaning
  0,AUTO (By default)
  1,GSM only
  2,WCDMA only
  3,LTE only
  4,TD-SCDMA only
  5,UMTS only
  6,CDMA only
  7,HDR only
  8,CDMA and HDR only
  ```

- **\<effect>** - Number format, When to take effect

  ```csv
  Value,Meaning
  0,Take effect after UE reboots
  1,Take effect immediately (By default)
  ```

### `AT+QCFG="nwscanseq"` Network Searching Sequence Configuration {#atqcfg-nwscanseq}

The command specifies the sequence of searching network.

This configuration is valid only after the module is restarted.

- Read Command: `AT+QCFG="nwscanseq"`

  Response:

  ```at
  +QCFG: "nwscanseq",<scanseq>

  OK
  ```

- Write Command: `AT+QCFG="nwscanseq",<scanseq>`

  Response: `OK` or `ERROR`

  If there is any error related to ME functionality:

  ```at
  +CME ERROR: <err>
  ```

Parameter:

- **\<scanseq>** - Number format, Network searching sequence

  e.g.: `04030201` (LTE/WCDMA/TD-SCDMA/GSM)

  ```csv
  Value,Meaning
  00,Automatic (LTE/ WCDMA/TD-SCDMA/GSM)
  01,GSM
  02,TD-SCDMA
  03,WCDMA
  04,LTE
  05,CDMA
  ```

### `AT+QCFG="roamservice"` Roam Service Configuration {#atqcfg-roamservice}

The command is used to enable or disable the roam service.

If **\<effect>** is omitted, the configuration will take effect immediately.

- Read Command: `AT+QCFG="roamservice"`

  Response:

  ```at
  +QCFG: "roamservice",<roammode>

  OK
  ```

- Write Command: `AT+QCFG="roamservice",<roammode>[,<effect>]`

  Response: `OK` or `ERROR`

  If there is any error related to ME functionality:

  ```at
  +CME ERROR: <err>
  ```

Parameter:

- **\<roammode>** - Number format, The mode of roam service

  ```csv
  Value,Meaning
  1,Disable roam service
  2,Enable roam service
  255,AUTO (By default)
  ```

### `AT+QCFG="servicedomain"` Service Domain Configuration {#atqcfg-servicedomain}

The command specifies the registered service domain.

If **\<effect>** is omitted, the configuration will take effect immediately.

- Read Command: `AT+QCFG="servicedomain"`

  Response:

  ```at
  +QCFG: "servicedomain",<service>

  OK
  ```

- Write Command: `AT+QCFG="servicedomain",<service>[,<effect>]`

  Response: `OK` or `ERROR`

  If there is any error related to ME functionality:

  ```at
  +CME ERROR: <err>
  ```

Parameter:

- **\<service>** - Service domain of UE

  ```csv
  Value,Meaning
  0,CS only
  1,PS only
  2,CS & PS
  ```

- **\<effect>** - Number format, When to take effect

  ```csv
  Value,Meaning
  0,Take effect after UE reboots
  1,Take effect immediately (By default)
  ```

### `AT+QCFG="band"` Band Configuration {#atqcfg-band}

The command specifies the preferred frequency bands to be searched of UE.

If **\<effect>** is omitted, the configuration will take effect immediately.

- Read Command: `AT+QCFG="band"`

  Response:

  ```at
  +QCFG: "band",<bandval>,<ltebandval>,<tdsbandval>

  OK
  ```

- Write Command: `AT+QCFG="band",<bandval>,<ltebandval>,<tdsbandval>[,<effect>]`

  Response: `OK` or `ERROR`

  If there is any error related to ME functionality:

  ```at
  +CME ERROR: <err>
  ```

Parameter:

- **\<bandval>** - A hexadecimal value that specifies the GSM and WCDMA frequency bands.

  If it is set to 0, it means not to change GSM and WCDMA frequency bands.

  e.g.: `0x0013 = 0x0001 (GSM900) + 0x0002 (GSM1800) + 0x0010 (WCDMA 2100)`

  ```csv
  Value,Meaning
  0x0000,No change
  0x0001,GSM 900
  0x0002,GSM 1800
  0x0004,GSM 850
  0x0008,GSM 1900
  0x0010,WCDMA 2100
  0x0020,WCDMA 1900
  0x0040,WCDMA 850
  0x0080,WCDMA 900
  0x0100,WCDMA 800
  0x0200,WCDMA 1700
  0xFFFF,Any frequency band
  ```

- **\<ltebandval>** - A hexadecimal value that specifies the LTE frequency band.

  If it is set to `0` or `0x40000000`, it means not to change LTE frequency band.

  e.g.: `0x15 = 0x01 (LTE B1) + 0x04 (LTE B3) + 0x10 (LTE B5)`

  ```csv
  Value,Meaning
  0x01,LTE B1
  0x04,LTE B3
  0x10,LTE B5
  0x40,LTE B7
  0x80,LTE B8
  0x80000,LTE B20
  0x7FFFFFFFFFFFFFFF,Any frequency band
  ```

- **\<tdsbandval>** - A hexadecimal value that specifies the TD-SCDMA frequency band.

  If it is set to `0` or `0x40000000`, it means not to change LTE frequency band.

  e.g.: `0x21 = 0x01 (TDS BCA) + 0x20 (TDS BCF)`

  ```csv
  Value,Meaning
  0x01,TDS BCA (TD-SCDMA Band A)
  0x02,TDS BCB (TD-SCDMA Band B)
  0x04,TDS BCC (TD-SCDMA Band C)
  0x08,TDS BCD (TD-SCDMA Band D)
  0x10,TDS BCE (TD-SCDMA Band E)
  0x20,TDS BCF (TD-SCDMA Band F)
  ```

- **\<effect>** - Number format, When to take effect

  ```csv
  Value,Meaning
  0,Take effect after UE reboots
  1,Take effect immediately (By default)
  ```

### `AT+QCFG="hsdpacat"` HSDPA Category Configuration {#atqcfg-hsdpacat}

The command specifies the [HSDPA](https://en.wikipedia.org/wiki/HSDPA) category.

This configuration is valid only after the module is restarted.

- Read Command: `AT+QCFG="hsdpacat"`

  Response:

  ```at
  +QCFG: "hsdpacat",<cat>

  OK
  ```

- Write Command: `AT+QCFG="hsdpacat",<cat>`

  Response: `OK` or `ERROR`

  If there is any error related to ME functionality:

  ```at
  +CME ERROR: <err>
  ```

Parameter:

- **\<cat>** - HSDPA category

  ```csv
  Category,Meaning
  6,Category 6
  8,Category 8
  10,Category 10
  12,Category 12
  14,Category 14
  18,Category 18
  20,Category 20
  24,Category 24 (By default)
  ```

### `AT+QCFG="hsupacat"` HSUPA Category Configuration {#atqcfg-hsupacat}

The command specifies the [HSUPA](https://en.wikipedia.org/wiki/HSUPA) category.

This configuration is valid only after the module is restarted.

- Read Command: `AT+QCFG="hsupacat"`

  Response:

  ```at
  +QCFG: "hsupacat",<cat>

  OK
  ```

- Write Command: `AT+QCFG="hsupacat",<cat>`

  Response: `OK` or `ERROR`

  If there is any error related to ME functionality:

  ```at
  +CME ERROR: <err>
  ```

Parameter:

- **\<cat>** - HSUPA category

  ```csv
  Category,Meaning
  5,Category 5
  6,Category 6 (By default)
  ```

### `AT+QCFG="rrc"` RRC Release Version Configuration {#atqcfg-rrc}

The command specifies the RRC release version.

This configuration is valid only after the module is restarted.

- Read Command: `AT+QCFG="rrc"`

  Response:

  ```at
  +QCFG: "rrc",<rrcr>

  OK
  ```

- Write Command: `AT+QCFG="rrc",<rrcr>`

  Response: `OK` or `ERROR`

  If there is any error related to ME functionality:

  ```at
  +CME ERROR: <err>
  ```

Parameter:

- **\<rrcr>** - RRC release version.

  ```csv
  Value,Version
  0,R99
  1,R5
  2,R6
  3,R7
  4,R8 (By default)
  ```

### `AT+QCFG="sgsn"` UE SGSN Release Version Configuration {#atqcfg-sgsn}

The command specifies the UE SGSN release version.

This configuration is valid only after the module is restarted.

- Read Command: `AT+QCFG="rrc"`

  Response:

  ```at
  +QCFG: "sgsn",<sgsnr>

  OK
  ```

- Write Command: `AT+QCFG="sgsn",<sgsnr>`

  Response: `OK` or `ERROR`

  If there is any error related to ME functionality:

  ```at
  +CME ERROR: <err>
  ```

Parameter:

- **\<sgsnr>** - SGSN release version.

  ```csv
  Value,Version
  0,R97
  1,R99
  2,Dynamic (By default)
  ```

### `AT+QCFG="msc"` UE MSC Release Version Configuration {#atqcfg-msc}

The command specifies the UE MSC release version.

This configuration is valid only after the module is restarted.

- Read Command: `AT+QCFG="msc"`

  Response:

  ```at
  +QCFG: "msc",<mscr>

  OK
  ```

- Write Command: `AT+QCFG="msc",<mscr>`

  Response: `OK` or `ERROR`

  If there is any error related to ME functionality:

  ```at
  +CME ERROR: <err>
  ```

Parameter:

- **\<mscr>** - MSC release version.

  ```csv
  Value,Version
  0,R97
  1,R99
  2,Dynamic (By default)
  ```

### `AT+QCFG="pdp/duplicatechk"` Establish Multi PDNs with the Same APN {#atqcfg-pdf-duplicatechk}

The command allows/refuses establishing multi PDNs with the same APN profile.

The configuration will take effect immediately.

- Read Command: `AT+QCFG="pdp/duplicatechk"`

  Response:

  ```at
  +QCFG: "pdp/duplicatechk",<enable>

  OK
  ```

- Write Command: `AT+QCFG="pdp/duplicatechk",<enable>`

Parameter:

- **\<enable>** - Establish multi PDNs with the same APN profile

  ```csv
  Value,Meaning
  0,Refused
  1,Allowed
  ```

### `AT+QCFG="tdscsq"` Set TD-SCDMA RSSI range {#atqcfg-tdscsq}

The command is used to set RSSI range in TD-SCDMA.

The configuration will take effect immediately.

{{< hint warning >}}

This command is valid only in TD-SCDMA.

Show the RSSI value by **AT+CSQ** and get RSSI details by **AT+CSQ**.

{{< /hint >}}

- Read Command: `AT+QCFG="tdscsq"`

  Response:

  ```at
  +QCFG: "tdscsq",<value>

  OK
  ```

- Write Command: `AT+QCFG="tdscsq",<value>`

  Response: `OK` or `ERROR`

  If there is any error related to ME functionality:

  ```at
  +CME ERROR: <err>
  ```

Parameter:

- **\<value>** - RSSI between

  ```csv
  Value,Meaning
  0,RSSI between 0-31 (By default)
  1,RSSI between 100-191
  ```

### `AT+QCFG="urc/ri/ring"` RI behavior when RING URC is Presented {#atqcfg-urc-ri-ring}

**AT+QCFG="urc/ri/ring"**, **AT+QCFG="urc/ri/smsincoming"** and **AT+QCFG="urc/ri/other"** control the RI
(ring indicator) behavior when a [URC]({{< ref "urc" >}}) is reported.

These configurations will be stored into NV automatically.

The ring indicator is active low.

**AT+QCFG="urc/ri/ring"** specifies the RI behavior when URC **RING** is presented to indicate an incoming call.

The sum of parameter **\<activeduration>** and **\<inactiveduration>** determines the interval time of **RING** indications when a call is coming.

- Read Command: `AT+QCFG="urc/ri/ring"`

  Response:

  ```at
  +QCFG: "urc/ri/ring",<typeri>,<pulseduration>,<activeduration>,<inactiveduration>,<ringnodisturbing>,<pulsecount>

  OK
  ```

- Write Command: `AT+QCFG="urc/ri/ring",<typeri>`

  Overloads:

  ```at
  AT+QCFG="urc/ri/ring","off"
  AT+QCFG="urc/ri/ring","pulse"[,<pulseduration>[,<ringnodisturbing>]]]
  AT+QCFG="urc/ri/ring","always"
  AT+QCFG="urc/ri/ring","auto"[,<ringnodisturbing>]
  AT+QCFG="urc/ri/ring","wave"[,<activeduration>[,<inactiveduration>[,<ringnodisturbing>]]]]
  ```

  Response: `OK` or `ERROR`

  If there is any error related to ME functionality:

  ```at
  +CME ERROR: <err>
  ```

Parameter:

- **\<typeri>** - RI behavior when URCs are presented

  - `"off"`

    No change.

    Ring indicator keeps inactive.

  - `"pulse"` (By default)

    Pulse width determined by **\<pulseduration>**.

  - `"always"`

    Change to active.

    RI behavior can be restored to inactive by **AT+QRIR**.

  - `"auto"`

    When **RING** is presented to indicate an incoming call.

    The ring indicator changes to and keeps active.

    When ring of the incoming call ends, either answering or hanging up the incoming call, the ring indicator will change to inactive.

  - `"wave"`

    When **RING** is presented to indicate an incoming call.

    The ring indicator outputs a square wave.

    Both **\<activeduration>** and **\<inactiveduration>** are used to set parameters of the square wave.

    When the ring of incoming call ends, either answering or hanging up the incoming call, the ring indicator will change to inactive.

- **\<pulseduration>** - The width of pulse.

  The value ranges from 1 to 2000ms and the default is _120ms_.

  This parameter is only meaningful when **\<typeri>** is `"pulse"`.

  If this parameter is not needed, it can set it as null.

- **\<activeduration>** - The active duration of the square wave.

  The value ranges from 1 to 10000ms, and the default is _1000ms_.

  This parameter is only meaningful when **\<typeri>** is `"wave"`.

- **\<inactiveduration>** - The inactive duration of the square wave.

  The value ranges from 1 to 10000ms, and the default is _5000ms_.

  This parameter is only meaningful when **\<typeri>** is `"wave"`.

- **\<ringnodisturbing>** - Set whether the ring indicator behavior could be disturbed.

  This parameter is only meaningful when **\<typeri>** is configured to `"auto"` or `"wave"`.

  For example, when **\<typeri>** is configured to `"wave"`, if the square wave needs not to be disturbed by other URCs (including SMS related URCs), then **\<ringnodisturbing>** should be set to `"on"`.

- **\<pulsecount>** - The count of pulse.

  This parameter is only meaningful when **\<typeri>** is `"pulse"`.

  The value ranges from 1 to 5 and the default is _1_.

  The interval time between two pulses is equal to **\<pulseduration>**.

### `AT+QCFG="urc/ri/smsincoming"` RI behavior when incoming SMS URCs are presente {#atqcfg-urc-ri-smsincoming}

The command specifies the RI (ring indicator) behavior when related incoming message URCs are presented.

Incoming message [URCs]({{< ref "urc" >}}) include **+CMTI**, **+CMT**, **+CDS** and **+CBM**.

- Read Command: `AT+QCFG="urc/ri/smsincoming"`

  Response:

  ```at
  +QCFG: "urc/ri/smsincoming",<typeri>,<pulseduration>,<pulsecount>

  OK
  ```

- Write Command: `AT+QCFG="urc/ri/smsincoming",<typeri>[,<pulseduration>]`

  Response: `OK` or `ERROR`

  If there is any error related to ME functionality:

  ```at
  +CME ERROR: <err>
  ```

Parameter:

- **\<typeri>** - RI behavior when URCs are presented

  - `"off"`

    No change.

    Ring indicator keeps inactive.

  - `"pulse"` (By default)

    Pulse width determined by **\<pulseduration>**.

  - `"always"`

    Change to active.

    RI behavior can be restored to inactive by **AT+QRIR**.

- **\<pulseduration>** - The width of pulse.

  The value ranges from 1 to 2000ms and the default is _120ms_.

  This parameter is only valid when **\<typeri>** is **"pulse"**.

- **\<pulsecount>** - The count of pulse.

  This parameter is only meaningful when **\<typeri>** is **"pulse"**.

  Value ranges from 1 to 5 and the default is _1_.

  The interval time between two pulses is equal to **\<pulseduration>**.

### `AT+QCFG="urc/ri/other"` RI behavior when other URCs are Presented {#atqcfg-urc-ri-other}

The command specifies the RI (ring indicator) behavior when other [URCs]({{< ref "urc" >}}) are presented.

- Read Command: `AT+QCFG="urc/ri/other"`

  Response:

  ```at
  +QCFG: "urc/ri/other",<typeri>,<pulseduration>,<pulsecount>

  OK
  ```

- Write Command: `AT+QCFG="urc/ri/other",<typeri>[,<pulseduration>]`

  Response: `OK` or `ERROR`

  If there is any error related to ME functionality:

  ```at
  +CME ERROR: <err>
  ```

Parameter:

- **\<typeri>** - RI behavior when URCs are presented

  - `"off"`

    No change.

    Ring indicator keeps inactive.

  - `"pulse"` (By default)

    Pulse width determined by **\<pulseduration>**.

- **\<pulseduration>** - The width of pulse.

  The value ranges from 1 to 2000ms and the default is _120ms_.

  This parameter is only valid when **\<typeri>** is **"pulse"**.

- **\<pulsecount>** - The count of pulse.

  This parameter is only meaningful when **\<typeri>** is **"pulse"**.

  Value ranges from 1 to 5 and the default is _1_.

  The interval time between two pulses is equal to **\<pulseduration>**.

### `AT+QCFG="risignaltype"` RI signal output carrier {#atqcfg-risignaltype}

The command specifies the RI (ring indicator) signal output carrier.

- Read Command: `AT+QCFG="risignaltype"`

  Response:

  ```at
  +QCFG: "risignaltype",<risignatype>

  OK
  ```

- Write Command: `AT+QCFG="risignaltype",[<risignatype>]`

  Response: `OK` or `ERROR`

  If there is any error related to ME functionality:

  ```at
  +CME ERROR: <err>
  ```

Parameter:

- **\<risignaltype>** - RI signal output carrier.

  - `"respective"`

    The ring indicator behaves on the port where URC is presented.

    For example, if a URC is presented on **UART port**,
    it is physical ring indicator.

    If the URC is presented on **USB port**,
    it is virtual ring indicator.

    If the URC is presented on **USB AT port**,
    and the port does not support ring indicator,
    then there will be no ring indicator.

    **AT+QURCCFG="urcport"** can get the port on which the URC is presented.

  - `"physical"`

    No matter which port the URC is presented on.

    URC only causes the behavior of physical ring indicator.

### `AT+QCFG="urc/delay"` Delay URC indication {#atqcfg-urc-delay}

The command can delay the output of URC indication until ring indicator pulse ends.

- Read Command: `AT+QCFG="urc/delay"`

  Response:

  ```at
  +QCFG: "urc/delay",<enable>

  OK
  ```

- Write Command: `AT+QCFG="urc/delay",<enable>`

  Response: `OK` or `ERROR`

  If there is any error related to ME functionality:

  ```at
  +CME ERROR: <err>
  ```

Parameter:

- **\<enable>** - RI signal output carrier.

  - 0 - URC indication will be outputted when ring indicator pulse starts

  - 1 - URC indication will be outputted when ring indicator pulse ends

    Only effective when the type of ring indicator is `"pulse"`.

    Please refer to **AT+QCFG="urc/ri/ring"**, **AT+QCFG="urc/ri/smsincoming"** and **AT+QCFG="urc/ri/other"** for more details.

### `AT+QCFG="urc/cache"` URC cache function {#atqcfg-urc-cache}

{{< hint warning >}}

The settings of the command will take effect immediately, and will be saved after power off.

{{< /hint >}}

- Read Command: `AT+QCFG="urc/cache"`

  Response:

  ```at
  +QCFG: "urc/cache",<enable>

  OK
  ```

- Write Command: `AT+QCFG="urc/cache",<enable>`

  Response: `OK` or `ERROR`

  If there is any error related to ME functionality:

  ```at
  +CME ERROR: <err>
  ```

Parameter:

- **\<enable>** - URC cache

  ```csv
  Value,Meaning
  0,Disable URC cache
  1,Enable URC cache
  ```

Example:

```at
AT+QCFG="urc/cache"
+QCFG: "urc/cache",0 // Disable URC cache

OK
AT+QCFG="urc/cache",1 // Enable URC cache
OK
AT+QCFG="urc/cache" // Make a call and send two messages to the module
+QCFG: "urc/cache",1

OK
AT+QCFG="urc/cache",0 // Disable URC cache
OK
RING          // Output cached URC
NO CARRIER    // Output cached URC
+CMTI: "ME",0 // Output cached URC
+CMTI: "ME",1 // Output cached URC
AT+QCFG="urc/cache"
+QCFG: "urc/cache",0 // Disable URC cache
OK
```

### `AT+QCFG="tone/incoming"` Ring tone function {#atqcfg-tone-incoming}

{{< hint warning >}}

The settings of the command will take effect immediately, and will be saved after power off.

{{< /hint >}}

- Read Command: `AT+QCFG="tone/incoming"`

  Response:

  ```at
  +QCFG: "tone/incoming",<enable>

  OK
  ```

- Write Command: `AT+QCFG="tone/incoming",<enable>`

  Response: `OK` or `ERROR`

  If there is any error related to ME functionality:

  ```at
  +CME ERROR: <err>
  ```

Parameter:

- **\<enable>** - Ring tone

  ```csv
  Value,Meaning
  0,Disable Ring tone
  1,Enable NOKIA Ring tone
  2,Enable Ring tone
  ```

Example:

```at
AT+QCFG="tone/incoming"
+QCFG: "tone/incoming",0 // Ring tone function is disabled

OK
AT+QCFG="tone/incoming",1 // Enable NOKIA Ring tone

OK
AT+QCFG="tone/incoming"
+QCFG: "tone/incoming",1

OK
```

## `AT+QINDCFG` URC indication Configuration {#atqindcfg}

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

- Write Command: `AT+QINDCFG=<urctype>[,<enable>[,<savetonvram>]]`

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
  Value,Meaning
  0,OFF
  1,ON
  ```

- **\<savetonvram>** - Whether to save configuration into NV.

  ```csv
  Value,Meaning
  0,Not save (By default)
  1,Save
  ```
