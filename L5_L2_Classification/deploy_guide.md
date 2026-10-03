# Deploy Guide — PAX_MONITOR
**Stack:** Python 3.11, psutil, py3nvml (NVIDIA), Prometheus metrics, AIOSS_FORMAT | Air-gap capable

## Prerequisites
Anticloud core stack installed. PAX 27B weights (pax-27b-q4.gguf). AIOSS_FORMAT.

## Install
```bash
pip install anticloud-pax-monitor
```

## AIOSS Integration
```bash
aioss init --module PAX_MONITOR --output ./pax_monitor.aioss
```

## Air-Gap
```bash
pip download -r requirements.txt -d ./wheels/
pip install --no-index --find-links ./wheels/ -r requirements.txt
```

## PAX Harness Wiring
```python
from anticloud_pax import PAXHarness
harness = PAXHarness(model_path="./pax-27b-q4.gguf", module="PAX_MONITOR",
                     aioss_chain="./pax_monitor.aioss",
                     classification="L5_NARROW_L2_GENERAL")
```

## Verification
```bash
aioss verify --chain ./pax_monitor.aioss --verbose
python -m pax_monitor.tests.smoke
```
