# Incident Commander Specialist - Documentation

## Overview

This documentation supports the Incident Commander Specialist consultant agent, providing comprehensive guidance for cybersecurity incident command, war room management, stakeholder communication, resource coordination, and decision-making during security incidents.

## Core Competencies

### 1. Incident Commander Role and Authority

**Primary Responsibilities:**
- Single source of truth and decision authority during incidents
- Strategic direction for incident response
- Team coordination and resource allocation
- Communication control and approval
- Escalation management

**Core IC Motto:**
> "The Incident Commander coordinates and decides; the team executes."

**Do Not:**
- Perform technical investigation tasks directly
- Execute remediation actions yourself
- Bypass the command structure
- Make technical changes without team coordination

### 2. Incident Command Structure

```
                    Incident Commander (IC)
                              |
      +-----------------+-----+------+------------------+
      |                 |            |                  |
 Deputy IC           Scribe      SME Team         Liaison Team
      |                 |            |                  |
Parallel work      Timeline &   Technical         Internal &
coordination       documentation execution      External comms
```

**Deputy Incident Commander:**
- Tracks parallel workstreams
- Assumes IC role if primary unavailable
- Coordinates cross-team dependencies
- Supports IC decision-making

**Scribe:**
- Documents all IC decisions and rationale
- Maintains detailed incident timeline
- Records response call notes
- Tracks action items and ownership

**Subject Matter Experts (SMEs):**
- Execute technical investigation and remediation
- Provide recommendations to IC
- Report findings and progress
- Escalate technical blockers

**Liaison Team:**
- Manages internal/external communications (IC pre-approved)
- Coordinates with Legal, HR, Compliance
- Handles regulatory notifications

### 3. Incident Declaration and Classification

**Automatic Incident Declaration Triggers:**
- Confirmed data breach
- Ransomware infection
- Confirmed APT activity
- Widespread compromise
- Critical system impact
- Insider threat
- Supply chain compromise
- Regulatory notification required
- Executive visibility required
- Public disclosure

**Incident Severity Matrix:**

| Functional Impact | Informational Impact | Incident Severity |
|-------------------|---------------------|-------------------|
| High | Integrity Loss / Proprietary Breach | **CRITICAL** |
| High | Privacy Breach | **CRITICAL** |
| Medium | Proprietary Breach / Integrity Loss | **HIGH** |
| Medium | Privacy Breach | **HIGH** |
| High | None | **HIGH** |
| Low | Proprietary Breach | **MEDIUM** |
| Low | Privacy Breach | **MEDIUM** |
| Medium | None | **MEDIUM** |
| Low | None | **LOW** |

**Functional Impact Levels:**
- **None:** No impact to services
- **Low:** Minimal impact, normal operations continue
- **Medium:** Loss of effectiveness in providing services
- **High:** Unable to provide critical services

**Informational Impact Levels:**
- **None:** No information compromised
- **Privacy Breach:** PII compromised
- **Proprietary Breach:** Trade secrets, IP compromised
- **Integrity Loss:** Data altered or destroyed

### 4. War Room Management

**Physical War Room Requirements:**
- Dedicated secure conference room
- Multiple monitors/displays
- Whiteboards for tracking
- Secure network connections
- Phone/video conferencing
- Access control and sign-in log

**Virtual War Room Requirements:**
- Secure video conferencing (dedicated bridge)
- SIRP for case management
- Secure document repository
- Real-time collaboration tool
- Dashboard/SIEM access

**Out-of-Band Communications:**
- Personal mobile phones
- Separate collaboration platform (not corporate)
- Signal/WhatsApp with verified identities
- Pre-established external conference bridges

**When to Use Out-of-Band:**
- Planning remediation activities
- Discussing containment strategies
- Coordinating simultaneous response actions
- Communications about attacker TTPs or IOCs

### 5. Response Call Structure

**Initial Response Call Agenda (50 minutes):**
1. Call to Order (2 min) - IC establishes command, roll call
2. Situation Overview (5 min) - What happened, when, current impact
3. Technical Briefing (10 min) - Technical details, evidence, IOCs
4. Investigation Plan (10 min) - Key questions, priorities, resources
5. Containment Strategy (10 min) - Immediate actions, risks, timing
6. Action Items and Ownership (5 min) - Tasks, deadlines, next call
7. Communication Plan (3 min) - Stakeholder notifications
8. Questions and Close (5 min) - Open forum, confirm assignments

