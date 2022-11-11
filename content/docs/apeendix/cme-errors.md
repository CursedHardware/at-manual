---
title: Summary of CME ERROR Codes
weight: 3
bookToC: false
---

Final result code **+CME ERROR: \<err>** indicates an error related to mobile equipment or network.

The operation is similar to **ERROR** result code.

None of the following commands in the same command line is executed.

Neither **ERROR** nor **OK** result code shall be returned.

**\<err>** values are mostly used by common message commands.

The following table lists most of general and GPRS related **ERROR** codes.

For some GSM protocol failure cause described in GSM specifications, the corresponding **ERROR** codes are not included.

Different Coding Schemes of **+CME ERROR: \<err>**:

<!-- cspell:disable -->

```csv
Code,Meaning
0,Phone failure
1,No connection to phone
2,Phone-adaptor link reserved
3,Operation not allowed
4,Operation not supported
5,PH-SIM PIN required
6,PH-FSIM PIN required
7,PH-FSIM PUK required
10,SIM not inserted
11,SIM PIN required
12,SIM PUK required
13,SIM failure
14,SIM busy
15,SIM wrong
16,Incorrect password
17,SIM PIN2 required
18,SIM PUK2 required
20,Memory full
21,Invalid index
22,Not found
23,Memory failure
24,Text string too long
25,Invalid characters in text string
26,Dial string too long
27,Invalid characters in dial string
30,No network service
31,Network timeout
32,Network not allowed - emergency calls only
40,Network personalization PIN required
41,Network personalization PUK required
42,Network subset personalization PIN required
43,Network subset personalization PUK required
44,Service provider personalization PIN required
45,Service provider personalization PUK required
46,Corporate personalization PIN required
47,Corporate personalization PUK required
901,Audio unknown error
902,Audio invalid parameters
903,Audio operation not supported
904,Audio device busy
```
