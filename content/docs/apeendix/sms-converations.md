---
title: SMS Character Sets Conversions
linkTitle: SMS Charset Conversions
---

in 3GPP TS 23.038 DCS (Data Coding Scheme) defined three kinds of alphabets in SMS,
GSM 7 bit default alphabet, 8 bit data and UCS2 (16 bit).

**AT+CSMP** can set the DCS in text mode (**AT+CMGF=1**).

In text mode, DCS (Data Coding Scheme) and **AT+CSCS** determine the way of SMS text input or output.

## The Way of SMS Text Input or Output {#sms-text-io}

```csv
DCS,AT+CSCS,The Way of SMS Text Input or Output
GSM 7 bit,GSM,Input or output GSM character sets.
GSM 7 bit,IRA,Input or output IRA character sets.\nInput: UE will convert IRA characters to GSM characters.\nOutput: UE will convert GSM characters to IRA characters.
GSM 7 bit,UCS2,Input or output a hex string similar to PDU mode.\nInput: UE will convert the UCS2 hex string to GSM characters.\nOutput: UE will convert the GSM characters to UCS2 hex string.
UCS2,,"Ignore the value of AT+CSCS,\ninput or output a hex string similar to PDU mode."
8 bit,,"Ignore the value of AT+CSCS,\ninput or output a hex string similar to PDU mode."
```

When DCS=GSM 7 bit, the input or output needs conversion.

The detailed conversion tables are shown as below.

Because the low 8 bit of **UCS2** character is the same as the **IRA** character:

- The conversion table of **DCS=GSM 7 bit** and `AT+CSCS="UCS2"` is similar to `AT+CSCS="IRA"`.
- The conversion table of **DCS=GSM 7 bit** and `AT+CSCS="GSM"` is similar to `AT+CSCS="GSM"`.
- The conversion table of **DCS=GSM 7 bit** and `AT+CSCS="IRA"` is similar to `AT+CSCS="IRA"`.
- The conversion table of **DCS=GSM 7 bit** and `AT+CSCS="UCS2"` is similar to `AT+CSCS="IRA"`.

The difference is the way of SMS text input or output.

## GSM Conversions Table {#gsm7bit}

> DCS=GSM 7 bit
>
> `AT+CSCS="GSM"`

{{< tabs "gsm7bit" >}}
{{< tab "Input Table" >}}

```csv
#,0,1,2,3,4,5,6,7
0,00,10,20,30,40,50,60,70
1,01,11,21,31,41,51,61,71
2,02,12,22,32,42,52,62,72
3,03,13,23,33,43,53,63,73
4,04,14,24,34,44,54,64,74
5,05,15,25,35,45,55,65,75
6,06,16,26,36,46,56,66,76
7,07,17,27,37,47,57,67,77
8,08,18,28,38,48,58,68,78
9,09,19,29,39,49,59,69,79
A,0A,Submit,2A,3A,4A,5A,6A,7A
B,0B,Cancel,2B,3B,4B,5B,6B,7B
C,0C,1C,2C,3C,4C,5C,6C,7C
D,0D,1A,2D,3D,4D,5D,6D,7D
E,0E,1E,2E,3E,4E,5E,6E,7E
F,0F,1F,2F,3F,4F,5F,6F,7F
```

{{< /tab >}}
{{< tab "Output Table" >}}

```csv
#,0,1,2,3,4,5,6,7
0,00,10,20,30,40,50,60,70
1,01,11,21,31,41,51,61,71
2,02,12,22,32,42,52,62,72
3,03,13,23,33,43,53,63,73
4,04,14,24,34,44,54,64,74
5,05,15,25,35,45,55,65,75
6,06,16,26,36,46,56,66,76
7,07,17,27,37,47,57,67,77
8,08,18,28,38,48,58,68,78
9,09,19,29,39,49,59,69,79
A,0D,0A,2A,3A,4A,5A,6A,7A
B,0B,0B,2B,3B,4B,5B,6B,7B
C,0C,1C,2C,3C,4C,5C,6C,7C
D,0D,1A,2D,3D,4D,5D,6D,7D
E,0E,1E,2E,3E,4E,5E,6E,7E
F,0F,1F,2F,3F,4F,5F,6F,7F
```