**Update Call Frequency:**
- **Critical incidents:** Every 4-6 hours minimum
- **High incidents:** Every 8-12 hours
- **Medium incidents:** Daily
- **Low incidents:** As needed

**Update Call Agenda (45 minutes):**
1. Roll Call (1 min)
2. Actions Completed Since Last Call (10 min)
3. New Findings (10 min)
4. Updated Impact Assessment (5 min)
5. Next Actions and Ownership (10 min)
6. Blockers and Escalations (5 min)
7. Communication Updates (5 min)
8. Next Call Time (1 min)

### 6. War Room Artifacts

**Incident Timeline:**
- Timestamp (UTC and local)
- Event description
- Source of information
- Confidence level (confirmed, suspected, hypothesis)
- Actor (attacker vs. response)

**Action Item Tracker:**
- Action ID
- Description
- Owner
- Deadline
- Status (Not Started, In Progress, Blocked, Complete)
- Blocker details
- Completion timestamp

**Affected Systems Inventory:**
- Hostname/IP
- Asset owner/business unit
- Discovery timestamp
- Compromise indicators
- Containment status
- Remediation status

**IOC Repository:**
- File hashes (MD5, SHA1, SHA256)
- IP addresses and domains
- Email addresses
- User accounts
- Processes, registry keys, scheduled tasks

**Evidence Inventory:**
- Evidence ID and description
- Collection timestamp and method
- Collected by (name)
- Hash values
- Storage location
- Access log (chain of custody)

### 7. Stakeholder Communication

**Internal Stakeholder Matrix:**

| Stakeholder | Notification Timing | Information Level |
|-------------|---------------------|-------------------|
| CISO | Immediate for Critical/High | Full technical + business |
| CTO/CIO | Within 2 hours for Critical/High | Technical + business |
| CEO/Board | Critical or regulatory impact | Business impact focus |
| Legal | Legal/regulatory implications | Full details, evidence |
| Compliance | Regulatory notification required | Full details for filing |
| HR | Insider threat | Need-to-know only |
| IT Operations | System impact | Technical requirements |
| Business Unit Leaders | Impact to their operations | Business continuity info |

**Communication Templates:**

**Initial Incident Declaration:**
```
INCIDENT NOTIFICATION
Incident ID: [ID]
Severity: [Critical/High/Medium/Low]
Declared: [Timestamp]
Incident Commander: [Name, Contact]

SUMMARY: [2-3 sentence description]

IMPACT:
Functional Impact: [None/Low/Medium/High]
Informational Impact: [None/Privacy/Proprietary/Integrity]
Affected Systems: [Count or description]

CURRENT STATUS: [Brief description of response]
NEXT UPDATE: [Timestamp]
```

**Status Update Template:**
```
INCIDENT STATUS UPDATE
Incident ID: [ID]
Update Number: [#]
Timestamp: [Current time]

SITUATION UPDATE: [Changes since last update]
INVESTIGATION FINDINGS: [Key discoveries]
CONTAINMENT ACTIONS: [Actions taken]
CURRENT IMPACT: [Updated assessment]
NEXT STEPS: [Planned activities]
NEXT UPDATE: [Timestamp]
```

**External Communications:**
- All require IC approval + Legal + PR coordination
- Regulatory notifications (GDPR 72hr, HIPAA 60d, PCI immediate, SEC 4 business days)
- Customer notifications
- Vendor/partner notifications
- Law enforcement engagement
- ISAC information sharing with TLP markings

**Traffic Light Protocol (TLP):**
- **TLP:CLEAR:** No restrictions
- **TLP:GREEN:** Community-wide sharing
- **TLP:AMBER:** Limited sharing (organization + partners)
- **TLP:AMBER+STRICT:** Organization only
- **TLP:RED:** Personal only, no distribution

### 8. Resource Coordination

**Personnel Resources:**
- SOC Analysts (alert triage, monitoring)
- Incident Responders (investigation, forensics)
- Network Engineers (isolation, analysis)
- System Administrators (isolation, resets, patching)
- Cloud Engineers (cloud investigation)
- Application Teams (app-specific response)
- Legal, HR, Compliance (as needed)

**Shift Management (Extended Incidents):**
- 12-hour rotations preferred
- 1-hour overlap for handoff
- Mandatory 12-hour break between shifts
- Maximum 5 consecutive days
- Monitor team for fatigue

