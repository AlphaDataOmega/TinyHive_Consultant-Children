# Threat Intel Manager Documentation

## Overview

This directory contains reference documentation for the Threat Intel Manager consultant, specializing in threat intelligence management, XSOAR TIM playbooks, indicator lifecycle management, SIEM distribution, and IOC enrichment.

## Core Competencies

### Indicator Types and Classification

| Type | Description | Processing Method |
|------|-------------|-------------------|
| IP Address | IPv4 and IPv6 addresses | Auto-process, check against exclusion lists |
| Domain | Fully qualified domain names | WHOIS validation, age analysis |
| URL | Full URLs including paths | Business partner list check |
| File Hash | MD5, SHA1, SHA256 hashes | Approved hash list verification |
| CIDR | IP address ranges | Size-based processing |

### Classification Tags

| Tag | Description |
|-----|-------------|
| `approved_black` | Confirmed malicious indicator |
| `approved_white` | Confirmed benign indicator |
| `approved_watchlist` | Suspicious indicator requiring monitoring |
| `pending_review` | Awaiting manual analyst review |
| `being_reviewed` | Currently under analyst review |
| `business_partner` | Belongs to business partner |
| `organizational_external_ip` | Organization's external IP |
| `approved_hash` | Verified safe file hash |
| `new_domain` | Recently registered domain |
| `no_whois_resolution` | WHOIS lookup failed |

### Reputation Scores

| Score | Reputation | Processing Action |
|-------|------------|-------------------|
| 0 | Unknown | Enrich if configured |
| 1 | Good | Tag as `approved_white` |
| 2 | Suspicious | Tag as `approved_watchlist` |
| 3 | Bad | Tag as `approved_black` |

## Processing Workflows

### Fully Automated Processing

For high-reliability threat intelligence feeds:

1. Query indicators from configured feeds
2. Execute auto-processing sub-playbook
3. Check against exclusion lists (business partners, organizational IPs, approved hashes)
4. Apply tags based on reputation score
5. Output processed indicators for downstream consumption

### Manual Review Processing

For low-confidence feeds requiring human validation:

1. Execute auto-processing sub-playbook
2. Filter business partner and organizational indicators
3. Tag remaining indicators as `pending_review`
4. Create review incident (optional)
5. Analyst claims indicators with `being_reviewed` tag
6. Apply classification after review
7. Optional approval workflow via email

## SIEM Distribution

### Prerequisites

Indicators must be:
- Tagged with: `approved_black`, `approved_white`, or `approved_watchlist`
- NOT tagged with: `pending_review`
- Status: `active` (not expired)

### Distribution Query

```
(type:ip or type:file or type:Domain or type:URL)
-tags:pending_review
and (tags:approved_black or tags:approved_white or tags:approved_watchlist)
and expirationStatus:active
```

## Enrichment Configuration

### Enrichment Sources by Type

| Indicator Type | Sources |
|----------------|---------|
| IP | Threat intel feeds, geolocation, reputation DBs, ASN info |
| Domain | WHOIS data, domain reputation, SSL certs, DNS records |
| URL | URL reputation, web categorization, malware analysis |
| File Hash | VirusTotal, malware sandboxes, internal reputation DB |

### Enrichment Controls

| Input | Description |
|-------|-------------|
| EnrichBadIndicators | Enrich indicators with score=3 |
| EnrichGoodIndicators | Enrich indicators with score=1 |
| EnrichSuspiciousIndicators | Enrich indicators with score=2 |
| EnrichUnknownIndicators | Enrich indicators with score=0 |

## Exclusion List Management

### List Types

| List Name | Content |
|-----------|---------|
| BusinessPartnersIPListName | Partner IP addresses |
| BusinessPartnersDomainListName | Partner domain names |
| BusinessPartnersURLListName | Partner URLs |
| OrganizationsExternalIPListName | Organization's external IPs |
| ApprovedHashList | Known-good file hashes |

## Operational Metrics

### Operational Targets

| Metric | Target |
|--------|--------|
| Auto-processing success rate | >99% |
| Manual review turnaround | <24 hours |
| SIEM distribution success | >99.9% |
| Enrichment coverage | >80% |

### Quality Targets

| Metric | Target |
|--------|--------|
| False positive rate | <5% |
| Indicator accuracy | >95% |
| Feed reliability score | >90% |

## XSOAR Playbook Reference

### Core Playbooks

- TIM - Process Indicators - Fully Automated
- TIM - Process Indicators - Manual Review
- TIM - Indicator Auto Processing
- TIM - Review Indicators Manually

### Processing Sub-Playbooks

- TIM - Process Indicators Against Approved Hash List
- TIM - Process Indicators Against Business Partners IP List
- TIM - Process Indicators Against Business Partners Domains List
- TIM - Process Indicators Against Business Partners URL List
- TIM - Process Indicators Against Organizations External IP List
- TIM - Process CIDR Indicators By Size
- TIM - Process Domains With Whois
- TIM - Process Domain Age With Whois
- TIM - Process Domain Registrant With Whois
- TIM - Process File Indicators With File Hash Type

### Enrichment Playbooks

- TIM - Run Enrichment For All Indicator Types
- TIM - Run Enrichment For IP Indicators
- TIM - Run Enrichment For Domain Indicators
- TIM - Run Enrichment For URL Indicators
- TIM - Run Enrichment For Hash Indicators

### SIEM Distribution Playbooks

- TIM - Add All Indicator Types To SIEM
- TIM - Add IP Indicators To SIEM
- TIM - Add Domain Indicators To SIEM
- TIM - Add URL Indicators To SIEM
- TIM - Add Bad Hash Indicators To SIEM

## Related Resources

- Source SOP: SOP-Threat-Intelligence-Management-XSOAR.md
- Platform: Cortex XSOAR 5.5.0+
