---
title: GNSS Commands
---

## Introduction

GNSS engine is high-performance and suitable for various applications which lowest-cost and accurate positioning are needed.

Meanwhile, it can also support position tracking without network assistance, and GNSS capabilities when GSM/WCDMA is out of network coverage areas.

GNSS can be applied in the following occasions:

- turn-by-turn navigation applications
- asset tracking
- buddy tracking
- location-aware games
- homing
- fleet management

### How to Use GNSS

GNSS engine allows calculating location without any assistance from the network.

The procedure of turning on GNSS is shown as below:

- Step 1: Configure corresponding demands by **AT+QGPSCFG**.
- Step 2: Active GNSS engine by **AT+QGPS**.
- Step 3: After GNSS session is started successfully and GNSS has fixed,
  positioning information can be obtained by three ways:

  1. NMEA sentences output to `"usbnmea"` port by default, you can read the port to obtain NMEA sentences.
  1. You can use **AT+QGPSLOC** to obtain some positioning information directly,
     such as latitude, longitude, height, time and positioning type and soon.
  1. After enabling **\<nmeasrc>** by **AT+QGPSCFG**, you can acquire the specificed NMEA sentence by **AT+QGPSGNMEA**.
     If **\<nmeasrc>** is disabled, this command cannot be used.

- Step 4: You can terminate GNSS by two-ways:

  1. If the parameter **\<fixcount>** of the **AT+QGPS** is set to 0 in **Step 2**,
     GNSS engine will get position continuously, and it can be ended by **AT+QGPSEND**.
  1. If the actual fix times reach to the specified **\*<fixcount>** value,
     the engine will stop automatically;
     in the process you can use the command **AT+QGPSEND** to end the session.

### NMEA Sentences Type