{{< /tab >}}
{{< tab "Extended Characters" >}}

```csv
#,0,1,2,3,4,5,6,7
0,,,,,1B40,,,
1,,,,,,,,
2,,,,,,,,
3,,,,,,,,
4,,1B14,,,,,,
5,,,,,,,,
6,,,,,,,,
7,,,,,,,,
8,,,1B28,,,,,
9,,,1B29,,,,,
A,,,,,,,,
B,,,,,,,,
C,,,,1B3C,,,,
D,,,,1B3D,,,,
E,,,,1B3E,,,,
F,,,1B2F,,,,,
```

{{< /tab >}}
{{< /tabs >}}

## IRA Conversions Table {#ira}

> DCS=GSM 7 bit
>
> `AT+CSCS="IRA"`

{{< tabs "ira" >}}
{{< tab "Input Table" >}}

```csv
#,0,1,2,3,4,5,6,7
0,20,20,20,30,00,50,20,70
1,20,20,21,31,41,51,61,71
2,20,20,22,32,42,52,62,72
3,20,20,23,33,43,53,63,73
4,20,20,02,34,44,54,64,74
5,20,20,25,35,45,55,65,75
6,20,20,26,36,46,56,66,76
7,20,20,27,37,47,57,67,77
8,Backspace,20,28,38,48,58,68,78
9,20,20,29,39,49,59,69,79
A,0A,Submit,2A,3A,4A,5A,6A,7A
B,20,Cancel,2B,3B,4B,1B3C,6B,1B28
C,20,20,2C,3C,4C,1B2F,6C,1B40
D,0D,20,2D,3D,4D,1B3E,6D,1B29
E,20,20,2E,3E,4E,1B14,6E,1B3D
F,20,20,2F,3F,4F,11,6F,20
```

{{< /tab >}}
{{< tab "Output Table" >}}

```csv
#,0,1,2,3,4,5,6,7
0,40,20,20,30,A1,50,BF,70
1,A3,5F,21,31,41,51,61,71
2,24,20,22,32,42,52,62,72
3,A5,20,23,33,43,53,63,73
4,E8,20,A4,34,44,54,64,74
5,E9,20,25,35,45,55,65,75
6,F9,20,26,36,46,56,66,76
7,EC,20,27,37,47,57,67,77
8,F2,20,28,38,48,58,68,78
9,C7,20,29,39,49,59,69,79
A,0D,0A,2A,3A,4A,5A,6A,7A
B,D8,D8,2B,3B,4B,C4,6B,E4
C,F8,C6,2C,3C,4C,D6,6C,F6
D,0D,E6,2D,3D,4D,D1,6D,F1
E,C5,DF,2E,3E,4E,DC,6E,FC
F,E5,C9,2F,3F,4F,A7,6F,E0
```

{{< /tab >}}
{{< tab "Extended Characters" >}}

```csv
#,A,B,C,D,E,F
0,20,20,20,20,7F,20
1,40,20,20,5D,20,7D
2,20,20,20,20,20,08
3,01,20,20,20,20,20
4,24,20,5B,20,7B,20
5,03,20,0E,20,0F,20
6,20,20,1C,5C,1D,7C
7,5F,20,09,20,20,20
8,20,20,20,0B,04,0C
9,20,20,1F,20,05,06
A,20,20,20,20,20,20
B,20,20,20,20,20,20
C,20,20,20,5E,07,7E
D,20,20,20,20,20,20
E,20,20,20,20,20,20
F,20,20,20,1E,20,20
```

{{< /tab >}}
{{< /tabs >}}
