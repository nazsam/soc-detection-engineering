# Detection Format

Sentinel detections use a consistent YAML schema so they're reviewable in PRs and portable into
Microsoft Sentinel (via REST API, Bicep/ARM, or the `Az.SecurityInsights` module).

## Schema

| Field | Purpose |
|-------|---------|
| `id` | Stable GUID (don't change once deployed) |
| `name` | Human-readable rule name |
| `description` | What it detects and why it matters |
| `severity` | Informational / Low / Medium / High |
| `requiredDataConnectors` | Tables/connectors the query depends on |
| `queryFrequency` / `queryPeriod` | How often it runs / lookback window |
| `triggerOperator` / `triggerThreshold` | When it raises an incident |
| `tactics` / `relevantTechniques` | MITRE ATT&CK mapping |
| `query` | The KQL |
| `entityMappings` | Map columns → entities (Account, IP, Host) for investigation |
| `tuning` | Guidance to reduce false positives |

## Conventions
- **Always** include ATT&CK `tactics` + `relevantTechniques` — coverage must be measurable.
- **Always** include `entityMappings` — an alert you can't pivot on wastes analyst time.
- **Always** include `tuning` notes — the next engineer needs to know the known false positives.
- Prefer **fewer, higher-fidelity** rules over many noisy ones.

## Testing
- Validate KQL in a dev Log Analytics workspace before enabling.
- Where possible, generate the behaviour (Atomic Red Team / purple-team) and confirm the rule fires.
- Track detections against an ATT&CK coverage heat-map to find gaps.
