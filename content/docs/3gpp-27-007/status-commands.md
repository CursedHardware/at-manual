---
title: Status Control Commands
weight: 2
---

## AT+CPAS (Mobile Equipment Activity Status)

- Test Command: `AT+CPAS=?`

  Response:

  ```at
  +CPAS: (list of supported <pas>s)

  OK
  ```

- Execution Command: `AT+CPAS`:

  TA returns the activity status of ME:

  Response:

  ```at
  +CPAS: <pas>

  OK // or ERROR
  ```

  If there is any error related to ME functionality:

  ```at
  +CME ERROR: <err>
  ```

Parameter:

```csv
Name,Value,Note
\<pas>,0,Ready
,3,Ringing
,4,Call in progress or call hold
```

Example:

```at
AT+CPAS
+CPAS: 0 // The module is idle

OK
RING
AT+CLCC
+CLCC: 1,1,4,0,0,"15695519173",161

OK
AT+CPAS
+CPAS: 3 // The module is ringing

OK
AT+CLCC
+CLCC: 1,0,0,0,0,"10010",129

OK
AT+CPAS
+CPAS: 4 // Call in progress

OK
```
