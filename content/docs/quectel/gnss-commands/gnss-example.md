---
title: Example
slug: example
weight: 3
---

## Turn On and Off the GNSS Engine {#gnss-power}

The example uses default arguments to start GNSS engine,
after turning on GNSS engine,
NMEA sentences will be outputted from "usbnmea" port by default.

```at
AT+QGPS=1 // Turn on GNSS engine. OK
// After turning on GNSS engine, NMEA sentences will be outputted from "usbnmea" port by default.
AT+QGPSLOC? // Obtain position information.
+QGPSLOC: 061951.0,3150.7223N,11711.9293E,0.7,62.2,2,0.0,0.0,0.0,110513,09

OK
AT+QGPSEND // Turn off GNSS engine.
OK
```

## Application of GNSS nmeasrc {#nmeasrc}

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

## Example of Injecting gpsOneXTRA {#inject-xtra}

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
