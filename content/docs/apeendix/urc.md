---
title: Summary of URC
weight: 4
---

## Unconditional

1. ME initialization is successful

   URC Display:

   ```at-command
   RDY
   ```

1. All function of the ME is available

   URC Display:

   ```at-command
   +CFUN: 1
   ```

1. SIM card pin state

   URC Display:

   ```at-command
   +CPIN: <state>
   ```

1. SMS initialization finished

   URC Display:

   ```at-command
   +QIND: SMS DONE
   ```

1. Phonebook initialization finished

   URC Display:

   ```at-command
   +QIND: PB DONE
   ```

## AT+CREG

1. Indicate registration status of the ME

   Condition: `AT+CREG=1`

   URC Display:

   ```at-command
   +CREG: <stat>
   ```

1. After cell neighborhood changing shows whether
   the network has currently indicated the registration
   of the ME, with location area code

   Condition: `AT+CREG=2`

   URC Display:

   ```at-command
   +CREG: <stat>[,<lac>,<ci>[,<Act>]]
   ```

## AT+CGREG

1. Indicate network registration status of the ME

   Condition: `AT+CGREG=1`

   URC Display:

   ```at-command
   +CGREG: <stat>
   ```

1. Indicate network registration and location information of the ME

   Condition: `AT+CGREG=2`

   URC Display:

   ```at-command
   +CGREG: <stat>[,<lac>,<ci>[,<Act>]]
   ```

## AT+CTZR

1. Indicate network registration status of the ME

   Condition: `AT+CTZR=1`

   URC Display:

   ```at-command
   +CTZV: <tz>
   ```

1. Indicate network registration and location information of the ME

   Condition: `AT+CTZR=2`

   URC Display:

   ```at-command
   +CTZE: <tz>,<dst>,<time>
   ```

## AT+CNMI

1. New message is received, and saved to memory

   URC Display:

   ```at-command
   +CMTI: <mem>,<index>
   ```

1. New short message is received and outputted directly to TE (PDU mode)

   URC Display:

   ```at-command
   +CMT: [<alpha>],<length><CR><LF>
   <pdu>
   ```

1. New short message is received and outputted directly to TE (Text mode)

   URC Display:

   ```at-command
   +CMT: <oa>,[<alpha>],<scts>[,<toa>,<fo>,<pid>,<dcs>,<sca>,<tosca>,<length>]<CR><LF>
   <data>
   ```

1. New short message is received and outputted directly to TE (CDMA Text mode)

   URC Display:

   ```at-command
   ^HCMT: <oa>,<scts>,<lang>, <fmt>,<length>,<prt>,<prv>,<type>,<stat><CR><LF>
   <data>
   ```

1. New CBM is received and outputted directly (PDU mode)

   URC Display:

   ```at-command
   +CBM: <length><CR><LF>
   <pdu>
   ```

1. New CBM is received and outputted directly to TE (Text mode)

   URC Display:

   ```at-command
   +CBM: <sn>,<mid>,<dcs>,<page>,<pages><CR><LF>
   <data>
   ```

1. New CDS is received and outputted directly (PDU mode)

   URC Display:

   ```at-command
   +CDS: <length><CR><LF>
   <pdu>
   ```

1. New CDS is received and outputted directly to TE (Text mode)

   URC Display:

   ```at-command
   +CDS: <fo>,<mr>,[<ra>],[<tora>],<scts>,<dt>,<st>
   ```

1. New message status report is received, and saved to memory

   URC Display:

   ```at-command
   +CDSI: <mem>,<index>
   ```

1. New CDS is received and outputted directly to TE (in CDMA Text mode)

   URC Display:

   ```at-command
   ^HCDS: <oa>,<scts>,<lang>,<fmt>,<length>,<prt>,<prv>,<type>,<stat><CR><LF><data>
   ```

## AT+COLP

1. The presentation of the COL (connected line) at the TE for a mobile originated call

   Condition: `AT+COLP=1`

   URC Display:

   ```at-command
   +COLP: <number>,<type>,[<subaddr>],[<satype>],[<alpha>]
   ```

## AT+CLIP

1. Mobile terminating call indication

   Condition: `AT+CLIP=1`

   URC Display:

   ```at-command
   +CLIP: <number>,<type>,[subaddr],[satype],[<alpha>],<CLI validity>
   ```

## AT+CRC

1. An incoming call is indicated to the TE with unsolicited result code instead of the normal RING

   Condition: `AT+CRC=1`

   URC Display:

   ```at-command
   +CRING: <type>
   ```

## AT+CCWA

1. Call waiting indication

   Condition: `AT+CCWA=1`

   URC Display:

   ```at-command
   +CCWA: <number>,<type>,<class>[,<alpha>]
   ```

## AT+CSSN

1. Shows the `+CSSI` intermediate result code presentation status to the TE

   Condition: `AT+CSSN=1`

   URC Display:

   ```at-command
   +CSSI: <code1>
   ```

1. Shows the +CSSU unsolicited result code presentation status to the TE

   Condition: `AT+CSSN=<n>,1`

   URC Display:

   ```at-command
   +CSSI: <code2>
   ```

## AT+CUSD

1. USSD response from the network, or a network initiated operation

   Condition: `AT+CUSD=1`

   URC Display:

   ```at-command
   +CUSD: <status>[,<rspstr>,[<dcs>]]
   ```

## AT+QPOWD

{{< hint info >}}Quectel Specific Commands{{< /hint >}}

1. Module power down

   Condition: `AT+QPOWD`

   URC Display:

   ```at-command
   POWERED DOWN
   ```

## AT+CGEREP

1. A network request for PDP activation, and was automatically rejected.

   Condition: `AT+CGEREP=2,1`

   URC Display:

   ```at-command
   +CGEV: REJECT <PDP_type>,<PDP_addr>
   ```

1. The network request PDP reactivation.

   Condition: `AT+CGEREP=2,1`

   URC Display:

   ```at-command
   +CGEV: NW REACT <PDP_type>,<PDP_addr>,[<cid>]
   ```

1. The network has forced a context deactivation.

   Condition: `AT+CGEREP=2,1`

   URC Display:

   ```at-command
   +CGEV: NW DEACT <PDP_type>,<PDP_addr>,[<cid>]
   ```

1. The ME has forced a context deactivation.

   Condition: `AT+CGEREP=2,1`

   URC Display:

   ```at-command
   +CGEV: ME DEACT <PDP_type>,<PDP_addr>,[<cid>]
   ```

1. The network has forced a Packet Domain detach.

   Condition: `AT+CGEREP=2,1`

   URC Display:

   ```at-command
   +CGEV: NW DETACH
   ```

1. The mobile equipment has forced a Packet Domain detach.

   Condition: `AT+CGEREP=2,1`

   URC Display:

   ```at-command
   +CGEV: ME DETACH
   ```

1. The network has forced a change of MS class.

   Condition: `AT+CGEREP=2,1`

   URC Display:

   ```at-command
   +CGEV: NW CLASS <class>
   ```

1. The mobile equipment has forced a change of MS class.

   Condition: `AT+CGEREP=2,1`

   URC Display:

   ```at-command
   +CGEV: ME CLASS <class>
   ```