The NMEA sentences are compatible with [NMEA-0183](https://en.wikipedia.org/wiki/NMEA_0183) protocol, and all of the standard NMEA sentences have two kinds of prefix.

for GPS sentences, the prefix is "GP", as below:

- GPGGA - Global Positioning System Fix Data, Time, Position and related fix data
- GPRMC - Recommended minimum data
- GPGSV - Detailed satellite data
- GPGSA - Overall satellite data
- GPVTG - Vector track and speed over the ground

And for GLONASS sentences, the prefixes are "GL" and "GN", as below:

- GLGSV - Detailed satellite data
- GNGSA - Overall satellite data
- GNGNS - Positioning System

### Introduction of _gpsOneXTRA_

_gpsOneXTRA_ assistance enhances standalone performance, and simplifies GNSS assistance delivery to GNSS engine, including ephemeris, almanac, ionosphere, UTC, health and coarse time assistance.

After booting _gpsOneXTRA_, TTFF (Time to First Fix) can be reduced by 18 to 30 sec (or more in harsh signal environments).

And the _gpsOneXTRA_ data needs to be updated once per day (or every a couple of days) which is obtained from an XTRA server on the network.

In order to use _gpsOneXTRA_ feature, you should ensure that valid _gpsOneXTRA_ assistance data is available.

Firstly download a new _gpsOneXTRA_ binary file from one of the _gpsOneXTRA_ assistance web servers via HTTP.

The files are named as _xtra.bin_ for GPS only and _xtra2.bin_ for **GPS+GLONASS**.

The exact file size should be less than 50kB:

- <http://xtra1.gpsonextra.net/xtra.bin> <http://xtra1.gpsonextra.net/xtra2.bin>
- <http://xtra2.gpsonextra.net/xtra.bin> <http://xtra2.gpsonextra.net/xtra2.bin>
- <http://xtra3.gpsonextra.net/xtra.bin> <http://xtra3.gpsonextra.net/xtra2.bin>

_gpsOneXTRA_ data needs to be updated regularly.

You can query the _gpsOneXTRA_ data status by **AT+QGPSXTRADATA?** to update _gpsOneXTRA_ data properly.

The working procedure of _gpsOneXTRA_ is shown as follows:

- Step 1: If _gpsOneXTRA_ is disabled, enable it by **AT+QGPSXTRA** and restart the module.
- Step 2: Confirm the current validity of _gpsOneXTRA_ data by **AT+QGPSXTRADATA?**.
- Step 3: Download _xtra.bin_ or _xtra2.bin_ to the module via HTTP AT command.
- Step 4: Inject the correct time by **AT+QGPSXTRATIME**.
- Step 5: Inject the downloaded _xtra.bin_ or _xtra2.bin_ file by **AT+QGPSXTRADATA**.
- Step 6: Others steps see [How to Use GNSS](#how-to-use-gnss).

### GNSS Power Saving Management {#low-power}

GNSS engine provides power saving solutions by DPO and ODP, thus extending battery life, maximizing talk and standby time, and enhancing accuracy and TTFF.

#### DPO (Dynamic Power Optimization) {#dpo}

DPO (Dynamic Power Optimization) is a power-saving solution which attempts to turn off GNSS RF and other unneeded components.

DPO takes effect after configuring **\<dpoenable>** via **AT+QGPSCFG**.

There are several preconditions to turn on the DPO, shown as below:

- All SVs > 26dB-Hz must have ephemeris or recent (< 3.5 days) XTRA almanac corrections for those SVs.

- Health or UTC information is not transmitted over-the-air.

- Valid position and HEPE should be less than 50m and within user's specified value in QoS.

- 6 SVs > 37dB-Hz or 4 SVs > 26dB-Hz and have almanac and health for all SVs.

Benefits and impacts of DPO:

- When the DPO feature is on and the SV or navigational data cannot be decoded,

  the GPS receiver will not be continuous.

- During the DPO, the SBAS feature is effectively disabled.

  The receiver cannot demodulate the SBAS messages.

  DPO always takes precedence over SBAS.

- TTFF and yield will not be impacted.

#### ODP (On-Demand Positioning) {#odp}

When On-Demand Positioning (ODP) is enabled, standalone GNSS positioning will be triggered in the background.

The positions calculated as a result of ODP are not presented to the application, NMEA, or the network.

However, when the on-demand session is operating and the users or network request a GNSS session, the on-demand session is immediately terminated and the incoming request is implemented.

ODP system requirements:

1. ODP requires valid gpsOneXTRA assistance data.
1. ODP requires that EC20 is in service.

If these two requirements are not fulfilled ODP will be turned off automatically. And ODP will be suspended if a regular GNSS fix is running.

In the enabled low power mode, the GNSS engine is turned on to consume low power.

Requests to determine the GNSS position are returned with a reduced time-to-fix while this mode is active.

In the enabled Ready mode, the GNSS engine is kept active and is available to perform fixed position.

Requests to determine the GNSS position are immediately returned while this mode is active.

The battery will be greatly impacted in this mode.

Maintenance of position and time uncertainty also improves the performance of E911 on UMTS.

Configure **\<odpcontrol>** to set two different modes by AT+QGPSCFG:

**Low power mode**:

- Low-frequency background GNSS tracking session.
- In good signal condition, use shorter interval with frequent ODP session (i.e., per 5 min).
- In weak signal condition, use longer interval, but less frequent ODP session (i.e., twice per hour).

**Ready mode**:

- GNSS engine will start 1 Hz positioning session.
- Main goal is to keep GNSS engine ready so that when the application demands a position from the
  GNSS engine, position can be reported quickly.

## Description of AT Commands {#at-commands}

<!--
2 Description of AT Command
2.1. AT+QGPSCFG Configure GNSS
2.2. AT+QGPSDEL Delete Assistance Data
2.3. AT+QGPS Operate GPS Session
2.4. AT+QGPSEND Terminate GNSS Session
2.5. AT+QGPSLOC Obtain Position
2.6. AT+QGPSGNMEA Obtain NMEA Sentences
2.7. AT+QGPSXTRA Enable gpsOneXTRA Functionality
2.8. AT+QGPSXTRATIME InjectgpsOneXTRATime
2.9. AT+QGPSXTRADATA Inject gpsOneXTRA Data Manually
2.10. Introduction of URC
2.10.1. Expired XTRA Data
-->

## Example

### Turn On and Off the GNSS Engine {#gnss-power}

The example uses default arguments to start GNSS engine, after turning on GNSS engine, NMEA sentences will be outputted from "usbnmea" port by default.

```at
AT+QGPS=1 // Turn on GNSS engine. OK
// After turning on GNSS engine, NMEA sentences will be outputted from "usbnmea" port by default.
AT+QGPSLOC? // Obtain position information.
+QGPSLOC: 061951.0,3150.7223N,11711.9293E,0.7,62.2,2,0.0,0.0,0.0,110513,09

OK
AT+QGPSEND // Turn off GNSS engine.
OK
```

### Application of GNSS nmeasrc {#nmeasrc}

When GNSS was started, you can turn on **\<nmeasrc>** feature, and obtain NMEA sentences by **AT+QGPSGNMEA** directly.

```at
AT+QGPSCFG="nmeasrc",1 // Enable nmeasrc functionality.
OK
AT+QGPSGNMEA="GGA" // Obtain GGA sentence.
+QGPSGNMEA: $GPGGA,103647.0,3150.721154,N,11711.925873,E,1,02,4.7,59.8,M,-2.0,M,,*77

OK
AT+QGPSCFG="nmeasrc",0 // Disable nmeasrc functionality.
OK
AT+QGPSGNMEA="GGA" // Disable nmeasrc functionality, GGA sentence can’t be obtained.
+CME ERROR: 507
```

### Example of Injecting gpsOneXTRA

You must enable gpsOneXTRA before injecting gpsOneXTRA time and data to GNSS engine.

In this example we manually download the XTRA file, then upload to UFS via **AT+QGPSXTRAUPL**.

```at
// If gpsOneXTRA is disabled, enable it by AT+QGPSXTRA and reset EC20, then perform the following procedures.
AT+QGPSXTRA=1 // Enable XTRA. OK
// Restart EC20, enable gpsOneXTRA of GNSS engine.
// If gpsOneXTRA data is invalid (query by AT+QGPSXTRADATA?), then perform the following procedures.
// You can download XTRA file to PC from this URL <http://xtra1.gpsonextra.net/xtra2.bin> or other URL (Refer to the Chapter 1.3).
AT+QFUPL="RAM:xtra2.bin",59748,60
<Select file & send it in QCOM>
OK
// <utc> format is YYYY/MM/DD,hh:mm:ss, e.g. 2015/01/03,15:30:30.
AT+QGPSXTRATIME=0,"2015/01/03,15:30:30",1,1,5 // Inject gpsOneXTRA time to GNSS engine. OK
AT+QGPSXTRADATA="RAM:xtra2.bin" // Inject gpsOneXTRA data to GNSS engine successfully.
OK
AT+QFDEL="RAM:xtra2.bin" // Delete XTRA data file from RAM file
OK
AT+QGPS=1 // Turn on GNSS engine
OK
```

## Appendix A: Terms and Abbreviations

```csv
Abbreviation,Description
GNSS,Global Navigation Satellite Systems
GPS,Global Positioning System provides by USA
GLONASS,Global Navigation Satellite System provides by Russia
NMEA,National Marine Electronics Association
gpsOneXTRA,An auxiliary positioning technology provides by Qualcomm
DPO,Dynamic Power Optimization
ODP,On-Demand Positioning
```

## Appendix B: Summary of Error Codes {#error-codes}

The error code **\<errcode>** indicates an error related to GNSS operations.

The detail about **\<errcode>** is described in the following table.

```csv
Error Code,Meaning
501,Invalid parameter(s)
502,Operation not supported
503,GNSS subsystem busy
504,Session is ongoing
505,Session not activity
506,Operation timeout
507,Function not enabled
508,Time information error
509,XTRA not enabled
510,XTRA file open failed
511,Bad CRC for XTRA data file
512,Validity time is out of range
513,Internal resource error
514,GNSS locked
515,End by E911
516,Not fixed now
549,Unknown error
```