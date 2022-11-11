---
title: Summary of CMS ERROR Codes
weight: 4
bookToC: false
---

Final result code **+CMS ERROR: \<err>** indicates an error related to mobile equipment or network.

The operation is similar to **ERROR** result code.

None of the following commands in the same command line is executed.

Neither **ERROR** nor **OK** result code shall be returned.

**\<err>** values are mostly used by common message commands.

Different Coding Schemes of **+CMS ERROR: \<err>**:

<!-- cspell:disable -->

```csv
Code,Meaning
300,ME failure
301,SMS ME reserved
302,Operation not allowed
303,Operation not supported
304,Invalid PDU mode
305,Invalid text mode
310,SIM not inserted
311,SIM pin necessary
312,PH SIM pin necessary
313,SIM failure
314,SIM busy
315,SIM wrong
316,SIM PUK required
317,SIM PIN2 required
318,SIM PUK2 required
320,Memory failure
321,Invalid memory index
322,Memory full
330,SMSC address unknown
331,No network
332,Network timeout
500,Unknown
512,SIM not ready
513,Message length exceeds
514,Invalid request parameters
515,ME storage failure
517,Invalid service mode
529,More message to send state error\nMO SMS is not allow
530,GPRS is suspended
531,ME storage full
```
