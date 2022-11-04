---
title: Summary of URC
weight: 4
---

## Unconditional

1. ME initialization is successful

   URC Display:

   ```at
   RDY
   ```

1. All function of the ME is available

   URC Display:

   ```at
   +CFUN: 1
   ```

1. SIM card pin state

   URC Display:

   ```at
   +CPIN: <state>
   ```

1. SMS initialization finished

   URC Display:

   ```at
   +QIND: SMS DONE
   ```

1. Phonebook initialization finished

   URC Display:

   ```at
   +QIND: PB DONE
   ```

## AT+CREG

1. Indicate registration status of the ME

   Condition: `AT+CREG=1`

   URC Display:

   ```at
   +CREG: <stat>
   ```

1. After cell neighborhood changing shows whether
   the network has currently indicated the registration
   of the ME, with location area code

   Condition: `AT+CREG=2`

   URC Display:

   ```at
   +CREG: <stat>[,<lac>,<ci>[,<Act>]]
   ```

## AT+CGREG

1. Indicate network registration status of the ME

   Condition: `AT+CGREG=1`

   URC Display:

   ```at
   +CGREG: <stat>
   ```

1. Indicate network registration and location information of the ME

   Condition: `AT+CGREG=2`

   URC Display:

   ```at
   +CGREG: <stat>[,<lac>,<ci>[,<Act>]]
   ```

## AT+CTZR

1. Indicate network registration status of the ME

   Condition: `AT+CTZR=1`

   URC Display:

   ```at
   +CTZV: <tz>
   ```

1. Indicate network registration and location information of the ME

   Condition: `AT+CTZR=2`

   URC Display:

   ```at
   +CTZE: <tz>,<dst>,<time>
   ```

## AT+CNMI

1. New message is received, and saved to memory

   URC Display:

   ```at
   +CMTI: <mem>,<index>
   ```

1. New short message is received and outputted directly to TE (PDU mode)

   URC Display:

   ```at
   +CMT: [<alpha>],<length><CR><LF>
   <pdu>
   ```

1. New short message is received and outputted directly to TE (Text mode)

   URC Display:

   ```at
   +CMT: <oa>,[<alpha>],<scts>[,<toa>,<fo>,<pid>,<dcs>,<sca>,<tosca>,<length>]<CR><LF>
   <data>
   ```

1. New short message is received and outputted directly to TE (CDMA Text mode)

   URC Display:

   ```at
   ^HCMT: <oa>,<scts>,<lang>, <fmt>,<length>,<prt>,<prv>,<type>,<stat><CR><LF>
   <data>
   ```

1. New CBM is received and outputted directly (PDU mode)

   URC Display:

   ```at
   +CBM: <length><CR><LF>
   <pdu>
   ```

1. New CBM is received and outputted directly to TE (Text mode)

   URC Display:

   ```at
   +CBM: <sn>,<mid>,<dcs>,<page>,<pages><CR><LF>
   <data>
   ```

1. New CDS is received and outputted directly (PDU mode)

   URC Display:

   ```at
   +CDS: <length><CR><LF>
   <pdu>
   ```

1. New CDS is received and outputted directly to TE (Text mode)

   URC Display:

   ```at
   +CDS: <fo>,<mr>,[<ra>],[<tora>],<scts>,<dt>,<st>
   ```

1. New message status report is received, and saved to memory

   URC Display:

   ```at
   +CDSI: <mem>,<index>
   ```

1. New CDS is received and outputted directly to TE (in CDMA Text mode)

   URC Display:

   ```at
   ^HCDS: <oa>,<scts>,<lang>,<fmt>,<length>,<prt>,<prv>,<ty pe>,<stat><CR><LF><data>
   ```

## AT+COLP

1. The presentation of the COL (connected line) at the TE for a mobile originated call

   Condition: `AT+COLP=1`

   URC Display:

   ```at
   +COLP: <number>,<type>,[<subaddr>],[<satype>],[<alpha>]
   ```

## AT+CLIP

1. Mobile terminating call indication

   Condition: `AT+CLIP=1`

   URC Display:

   ```at
   +CLIP: <number>,<type>,[subaddr],[satype],[<alpha>],<CLI validity>
   ```

## AT+CRC

1. An incoming call is indicated to the TE with unsolicited result code instead of the normal RING

   Condition: `AT+CRC=1`

   URC Display:

   ```at
   +CRING: <type>
   ```

## AT+CCWA

1. Call waiting indication

   Condition: `AT+CCWA=1`

   URC Display:

   ```at
   +CCWA: <number>,<type>,<class>[,<alpha>]
   ```

## AT+CSSN

1. Shows the `+CSSI` intermediate result code presentation status to the TE

   Condition: `AT+CSSN=1`

   URC Display:

   ```at
   +CSSI: <code1>
   ```

1. Shows the +CSSU unsolicited result code presentation status to the TE

   Condition: `AT+CSSN=<n>,1`

   URC Display:

   ```at
   +CSSI: <code2>
   ```

## AT+CUSD

1. USSD response from the network, or a network initiated operation

   Condition: `AT+CUSD=1`

   URC Display:

   ```at
   +CUSD: <status>[,<rspstr>,[<dcs>]]
   ```

## AT+QPOWD

{{< hint info >}}Quectel Specific Commands{{< /hint >}}

1. Module power down

   Condition: `AT+QPOWD`

   URC Display:

   ```at
   POWERED DOWN
   ```

## AT+CGEREP

1. A network request for PDP activation, and was automatically rejected.

   Condition: `AT+CGEREP=2,1`

   URC Display:

   ```at
   +CGEV: REJECT <PDP_type>,<PDP_addr>
   ```

1. The network request PDP reactivation.

   Condition: `AT+CGEREP=2,1`

   URC Display:

   ```at
   +CGEV: NW REACT <PDP_type>,<PDP_addr>,[<cid>]
   ```

1. The network has forced a context deactivation.

   Condition: `AT+CGEREP=2,1`

   URC Display:

   ```at
   +CGEV: NW DEACT <PDP_type>,<PDP_addr>,[<cid>]
   ```

1. The ME has forced a context deactivation.

   Condition: `AT+CGEREP=2,1`

   URC Display:

   ```at
   +CGEV: ME DEACT <PDP_type>,<PDP_addr>,[<cid>]
   ```

1. The network has forced a Packet Domain detach.

   Condition: `AT+CGEREP=2,1`

   URC Display:

   ```at
   +CGEV: NW DETACH
   ```

1. The mobile equipment has forced a Packet Domain detach.

   Condition: `AT+CGEREP=2,1`

   URC Display:

   ```at
   +CGEV: ME DETACH
   ```

1. The network has forced a change of MS class.

   Condition: `AT+CGEREP=2,1`

   URC Display:

   ```at
   +CGEV: NW CLASS <class>
   ```

1. The mobile equipment has forced a change of MS class.

   Condition: `AT+CGEREP=2,1`

   URC Display:

   ```at
   +CGEV: ME CLASS <class>
   ```
