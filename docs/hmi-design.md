# HMI Design

## Platform

The operator interface is a C-more CM5-T10W panel using AutomationDirect K-Sequence communications to the D2-262 PLC.

The HMI database contains one live discrete tag per flow point. Separate "No Flow" tags are not required; the display object handles both states from the same PLC bit.

## Indicator behavior

Each flow point is shown as a large status tile:

- green = flow / normal
- red = no flow / abnormal

The final screen is based on a 7 x 6 layout, providing room for all 39 active indicators plus spare positions for future use.

The design favors readability over decorative graphics. Equipment names are large enough to identify quickly during troubleshooting, and the final layout avoids the cramped appearance of the legacy screen.

## Tag design

Representative sanitized tags:

```text
DI12000_1_Flow
HeatShield_1_Flow
Gun_1_Flow
LoadingDoor_1_Flow
Turbo1000_Flow
```

All PLC tags are registered to the actual D2-262 device in the C-more protocol manager. During commissioning, an import issue exposed the importance of matching the CSV `DeviceName` exactly to the registered device name; otherwise C-more converts the unmatched tags into internal tags.

## Alarm philosophy

The main all-flow alarm/healthy condition remains in the PLC. The HMI can optionally add banner or history events, but the machine-level condition does not depend on HMI execution.
