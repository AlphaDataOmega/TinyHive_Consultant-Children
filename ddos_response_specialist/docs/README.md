# DDoS Response Specialist Documentation

This directory contains reference materials and procedures for DDoS mitigation and incident response.

## Core Competencies

### Attack Types and Classification

| Category | MITRE Technique | Attack Vectors |
|----------|-----------------|----------------|
| Network DoS | T1498 | Direct Network Flood (T1498.001), Reflection Amplification (T1498.002) |
| Endpoint DoS | T1499 | OS Exhaustion (T1499.001), Service Exhaustion (T1499.002), Application Exhaustion (T1499.003), System Exploitation (T1499.004) |

### Volumetric Attack Vectors

- **UDP Flood**: High-volume UDP packets to random ports
- **ICMP Flood**: Ping requests overwhelming target
- **SYN Flood**: Half-open connections exhausting resources
- **Reflection Amplification**: DNS (28-54x), NTP (556x), Memcached (51,000x), SSDP (30x)

### Application Layer Attacks

- **HTTP GET/POST Flood**: High-volume page/form requests
- **Slowloris**: Slow, incomplete HTTP requests holding connections
- **RUDY (R-U-Dead-Yet)**: Random data in content-length field
- **SSL/TLS Exhaustion**: Expensive cryptographic operations

## Defense Architecture

```
[Internet] --> [CDN/Edge] --> [WAF] --> [Load Balancer] --> [Application]
                   |            |              |
                   v            v              v
              [DDoS Shield] [Rate Limit]  [Auto-Scale]
```

### Key Components

1. **Content Delivery Network (CDN)**: Distribute traffic, cache content, origin shield
2. **Web Application Firewall (WAF)**: Managed rules, custom rules, rate-based rules
3. **Load Balancer**: Multi-AZ deployment, health checks, connection draining
4. **Auto-Scaling**: CPU/network/request-based scaling policies

## Rate Limiting Guidelines

| Service Type | Rate Limit | Time Window | Action |
|--------------|------------|-------------|--------|
| API Endpoints | 100 req | 1 second | Block |
| Login Pages | 5 req | 1 minute | CAPTCHA |
| Static Content | 1000 req | 1 second | Throttle |
| Form Submissions | 10 req | 1 minute | Block |

## Cloud-Native Protection Services

### AWS
- **Shield Standard**: Automatic Layer 3/4 protection
- **Shield Advanced**: 24/7 DRT, cost protection, advanced metrics
- **WAF**: Web ACLs with managed and custom rules

### Azure
- **DDoS Protection Basic**: Automatic, no cost
- **DDoS Protection Standard**: Adaptive tuning, analytics, DRR support

### GCP
- **Cloud Armor**: Preconfigured WAF rules, adaptive protection (ML-based), CEL custom rules

## Incident Response Phases

### 1. Detection (0-15 minutes)
- Confirm incident is occurring
- Identify attack type and scope
- Open incident ticket
- Initiate war room if critical

### 2. Containment (15-60 minutes)
- Deploy emergency WAF rules
- Implement IP/geo blocking
- Enable rate limiting
- Scale infrastructure

### 3. Eradication (1-4 hours)
- Deploy comprehensive WAF rule sets
- Harden network configurations
- Implement application-level protections
- Coordinate with upstream providers

### 4. Recovery
- Verify attack has subsided
- Gradually reduce protective measures
- Monitor for attack resumption
- Confirm service restoration

### 5. Post-Incident
- Conduct lessons learned review
- Update documentation and runbooks
- Archive evidence
- Implement improvements

## Key Metrics to Monitor

| Category | Metrics | Threshold |
|----------|---------|-----------|
| Network | Bandwidth utilization | >80% capacity |
| Network | Packets per second | >2x baseline |
| Application | Request rate | >3x baseline |
| Application | Error rate (4xx/5xx) | >5% |
| Application | Response latency | >2x baseline |
| Infrastructure | CPU utilization | >80% |
| Infrastructure | Connection count | >75% capacity |

## Quick Reference Commands

```bash
# Check SYN flood indicators
netstat -an | grep SYN_RECV | wc -l

# Check connection states
ss -s

# Check web server connections
netstat -an | grep :443 | wc -l

# Find top requesting IPs
awk '{print $1}' access.log | sort | uniq -c | sort -rn | head -20

# Linux SYN flood protection
sysctl -w net.ipv4.tcp_syncookies=1
sysctl -w net.ipv4.tcp_max_syn_backlog=2048
```

## Related Standards

- NIST SP 800-61r2: Computer Security Incident Handling Guide
- MITRE ATT&CK: T1498 (Network DoS), T1499 (Endpoint DoS)
- AWS DDoS Resiliency Best Practices Whitepaper
- OWASP Application Security Resources
