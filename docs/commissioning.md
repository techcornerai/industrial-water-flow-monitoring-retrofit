# Commissioning Approach

The retrofit was commissioned in a controlled sequence rather than rewiring the entire system at once.

## Field preparation

Existing conductors were identified and labeled before removal. Source voltage was verified before transferring any signal. Legacy 24 VAC and 120 VAC circuits were kept electrically isolated from the new 24 VDC PLC side through interposing relays.

## PLC verification

Each point was verified online in DirectSOFT before final HMI validation. The commissioning process included checking:

- physical input state
- expected octal PLC address
- internal status bit
- intentional spare addresses
- grouped all-flow healthy logic
- final healthy output behavior

## HMI verification

The C-more tag database was checked against the PLC map. Each indicator was verified for the correct live PLC address and red/green state behavior.

A tag-import mismatch was also caught during commissioning: some imported tags referenced an unregistered device name and were automatically converted into internal tags. The database was corrected to use the exact registered PLC device name before final turnover.

## Turnover

Final turnover documentation recorded the legacy signal path, corrected I/O map, relay isolation concept, PLC logic structure, HMI database approach, and the deliberate spare addresses created by the duplicate-signal discovery.
