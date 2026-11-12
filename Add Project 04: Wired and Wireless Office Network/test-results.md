# Project 04 — Connectivity Test Results

All five tests were reported as successful.

| Test ID | Source | Destination | Result |
|---|---|---|---|
| TC-01 | PC0 | PC1 (`192.168.10.11`) | Pass |
| TC-02 | Laptop | PC0 (`192.168.10.10`) | Pass |
| TC-03 | PC0 | Laptop (`192.168.10.12`) | Pass |
| TC-04 | Laptop | Smartphone (`192.168.10.14`) | Pass |
| TC-05 | Laptop | Gateway (`192.168.10.1`) | Pass |

## Notes
- These tests establish basic connectivity between the listed devices.
- Same-subnet client-to-client traffic is switched locally; it does not need
  Layer 3 routing through the default gateway.
- First-time communication may trigger ARP address resolution.
