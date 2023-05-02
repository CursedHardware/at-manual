---
title: Tricks
weight: 1000
---

## Lock Band

see [`AT+QCFG="band"`]({{< ref "status-commands#atqcfg-band" >}})

## Lock Network

see [`AT+QCFG="nwscanmode"`]({{< ref "status-commands#atqcfg-nwscanmode" >}})

## Lock Cells

```at
AT+QNWLOCK="common/lte" # Read
AT+QNWLOCK="common/lte",0 # Unlock
AT+QNWLOCK="common/lte",1,earfcn,0 # Lock EARFCN
AT+QNWLOCK="common/lte",2,earfcn,pci,0 # Lock Cell
```

## USB mode

```at
AT+QCFG="usbnet",0 # RMNET, QMI
AT+QCFG="usbnet",1 # ECM
AT+QCFG="usbnet",2 # MBIM
AT+QCFG="usbnet",3 # RNDIS
```

## Modify IMEI

see [AT+EGMR]({{< ref "unspecific-commands#ategmr" >}})