**Third-Party Engagement:**
- Incident response firms (Mandiant, CrowdStrike, Unit 42)
- Forensics specialists
- Malware analysis labs
- When: Lack expertise, exceed capacity, need independent validation

**Budget Authority:**
- **Critical Incidents:** Up to $50,000 without additional approval
- **High Incidents:** Up to $25,000 without additional approval
- **Medium/Low:** Up to $10,000 without additional approval
- Escalate to CISO/CFO for higher amounts

### 9. Decision-Making Framework

**Decision Authority Matrix:**

| Decision | IC Authority | Escalation Required |
|----------|--------------|---------------------|
| Isolate individual workstations | Yes | No |
| Isolate servers (non-critical) | Yes | No (notify stakeholders) |
| Isolate critical business systems | Yes | Yes (business owner) |
| Network-wide containment | Yes | Yes (CISO) |
| Disable user accounts | Yes | No (notify managers) |
| Mass credential resets | Yes | Yes (CISO + IT leadership) |
| Engage external IR firm | No | Yes (CISO + CFO) |
| Public communications | No | Yes (CEO + Legal + PR) |
| Law enforcement | No | Yes (Legal + CISO) |

**OODA Loop Decision Process:**
1. **Observe:** Gather current situation data
2. **Orient:** Analyze in context, evaluate options
3. **Decide:** Select course of action, document rationale
4. **Act:** Direct execution, monitor, adjust

**Containment Strategies:**

**Immediate Containment (Minutes):**
- Block malicious IPs/domains
- Disable compromised accounts
- Isolate infected workstations
- Kill malicious processes

**Short-Term Containment (Hours):**
- Isolate compromised servers
- Network segmentation
- Reset credentials
- Patch vulnerabilities

**Long-Term Containment (Days):**
- Rebuild systems
- Architecture changes
- Enhanced detection
- Long-term monitoring

**Containment Timing:**
- **Simultaneous Coordinated:** Preferred, prevents attacker evasion
- **Phased:** When coordination difficult, staged approach
- **Delayed:** When observation provides intelligence value

### 10. Escalation Procedures

**Escalation Timing:**
- **Critical:** CISO within 15 min, Executive within 1 hour
- **High:** CISO within 1 hour, Executive within 4 hours
- **Medium:** CISO within 4 hours, Executive if business impact
- **Low:** CISO next business day, Executive not required

**Escalation Path:**
```
Incident Commander
        |
        v
CISO / Security Director
        |
        +-- Business Impact --> CTO/CIO
        +-- Legal Impact --> General Counsel
        +-- Financial Impact --> CFO
        +-- Public Impact --> CEO --> Board
```

**Escalation Call Outline:**
1. Identification: "This is [IC Name], Incident Commander for [ID]"
2. Situation: What, when, current impact (30 sec)
3. Assessment: Scope, cause, status (30 sec)
4. Decision Needed: Specific ask, impact, risk, timeline (30 sec)
5. Next Steps: Follow-up actions, next update

### 11. Status Reporting

**Executive Status Report (1-2 pages):**
- Executive Summary
- Timeline (detection, declaration, elapsed, estimated resolution)
- Impact Assessment
- Current Status
- Key Findings
- Actions Taken
- Next Steps
- Resource Status
- Risks and Concerns

**Response Metrics:**
- **MTTD:** Mean Time to Detect (attacker action to detection)
- **MTTT:** Mean Time to Triage (detection to declaration)
- **MTTC:** Mean Time to Contain (declaration to containment)
- **MTTE:** Mean Time to Eradicate (containment to eradication)
- **MTTR:** Mean Time to Recover (eradication to recovery)

**Board-Level Brief (5-10 slides):**
1. Executive Summary
2. Timeline
3. Business Impact
4. Response Actions
5. Root Cause
6. Risk Mitigation
7. Lessons Learned
8. Open Items
9. Q&A

### 12. Incident Closure Criteria

**All Criteria Must Be Met:**

**Technical:**
- [ ] Investigation complete (root cause, timeline, all systems/accounts)
- [ ] Containment complete (access revoked, processes terminated)
- [ ] Eradication complete (malware removed, persistence cleared, credentials reset)
- [ ] Recovery complete (systems restored, services operational, data validated)
- [ ] Validation complete (no attacker activity for 7-14 days)

**Business:**
- [ ] Operations returned to normal
- [ ] Stakeholders satisfied
- [ ] Regulatory notifications completed

**Documentation:**
- [ ] Incident file complete with evidence
- [ ] Timeline finalized
- [ ] IOCs documented in TIP
- [ ] MITRE ATT&CK mapping complete

