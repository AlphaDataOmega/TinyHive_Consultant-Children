# Cloud Security Engineer Documentation

## Overview

This directory contains reference materials and procedures for the Cloud Security Engineer consultant agent. The agent specializes in securing AWS, Azure, and container environments with expertise in incident response, threat detection, and identity management.

## Core Competencies

### AWS Security
- **GuardDuty** — Threat detection service for monitoring malicious activity and unauthorized behavior
- **CloudTrail** — API logging and analysis for security investigation and compliance
- **IAM Security** — Access key management, role session revocation, permission boundaries
- **Security Hub** — Centralized security findings aggregation and compliance monitoring

### Azure Security
- **Azure Security Center** — Unified security management and threat protection
- **Authorization Monitoring** — Critical event tracking for role assignments and privilege escalation
- **Azure RBAC** — Role-based access control and custom role management

### Container Security
- **EKS/AKS/GKE** — Managed Kubernetes security configuration and monitoring
- **Network Policies** — Pod isolation and traffic control for incident containment
- **Container Forensics** — Volatile artifact capture and privileged container detection

### Storage Security
- **S3 Security** — Block Public Access, encryption, versioning, access logging
- **Azure Blob** — Storage account security and access control
- **Data Protection** — Encryption at rest, in transit, and access monitoring

## Key Procedures

### Credential Compromise Response
1. Evidence acquisition from GuardDuty/CloudTrail
2. Stakeholder notification and war room establishment
3. Credential containment (disable keys, revoke sessions)
4. CloudTrail analysis for all post-compromise API calls
5. Eradication of unauthorized resources
6. Recovery and lessons learned

### Kubernetes Incident Response
1. Identify affected cluster, pod, and node
2. Apply network policy for pod isolation
3. Cordon worker node to prevent new pods
4. Enable termination protection on instance
5. Capture volatile forensic artifacts
6. Label node for investigation tracking

### S3 Exposure Remediation
1. Enable Block All Public Access immediately
2. Modify bucket policy to remove unauthorized principals
3. Update object ACLs to remove public grants
4. Enable encryption and access logging
5. Review CloudTrail data events for access history

## Reference Documents

- AWS Security Incident Response Guide
- AWS GuardDuty Finding Types Documentation
- AWS EKS Best Practices Security Guide
- Azure Authorization API Reference
- NIST SP 800-61 Computer Security Incident Handling Guide
- CIS Benchmarks for AWS/Azure/Kubernetes
- MITRE ATT&CK Cloud Matrix

## Related SOPs

- Cloud Security SOP (`/home/ubuntu/TinyHive-sops/cloud_security_sop.md`)
