# System Security Plan Summary

## System Name

FedRAMP-RMF Compliance Lab (fedramp-rmf-lab)

## System Description

The system is a single Ubuntu 24.04 LTS server, deployed as a WSL2 instance, built to demonstrate a full Risk Management Framework (RMF) authorization cycle against a FedRAMP Moderate baseline. The server hosts no external services and is used exclusively for compliance scanning, hardening, and documentation exercises. Its function is to serve as the assessment target for OpenSCAP STIG scanning, Ansible-based remediation, and downstream POA&M and FedRAMP control mapping.

The system boundary is limited to the operating system and its installed packages. No network-facing application, database, or externally accessible service runs on this host.

## System Categorization (FIPS 199)

| Security Objective | Categorization | Rationale |
|---|---|---|
| Confidentiality | Moderate | System contains configuration and compliance data of moderate sensitivity; no regulated data (PII, PHI, CUI) is processed or stored. |
| Integrity | Moderate | Unauthorized modification of hardening configuration or scan results would undermine the reliability of compliance reporting. |
| Availability | Low | System is a standalone lab environment with no operational dependency; downtime has no mission impact. |

**Overall system categorization: Moderate**, driven by the high-water mark across the three objectives, consistent with a FedRAMP Moderate baseline scope.

## NIST SP 800-53 Rev 5 Moderate Baseline: Control Family Implementation Status

| Family | Name | Implementation Status |
|---|---|---|
| AC | Access Control | Partially Implemented |
| AT | Awareness and Training | Not Applicable |
| AU | Audit and Accountability | Partially Implemented |
| CA | Assessment, Authorization, and Monitoring | Implemented |
| CM | Configuration Management | Implemented |
| CP | Contingency Planning | Not Applicable |
| IA | Identification and Authentication | Partially Implemented |
| IR | Incident Response | Not Applicable |
| MA | Maintenance | Not Applicable |
| MP | Media Protection | Not Applicable |
| PE | Physical and Environmental Protection | Not Applicable |
| PL | Planning | Implemented |
| PM | Program Management | Not Applicable |
| PS | Personnel Security | Not Applicable |
| PT | PII Processing and Transparency | Not Applicable |
| RA | Risk Assessment | Implemented |
| SA | System and Services Acquisition | Not Applicable |
| SC | System and Communications Protection | Partially Implemented |
| SI | System and Information Integrity | Partially Implemented |
| SR | Supply Chain Risk Management | Not Applicable |

**Notes on status determinations:**

- **Implemented**: control is fully satisfied by the current OpenSCAP STIG scan results and Ansible remediation, with no open POA&M items in that family.
- **Partially Implemented**: control is largely satisfied, but one or more open POA&M items (see POAM.xlsx) remain within that family. For example, AC and IA carry open findings related to SSH client cipher restrictions (UBTU-24-100850) and SSSD certificate trust configuration (UBTU-24-400360, UBTU-24-400370).
- **Not Applicable**: control family addresses organizational, physical, personnel, or supply chain processes that fall outside the scope of a single technical lab host and would be addressed at the organization level in a production FedRAMP authorization, not re-derived here.

This status table reflects the OpenSCAP STIG evaluation (Canonical Ubuntu 24.04 LTS STIG V1R5, profile `xccdf_org.ssgproject.content_profile_stig`) performed against this host before and after Ansible remediation, and the resulting POA&M in POAM.xlsx.

## FedRAMP Control Inheritance Table

| Control Area | Inherited From Cloud Provider | Customer Responsible | Notes |
|---|---|---|---|
| Physical and Environmental Protection (PE) | N/A (self-hosted lab) | N/A | Lab runs on local hardware under WSL2; not applicable to a cloud-hosted FedRAMP boundary. |
| Network Perimeter and Boundary Protection | Yes (in a production FedRAMP deployment) | Partial | In a production deployment, perimeter firewalling would be inherited from the CSP; host-based firewall (ufw) configuration remains customer responsibility. |
| Operating System Hardening (STIG/CIS) | No | Yes | Full customer responsibility, demonstrated in this lab via OpenSCAP scanning and Ansible remediation. |
| Identity and Access Management (IAM policy) | Partial | Yes | Underlying IAM platform availability may be inherited from a CSP; account provisioning, password policy, and PAM configuration are customer responsibility, as evidenced by findings in this lab. |
| Audit Logging Infrastructure | Partial | Yes | Log storage/retention infrastructure may be inherited; audit rule configuration and content are customer responsibility. |
| Disk Encryption at Rest | Partial | Yes | In a production cloud deployment, storage-layer encryption is often CSP-managed; OS-level partition encryption remains customer responsibility. This lab's WSL2 environment does not support block-level encryption, which is documented as an accepted-risk POA&M item (POA-001). |
| Configuration Management Tooling | No | Yes | Ansible playbook and STIG remediation content developed and executed entirely by the customer (system owner) in this lab. |
| Vulnerability Scanning | No | Yes | OpenSCAP scanning performed directly against the host by the system owner. |

This table reflects a customer-responsible technical hardening exercise. In a FedRAMP Moderate authorization on a CSP platform (AWS GovCloud, Azure Government, etc.), a larger share of physical, environmental, and infrastructure-level controls would be inherited; those inheritance claims are not asserted here since this system does not run on a FedRAMP-authorized cloud platform.

## Summary of Assessment Results

- Baseline STIG scan: 28 passed, 11 failed, 2 not checked (69.58% score)
- Post-remediation STIG scan: 38 passed, 7 failed, 2 not checked (78.06% score)
- Ansible remediation applied 13 configuration changes across the STIG profile
- 7 remaining findings tracked in POAM.xlsx with STIG finding IDs, risk levels, and target completion dates

See POAM.xlsx for the full remediation tracking detail and FedRAMP_Control_Matrix.xlsx for the control-by-control FedRAMP Moderate mapping.
