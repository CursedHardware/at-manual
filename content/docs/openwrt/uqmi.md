---
title: uQMI
weight: 1
---

<!-- cspell:ignore uqmi -->

OpenWrt Tiny QMI command line utility

URL: <https://git.openwrt.org/project/uqmi.git>

User Guide: <https://openwrt.org/docs/guide-user/network/wan/wwan/ltedongle>

---

## Tricks

```bash
# Read signal strength
uqmi -d /dev/cdc-wdm0 --get-signal-info
# Read registered network
uqmi -d /dev/cdc-wdm0 --get-serving-system
# Check is connected data plane
uqmi -d /dev/cdc-wdm0 --get-data-status
# Read IP and DNS information
uqmi -d /dev/cdc-wdm0 --get-current-settings
# Reboot module
uqmi -d /dev/cdc-wdm0 --set-device-operating-mode reset
```
