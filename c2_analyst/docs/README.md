# C2 Analyst Documentation

## Overview

This directory contains reference documentation, detection rules, and operational procedures for Command and Control (C2) detection and response aligned with MITRE ATT&CK TA0011.

## Core Competencies

### C2 Techniques Coverage (MITRE ATT&CK TA0011)

| Technique ID | Name | Detection Priority |
|--------------|------|-------------------|
| T1071 | Application Layer Protocol | Critical |
| T1071.001 | Web Protocols (HTTP/HTTPS) | Critical |
| T1071.004 | DNS | Critical |
| T1095 | Non-Application Layer Protocol | High |
| T1572 | Protocol Tunneling | High |
| T1573 | Encrypted Channel | High |
| T1102 | Web Service | Medium |
| T1105 | Ingress Tool Transfer | Medium |
| T1219 | Remote Access Software | Medium |
| T1571 | Non-Standard Port | Medium |

### Key Risk Indicators

- **Beaconing patterns**: Regular, periodic outbound connections with low interval variance
- **DNS anomalies**: High entropy subdomains, encoded TXT records, excessive query volumes
- **Unusual outbound traffic**: Connections to uncategorized destinations or non-standard ports
- **Encrypted traffic to unknown hosts**: TLS connections to non-categorized IPs without valid certificates

## Detection Strategies

### DNS-Based C2 Detection

```yaml
title: DNS C2 Beaconing Detection
description: Detect DNS-based C2 beaconing activity
detection:
  selection:
    EventType: DNS_Query
  filter:
    - entropy(subdomain) > 3.5
    - length(subdomain) > 30
  aggregation:
    - count() by destination_domain > 50
    - std_dev(timestamp_intervals) < threshold
  timeframe: 1h
severity: high
tags:
  - attack.command_and_control
  - attack.t1071.004
```

### HTTP/HTTPS C2 Indicators

- Connections to newly registered domains (< 30 days)
- High volume POST requests with encoded payloads
- Unusual or spoofed User-Agent strings
- Consistent payload sizes indicating beaconing
- Direct IP connections without DNS resolution

### Network Traffic Analysis

- Extract PCAP data for suspicious connections
- Analyze protocol patterns and payload characteristics
- Identify beaconing intervals and data transfer volumes
- Map communication timeline for incident scoping

## Threat Intelligence Integration

### Recommended C2 Feeds

| Source | Endpoint | Update Frequency |
|--------|----------|------------------|
| Bambenek C2 Master List | osint.bambenekconsulting.com/feeds/c2-masterlist.txt | Daily |
| Feodo Tracker | feodotracker.abuse.ch/blocklist/ | Hourly |
| C2IntelFeeds | C2IntelFeeds/feeds/IPC2s-30day.csv | Daily |
| Abuse.ch ThreatFox | threatfox.abuse.ch | Continuous |
| MontySecurity C2-Tracker | github.com/montysecurity/C2-Tracker | Daily |

### IOC Management

- **Expiration policy**: 24-48 hours for dynamic C2 infrastructure
- **Confidence scoring**: Apply risk scores from threat intelligence platforms
- **Multi-source validation**: Verify IOCs against 2+ sources before blocking

## Response Procedures

### Containment Actions

1. **Network isolation** via EDR or switch port disable
2. **Perimeter blocking** of C2 IP/domain at firewall
3. **DNS sinkholing** for malicious domains under DNS control
4. **Account disable** for compromised user credentials

### Eradication Steps

1. Identify all malware artifacts on affected systems
2. Remove persistence mechanisms (scheduled tasks, registry, services)
3. Reset compromised credentials across all systems
4. Verify no remaining C2 connections

## Performance Metrics

### Detection KPIs

| Metric | Target |
|--------|--------|
| Mean Time to Detect (MTTD) | < 1 hour |
| C2 IOC match rate | > 95% |
| False positive rate | < 10% |

### Response KPIs

| Metric | Target |
|--------|--------|
| Mean Time to Contain (MTTC) | < 30 minutes |
| Mean Time to Eradicate (MTTE) | < 4 hours |
| IOC blocking coverage | 100% |

## References

- [MITRE ATT&CK TA0011 - Command and Control](https://attack.mitre.org/tactics/TA0011/)
- [MITRE D3FEND Countermeasures](https://d3fend.mitre.org/)
- SOP-MITRE-TA0011-Command-and-Control.md
