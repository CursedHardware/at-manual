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
  +QCFG: "pdp/duplicatechk",(list of supported <enable>s) +QCFG: "tdscsq",(list of supported <value>s)
  +QCFG: "urc/ri/ring",(list of supported <typeri>s),(list of supported <pulseduration>s),(list of supported <activeduration>s),(list of supported <inactiveduration>s),(list of supported <ringnodisturbing>s)
  +QCFG: "urc/ri/smsincoming",(list of supported <typeri>s),(list of supported <pulseduration>s)
  +QCFG: "urc/ri/other",(list of supported <typeri>s),(list of supported <pulseduration>s)
  +QCFG: "risignaltype",(list of supported <risignatype>s)
  +QCFG: "urc/cache",(list of supported <value>s)
  +QCFG: "tone/incoming",(list of supported <value>s)

  OK
  ```

### `AT+QCFG="gprsattach"` (GPRS Attach Mode Configuration) {#atqcfg-gprsattach}

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

- **\<attachmode>** - Number format, the mode to attach GRPS when UE is powered on

  ```csv
  Value,Note
  0,Manual attach
  1,Auto attach (by default)
  ```

### `AT+QCFG="nwscanmode"` (Network Search Mode Configuration) {#atqcfg-nwscanmode}

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
  Value,Note
  0,AUTO (by default)
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
  Value,Note
  0,Take effect after UE reboots
  1,Take effect immediately
  ```

### `AT+QCFG="nwscanseq"` (Network Searching Sequence Configuration) {#atqcfg-nwscanseq}

The command specifies the sequence of searching network.

This configuration is valid only after the module is restarted.

- Read Command: `AT+QCFG="nwscanseq"`

  Response:

  ```at
  +QCFG: "nwscanseq",<scanseq>

  OK
  ```

- Write Command:

  Response: `OK` or `ERROR`

  If there is any error related to ME functionality:

  ```at
  +CME ERROR: <err>
  ```

Parameter:

- **\<scanseq>** - Number format, Network searching sequence

  (e.g.: `04030201` (LTE/WCDMA/TD-SCDMA/GSM))

  ```csv
  Value,Note
  00,Automatic (LTE/ WCDMA/TD-SCDMA/GSM)
  01,GSM
  02,TD-SCDMA
  03,WCDMA
  04,LTE
  05,CDMA
  ```

### AT+QCFG="roamservice" (Roam Service Configuration) {#atqcfg-roamservice}

### AT+QCFG="servicedomain" (Service Domain Configuration) {#atqcfg-servicedomain}

### AT+QCFG="band" (Band Configuration) {#atqcfg-band}

### AT+QCFG="hsdpacat" (HSDPA Category Configuration) {#atqcfg-hsdpacat}

### AT+QCFG="hsupacat" (HSUPA Category Configuration) {#atqcfg-hsupacat}

### AT+QCFG="rrc" (RRC Release Version Configuration) {#atqcfg-rrc}

### AT+QCFG="sgsn" (UE SGSN Release Version Configuration) {#atqcfg-sgsn}

### AT+QCFG="msc" (UE MSC Release Version Configuration) {#atqcfg-msc}

### AT+QCFG="PDP/duplicatechk" (Establish Multi PDNs with the Same APN) {#atqcfg-pdf-duplicatechk}

### AT+QCFG="tdscsq" (Set TD-SCDMA RSSI Range) {#atqcfg-tdscsq}

### AT+QCFG="urc/ri/ring" (RI Behavior When RING URC is Presented) {#atqcfg-urc-ri-ring}

### AT+QCFG="urc/ri/smsincoming" (RI Behavior When Incoming SMS URCs are Presente) {#atqcfg-urc-ri-smsincoming}

### AT+QCFG="urc/ri/other" (RI Behavior When Other URCs are Presented) {#atqcfg-urc-ri-other}

### AT+QCFG="risignaltype" (RI Signal Output Carrier) {#atqcfg-risignaltype}

### AT+QCFG="urc/delay" (Delay URC Indication) {#atqcfg-urc-delay}

### AT+QCFG="urc/cache" (URC Cache Function) {#atqcfg-urc-cache}

### AT+QCFG="tone/incoming" (Ring Tone Function) {#atqcfg-tone-incoming}

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
