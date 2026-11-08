# Deploy Guide — L_OPENBCI
**Tier:** TIER_7_BIOSIGNALS_NEURO | **Stack:** Python 3.11, brainflow 5.x (OpenBCI backend), pyserial, PAX 27B, AIOSS_FORMAT
**Air-gap capable after initial setup.**

## Prerequisites
Python 3.11+, brainflow 5.x, pyserial 3.5+. OpenBCI hardware required or synthetic board.

## Environment
OpenBCI Cyton or Ganglion hardware. USB dongle. 8GB RAM. Linux/Windows/Mac.

## AIOSS Integration
```bash
aioss init --module L_OPENBCI --output ./l_openbci.aioss
aioss append --chain ./l_openbci.aioss --payload ./output.bin --module L_OPENBCI
aioss verify --chain ./l_openbci.aioss
```

## Air-Gap Setup
```bash
pip download -r requirements.txt -d ./wheels/
pip install --no-index --find-links ./wheels/ -r requirements.txt
```

## PAX 27B Harness Wiring
```python
from anticloud_pax import PAXHarness
harness = PAXHarness(
    model_path="./pax-27b-q4.gguf",
    module="L_OPENBCI",
    aioss_chain="./L_OPENBCI.aioss",
    classification="L5_NARROW_L2_GENERAL"
)
result = harness.process(input_data)
```

## Verification
```bash
aioss verify --chain ./L_OPENBCI.aioss --verbose
python -m L_OPENBCI.tests.smoke
```
