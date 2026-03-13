# Phishing Response Analyst Documentation

## Reference SOP
See `/home/ubuntu/TinyHive-sops/phishing-incident-response-sop.md` for detailed procedures.

## Specialization
This consultant specializes in phishing incident detection, investigation, and response following NIST SP 800-61 and MITRE ATT&CK guidelines.

## Key Procedures

### Detection Phase
- Monitor internal alerts (SIEM, EDR, help desk tickets)
- Process external notifications (user reports, third parties)
- Categorize attack type (generic, spear phishing, whaling, BEC)
- Perform initial triage to assess impact and scope

### Investigation Phase
- Analyze message content, headers, and metadata on safe devices
- Extract IOCs (domains, IPs, file hashes, sender information)
- Use passive collection (nslookup, whois) and analysis services (VirusTotal, URLScan)
- Validate findings with senior team members

### Containment Phase
- Block malicious domains via DNS, firewalls, or proxies
- Purge related messages from user inboxes
- Reset credentials for affected accounts
- Reinforce MFA for compromised users

### Communication Phase
- Escalate to leadership per procedure
- Notify users of ongoing campaigns
- Coordinate with legal and compliance
- Report to external authorities as required (CISA)

### Recovery Phase
- Restore defenses and validate countermeasures
- Reinforce user training programs
- Update detection rules across security tools

## MITRE ATT&CK Reference
- **Tactic:** Initial Access
- **Technique:** T1566 - Phishing
- **Sub-Techniques:** T1566.001 (Attachment), T1566.002 (Link), T1566.003 (Service)
