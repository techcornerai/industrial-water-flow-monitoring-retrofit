# PLC Design

## Hardware

The PLC platform is an AutomationDirect DirectLOGIC DL205 system using a D2-262 CPU.

- D2-262 CPU
- three D2-16ND3-2 24 VDC input modules
- one D2-08TR relay output module reserved for alarm or future expansion

The input modules are used in a sinking-input configuration. The PLC input common is tied to 0 VDC, while an interposing relay contact applies +24 VDC to the individual PLC input.

```text
+24 VDC ---- relay NO contact ---- PLC X input
0 VDC --------------------------- PLC common
```

This isolates the PLC from the legacy AC field circuits.

## Addressing strategy

The final project intentionally preserves gaps in the octal I/O map. After drawing review, nine apparent additional inputs were identified as duplicate representations of existing signals already passed through interposing relay contacts.

Those addresses were left spare instead of shifting all later points. This avoided unnecessary PLC and HMI renumbering and reduced commissioning risk.

## Status logic

Each active input is mirrored into an internal status bit. The main purpose is readability, troubleshooting, and future expansion.

A representative rung is:

```text
STR X0
OUT C0
```

## All-flow healthy logic

A single rung containing all 39 contacts exceeded the practical rung-length limit in DirectSOFT. The final solution groups the flow inputs into five smaller health conditions:

```text
Group 1 healthy -> C100
Group 2 healthy -> C101
Group 3 healthy -> C102
Group 4 healthy -> C103
Group 5 healthy -> C104
```

The final healthy output is then:

```text
STR C100
AND C101
AND C102
AND C103
AND C104
OUT Y0
```

`Y0` is ON only when every active flow input is healthy. Any failed flow condition drops `Y0`.

The HMI does not own this logic. The PLC remains responsible for the real alarm/healthy state so the control function is not dependent on the operator interface.
