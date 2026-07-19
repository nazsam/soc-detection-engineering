# Playbook: Phishing / Business Email Compromise (BEC)

**Aligned to NIST SP 800-61.** Trigger: user report, Defender for Office alert, or mail-flow anomaly.

## 1. Detect & Triage
- Pull the message (Defender → Threat Explorer). Identify sender, URLs, attachments, and **who
  received/clicked/reported**.
- Determine campaign scope: how many recipients, how many interacted.

## 2. Contain
- **Purge** the malicious message tenant-wide (Explorer → Soft/Hard delete).
- **Block** sender, URLs, and file hashes (Tenant Allow/Block List, Defender indicators).
- If credentials were entered → immediately run the **[compromised-account](compromised-account.md)**
  playbook for those users.

## 3. Analyze
- For any clicker: check sign-in logs, new inbox rules (auto-forward is a BEC hallmark), OAuth
  consents, and mailbox delegation.
- Detonate attachments/URLs in a sandbox; extract IOCs.

## 4. Eradicate & Recover
- Remove inbox rules/forwarding created by the attacker.
- Confirm no residual access; restore normal mail flow.

## 5. Lessons Learned
- Feed IOCs into threat intel & detections.
- Targeted awareness for affected users; tune anti-phishing policies (impersonation protection).

**Preventive controls:** anti-phishing/impersonation policies, safe links/attachments, DMARC/DKIM/SPF
enforcement, disable auto-forwarding to external domains.
