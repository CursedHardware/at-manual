---
title: Serial Interface Control Commands
weight: 2
---

## `AT+QRIR` Restore RI Behavior to Inactive {#atqrir}

If the RI (ring indicator) behavior is "always", it can be restored to inactive by the _Execution Command_.

The RI behavior is controlled by `AT+QCFG`.

Please refer to
[`AT+QCFG="urc/ri/ring"`]({{< ref "status-commands#atqcfg-urc-ri-ring" >}}),
[`AT+QCFG="urc/ri/smsincoming"`]({{< ref "status-commands#atqcfg-urc-ri-smsincoming" >}}) and
[`AT+QCFG="urc/ri/other"`]({{< ref "status-commands#atqcfg-urc-ri-other" >}})
for more details.

- Test Command: `AT+QRIR=?`

  Response: `OK`

- Execution Command: `AT+QRIR`

  Response: `OK` or `ERROR`
