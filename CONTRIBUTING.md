# Contributing

Detections and playbooks welcome.

- **New Sentinel rule:** follow the schema in [docs/DETECTION-FORMAT.md](docs/DETECTION-FORMAT.md) —
  include ATT&CK mapping, entity mappings, and tuning notes. Give it a fresh GUID.
- **New Splunk search:** comment the data source, logic, and tuning inline.
- **Playbooks:** keep the NIST 800-61 phase structure.
- **Never** commit real IOCs, tenant IDs, hostnames, or account names — use placeholders.

Test detections in a dev workspace before submitting. Contributions are MIT-licensed and provided
as reference material, not as guaranteed detections for your environment.
