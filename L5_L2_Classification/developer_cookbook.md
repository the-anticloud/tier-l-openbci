# Developer Cookbook — L_OPENBCI
**Stack:** Python 3.11, brainflow 5.x (OpenBCI backend), pyserial, PAX 27B, AIOSS_FORMAT
**Domain:** OpenBCI: OpenBCI hardware integration for Anticloud EEG/EMG data acquisition

## OpenBCI acquisition
```python
from l_openbci import OpenBCIManager

manager = OpenBCIManager(
    board="cyton",
    port="COM3",
    n_channels=8,
    fs=250,
    pax_model="./pax-27b-q4.gguf",
    aioss_chain="./openbci.aioss"
)

# Check impedances before recording
impedances = manager.check_impedances()
for ch, imp in enumerate(impedances):
    print(f"Ch{ch+1}: {imp:.0f}kΩ {'OK' if imp < 20 else 'HIGH'}")

manager.start_recording(duration_s=60)
data = manager.get_recording()
print(f"PAX quality: {manager.pax_quality_report}")
```

## AIOSS Chain Append
```python
import hashlib, time

def aioss_append(chain_path, payload: bytes, module_id: str):
    entry_hash = hashlib.sha3_256(payload).digest()
    ts = int(time.time_ns()).to_bytes(8, 'big')
    with open(chain_path, 'rb') as f:
        f.seek(-32, 2); prev_hash = f.read(32)
    new_hash = hashlib.sha3_256(prev_hash + entry_hash + ts).digest()
    with open(chain_path, 'ab') as f:
        f.write(ts + entry_hash + new_hash)
    return new_hash.hex()
```
