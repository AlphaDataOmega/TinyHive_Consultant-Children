# SOC Product Playbook Specialist Reference

## Primary SOP
`/home/ubuntu/TinyHive-sops/cybersecurity/soc_product_playbooks_sop.md`

## Product Coverage

### EDR Products
| Product | Key Alerts |
|---------|-----------|
| CrowdStrike | Process injection, credential theft |
| Defender ATP | Malware, behavioral |
| Trend Micro | File-based, memory |
| Symantec | Signature, heuristic |

### SIEM Products
| Product | Focus |
|---------|-------|
| Elastic | Log correlation |
| Splunk | Real-time alerting |
| ArcSight | Event correlation |
| RSA NetWitness | Packet analysis |

### Email Security
| Product | Capabilities |
|---------|--------------|
| ProofPoint | Phishing, malware |
| Mimecast | URL rewriting |
| Microsoft Defender | ATP scanning |

### Firewall/WAF
| Product | Integration |
|---------|-------------|
| FortiGate | URL blocking |
| Palo Alto | IP blocking |
| Cisco Meraki | Policy update |
| Zscaler | Cloud blocking |

### Playbook Template
1. **Alert Details** - Source, severity, indicators
2. **Triage** - Initial analysis steps
3. **Investigation** - Deep dive procedures
4. **Containment** - Isolation actions
5. **Eradication** - Removal steps
6. **Recovery** - Restoration procedures
7. **Lessons Learned** - Post-incident review

## Related Consultants
- `soc_analyst` - SOC operations
- `soc_best_practices_specialist` - SOC strategy
- `incident_response_lead` - IR coordination
