---
title: (U)SIM Related Commands
weight: 4
---

## `AT+QCCID` Show ICCID {#atqccid}

The command returns the ICCID (Integrated Circuit Card Identifier) number of the (U)SIM card.

## `AT+QPINC` Display PIN Remainder Counter {#atqpinc}

The command can query the number of attempts left to enter the password of (U)SIM PIN/PUK.

## `AT+QINISTAT` Query Initialization Status of (U)SIM Card {#atqinistat}

The command is used to query the initialization status of (U)SIM card.

## `AT+QSIMDET` (U)SIM Card Detection {#atqsimdet}

The command enables (U)SIM card hot-swap function. (U)SIM card is detected by GPIO interrupt.

The level of (U)SIM card detection pin should also be set when the (U)SIM card is inserted.

## `AT+QSIMSTAT` (U)SIM Card Insertion Status Report {#atqsimstat}

The command queries (U)SIM card insertion status or determines whether (U)SIM card insertion status report is enabled.

The configuration of this command can be saved by **AT&W**.
