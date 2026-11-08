# L5 Narrow / L2 General Classification — L_OPENBCI
**Platform:** Anticloud | **Tier:** TIER_7_BIOSIGNALS_NEURO | **PAX:** 27B
**IP:** USPTO pending 2026, Anticloud FZ LLE, 0-1.gg | **License:** Apache-2.0

## L5 Narrow
L_OPENBCI provides deep integration with OpenBCI hardware (Cyton, Ganglion, Daisy) for Anticloud: board configuration, electrode impedance measurement, real-time streaming, and recording management. Narrow scope: Anticloud OpenBCI deployments.

## L2 General
L2 General: L_OPENBCI enables Anticloud deployment in resource-constrained settings (field BCI, affordable clinical systems) using OpenBCI's low-cost hardware. Same Anticloud software stack, different hardware economics.

## PAX 27B Integration
PAX 27B monitors OpenBCI signal quality in real-time: 'Channel 3 impedance elevated at 45kΩ — patient may need electrode re-gel. Signal quality: acceptable for research, below clinical threshold.'

## AIOSS Audit Chain
Every acquisition session (board config hash + impedance check hash + signal quality hash + recording hash) is chained: H_n = SHA3-256(H_{n-1} || entry_hash_n || timestamp_n).
Offline-verifiable, tamper-evident, zero cloud dependency.

## Regulatory / Compliance
IEC 62304 (medical software). HIPAA. FCC Part 15 (wireless EEG headsets).
