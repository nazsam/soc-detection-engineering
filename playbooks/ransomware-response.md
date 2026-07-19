# Playbook: Ransomware

**Aligned to NIST SP 800-61.** Trigger: EDR mass-encryption alert, Defender ransomware detection,
or reports of encrypted files / ransom notes.

## 1. Detect & Triage (act fast — minutes matter)
- Confirm via EDR (Defender for Endpoint) — identify **patient-zero host(s)** and process lineage.
- Assess spread: how many hosts, which shares/servers, is it still encrypting?

## 2. Contain (priority: stop spread)
- **Isolate** affected hosts (Defender → Isolate device) — do **not** power off (preserves memory/forensics).
- Disable compromised accounts; revoke tokens.
- Block C2 IOCs at firewall/proxy; segment affected VLANs.
- Protect **backups** — verify they're offline/immutable and not reachable from compromised creds.

## 3. Analyze
- Identify strain, initial access vector, and dwell time (was there prior data exfiltration →
  double-extortion?).
- Preserve forensic evidence; engage legal, leadership, and (if applicable) cyber-insurance/IR retainer.

## 4. Eradicate & Recover
- Rebuild from known-good images; restore data from **verified clean** backups.
- Rotate all potentially exposed credentials/secrets and Kerberos (krbtgt x2 if AD compromised).
- Stagger restoration; monitor for reinfection.

## 5. Lessons Learned
- Root-cause the initial access (phishing, exposed RDP, unpatched VPN) and close it.
- Test backups/DR regularly; validate immutability and recovery-time objectives.

> ⚠️ **Do not pay** without executive, legal, and law-enforcement involvement — payment doesn't
> guarantee recovery and may carry legal/sanctions risk.
