---
title: Serial Interface Control Commands
weight: 2
---

## `AT&C` Set DCD Function Mode {#atc}

The command controls the behavior of the UE's DCD (data carrier detection) line.

- Execution Command: `AT&C[<value>]`

  This parameter determines how the state of circuit 109 (DCD) relates to the detection of received line signal from the distant end.

  Response: `OK`

Parameter:

```csv
Name,Value,Meaning
\<value>,0,DCD function is always ON
,1,DCD function is ON only in the presence of data carrier
```

## `AT&D` Set DTR Function Mode {#atd}

The command determines how the UE responds if DTR line is changed from low to high level during data mode.

- Execution Command: `AT&D[<value>]`

  This parameter determines how the TA responds when circuit 108/2 (DTR) is changed from low to high level during data mode.

  Response: `OK`

Parameter:

```csv
Name,Value,Meaning
\<value>,0,TA ignores status on DTR
,1,"Low->High on DTR:\nChange to command mode\nwhile remaining the connected call."
,2,"Low->High on DTR:\nDisconnect data call, and change to command mode.\nWhen DTR is at high level, auto-answer function is disabled."
```

## `AT+IFC` Set TE-TA Local Data Flow Control {#atifc}

The command determines the flow control behavior of the serial port.

- Test Command: `AT+IFC=?`

  Response:

  ```at
  +IFC: (list of supported <dce_by_dte>s),(list of supported <dte_by_dce>s)

  OK
  ```

- Read Command: `AT+IFC?`

  Response:

  ```at
  +IFC: <dce_by_dte>,<dte_by_dce>

  OK
  ```

- Write Command: `AT+IFC=<dce_by_dte>,<dte_by_dce>`

  This parameter setting determines the data flow control on the serial interface for data mode.

  Response: `OK`

Parameter:

- **\<dce_by_dte>** - Specifies the method that will be used by TE when receiving data from TA

  ```csv
  Value,Meaning
  1,None
  2,RTS flow control
  ```

- **\<dte_by_dce>** - Specifies the method that will be used by TA when receiving data from TE

  ```csv
  Value,Meaning
  1,None
  2,CTS flow control
  ```

{{< hint info >}}

Flow control is only applicable for data mode.

{{< /hint >}}

Example:

```at
AT+IFC=2,2 // Open the hardware flow control
OK
AT+IFC?
+IFC: 2,2

OK
```

## `AT+ICF` Set TE-TA Control Character Framing {#aticf}

The command determines the serial interface character framing format and parity received by TA from TE.

- Test Command: `AT+ICF=?`

  Response:

  ```at
  +ICF: (list of supported <format>s),(list of supported <parity>s)

  OK
  ```

- Read Command: `AT+ICF?`

  Response:

  ```at
  +ICF: <format>,<parity>

  OK
  ```

- Write Command: `AT+ICF=<format>,[<parity>]`

  This parameter setting determines the serial interface character framing format and parity received by TA from TE.

  Response: `OK`

Parameter:

{{< hint info >}}

1. The command is applied for command mode.
1. The **\<parity>** field is ignored if the **\<format>** field specifies no parity.

{{< /hint >}}

```csv
Name,Value,Meaning
\<format>,3,8 data 0 parity 1 stop
\<parity>,0,Odd
,1,Even
,2,Mark (1)
,3,Space (0)
```

## `AT+IPR` Set TE-TA Fixed Local Rate {#atipr}

The command is used to query and set the baud rate of the UART.

The default baud rate value (**\<rate>**) is _115200bps_.

The setting of **\<rate>** will not be restored with AT&F.

- Test Command: `AT+IPR=?`

  Response:

  ```at
  +IPR: (list of supported auto detectable <rate>s),(list of supported fixed-only <rate>s)

  OK
  ```

- Read Command: `AT+IFC?`

  Response:

  ```at
  +IPR: <rate>

  OK
  ```

- Write Command: `AT+IFC=<dce_by_dte>,<dte_by_dce>`

  This parameter setting determines the data rate of the TA on the serial interface.

  After the delivery of any result code associated with the current command line, the rate of command takes effect.

  Response: `OK`

Parameter:

- **\<rate>** - Baud rate per second

  Available Baud rates: 9600, 19200, 38400, 57600, 115200, 230400, 460800, 921600

{{< hint info >}}

1. If a fixed baud rate is set, make sure that both TE (DTE, usually external processor)
   and TA (DCE, Quectel module) are configured to the same rate.
1. The value of **AT+IPR** cannot be restored with **AT&F** and **ATZ**;
   but it is still storable with **AT&W**.
1. In multiplex mode, the baud rate cannot be changed by the _Write Command_ **AT+IPR=\<rate>**,
   and the setting is invalid and cannot be stored even if **AT&W** is executed after the _Write Command_.
1. A selected baud rate takes effect after the _Write Command_ is executed and acknowledged by **OK**.

{{< /hint >}}

Example:

```at
AT+IPR=115200 // Set fixed baud rate to 115200bps.
OK
AT&W // Store current setting, that is, the serial communication speed is 115200bps after restarting module
OK
AT+IPR?
+IPR: 115200

OK
AT+IPR=115200;&W // Set fixed baud rate to 115200bps and store current setting
OK
```
