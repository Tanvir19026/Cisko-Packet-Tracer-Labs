# Project 03 — Test Results

| Test | Source | Destination | Observed result |
|---|---|---|---|
| TC-01 | IT | HR `192.168.20.10` | 3/4 replies; 25% loss on first test |
| TC-02 | HR | Admin `192.168.30.10` | 4/4 replies; 0% loss |
| TC-03 | Admin | IT `192.168.10.10` | 4/4 replies; 0% loss |

## Troubleshooting
- HR interface G0/2 was shut down.
- IT-to-HR communication failed as expected.
- IT-to-Admin communication remained successful.
- G0/2 was restored with `no shutdown` and returned to up/up.

See the screenshots folder for captured topology and ping results.