**Communication:**
- [ ] All stakeholders notified of closure
- [ ] Final status report distributed
- [ ] After-action review scheduled

**Closure Process:**
1. IC reviews closure checklist
2. Stakeholder validation (CISO, business units, legal, compliance)
3. Monitoring validation period (7-14 days)
4. Final approval from CISO
5. IC formally closes incident
6. Closure notification to all stakeholders

### 13. Post-Incident Handoff

**Final Incident Report Structure:**
1. Executive Summary (1 page)
2. Incident Details (2-3 pages)
3. Attacker Timeline (2-5 pages)
4. Response Timeline (2-5 pages)
5. Technical Analysis (5-10 pages)
6. Root Cause Analysis (2-3 pages)
7. Response Metrics (1-2 pages)
8. Lessons Learned (2-3 pages)
9. Recommendations (2-3 pages)
10. Appendices (IOCs, evidence, communications, costs)

**After-Action Review (AAR):**
- **Timing:** Within 7-14 days of closure
- **Duration:** 60-120 minutes
- **Facilitator:** IC or independent facilitator
- **Attendees:** All response participants, stakeholders, management

**AAR Agenda:**
1. Introduction (5 min) - Blameless culture reminder
2. Incident Overview (10 min) - Summary and timeline
3. What Went Well (20 min) - Effective processes, good decisions
4. What Could Be Improved (30 min) - Process gaps, delays, issues
5. Root Cause Discussion (15 min) - Why it occurred, control failures
6. Recommendations and Action Items (20 min) - Improvements, ownership
7. Closing (5 min) - Summary, next steps, appreciation

**Improvement Action Categories:**
- **Process:** Procedure updates, playbook revisions
- **Technology:** Tool deployment, configuration changes
- **Training:** Awareness programs, skill development
- **Policy:** Policy updates, control changes
- **Architecture:** Design changes, network segmentation

**Handoffs:**
- **SOC:** Enhanced monitoring plan, IOC list, detection rules
- **Detection Engineering:** New SIEM rules for observed TTPs
- **IT Operations:** System hardening, patching requirements
- **Compliance:** Regulatory documentation, audit support
- **Finance:** Final cost summary, insurance claims
- **Training:** Awareness updates, tabletop scenarios

**Enhanced Monitoring Period:**
- Duration: 30-90 days post-closure
- IOC monitoring in SIEM/TIP
- Behavioral monitoring for similar TTPs
- Threat hunting for related activity
- Daily review initially, weekly after 30 days

## Reference Frameworks

- **NIST SP 800-61 Rev 3:** Computer Security Incident Handling Guide
- **MITRE ATT&CK:** Framework for incident mapping
- **PICERL Framework:** Preparation, Identification, Containment, Eradication, Recovery, Lessons Learned
- **ISO/IEC 27035:** Information Security Incident Management
- **FIRST CSIRT Services Framework**

## Key Documentation

- Incident Commander SOP: `/home/ubuntu/TinyHive-sops/cybersecurity/incident_commander_sop.md`
- Incident Response Playbooks SOP
- SOC Best Practices SOP
- Data Exfiltration IRP

## Essential Skills

- Incident command and control
- Crisis communication
- Rapid decision-making under pressure
- Resource management and coordination
- Stakeholder management
- Technical security understanding
- MITRE ATT&CK framework
- NIST SP 800-61 framework
- Legal and regulatory awareness
- After-action review facilitation

## Common Mistakes to Avoid

1. **IC Performing Technical Tasks:** Delegate to SMEs, don't investigate yourself
2. **Premature Containment:** Plan and coordinate before executing
3. **Poor Communication:** Update stakeholders on committed schedule
4. **Decision Without Coordination:** Don't act without team input and coordination
5. **Premature Closure:** Validate all criteria before closing
6. **Skipping AAR:** Always conduct after-action review
7. **Using Compromised Communications:** Use out-of-band during active incidents
8. **Failing to Document:** Document all decisions and rationale

## Related Agents

- `incident_response_lead`: Overall IR lifecycle and PICERL framework execution
- `soc_operations_manager`: SOC management, detection engineering, SOAR
- `incident_playbook_specialist`: Incident-specific playbooks and threat response
- `malware_response_analyst`: Malware analysis and remediation
- `soc_analyst`: SOC operations, alert triage, detection
- `threat_intel_manager`: Threat intelligence program management
