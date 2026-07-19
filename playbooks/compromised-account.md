# Playbook: Compromised Account

**Aligned to NIST SP 800-61.** Trigger: impossible-travel, password-spray-success, illicit consent,
or user-reported takeover.

## 1. Detect & Triage (0–15 min)
- Confirm the alert (Sentinel incident → related entities, sign-in logs).
- Classify severity by account privilege (standard user vs. admin vs. service principal).

## 2. Contain (immediate)
- **Disable sign-in** for the account (Entra → user → Block sign-in).
- **Revoke sessions & refresh tokens** (`Revoke-MgUserSignInSession` / Entra "Revoke sessions").
- **Reset password**; require re-registration of MFA if MFA method is suspect.
- Review & remove any **new OAuth consents, mail forwarding rules, inbox rules, MFA methods,
  or app passwords** created during the compromise window.

## 3. Analyze (scope)
- Pivot on IP/user in Sentinel: what did the attacker access (mail, files, apps)?
- Check for **persistence**: added devices, added app registrations, role assignments (PIM/Entra).
- Determine data exposure (Purview audit, download volume) for breach-notification decisions.

## 4. Eradicate & Recover
- Remove attacker persistence; re-enable the account only after clean.
- Restore any altered rules/permissions to known-good.
- Monitor the account closely for 7 days.

## 5. Lessons Learned
- Root cause (phishing? no MFA? legacy auth?) → drive a control fix (CA policy, awareness).
- Update detections/thresholds; document timeline for the incident record.

**Key controls that prevent recurrence:** phishing-resistant MFA, block legacy auth, restrict user
consent, PIM for privileged roles.
