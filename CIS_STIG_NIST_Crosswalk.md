# CIS / DISA STIG / NIST 800-53 Crosswalk

This crosswalk maps 10 representative hardening controls across three frameworks: the CIS Ubuntu Linux 24.04 LTS Benchmark, the DISA STIG for Canonical Ubuntu 24.04 LTS (V1R5), and NIST SP 800-53 Rev 5. The reference values below were extracted directly from the ComplianceAsCode SCAP content datastream built and scanned against this lab's host (`ssg-ubuntu2404-ds.xml`), so each row reflects what a single automated check enforces across all three frameworks.

| CIS Control | CIS Description | DISA STIG ID | NIST 800-53 Control |
|---|---|---|---|
| 13 | Encrypt Partitions | UBTU-24-600090 | SC-28 |
| 1 | Ensure Users Re-Authenticate for Privilege Escalation (sudo NOPASSWD removed) | UBTU-24-300020 | IA-11 |
| 12 | Disable Ctrl-Alt-Del Reboot Key Sequence in GNOME3 | UBTU-24-300025 | AC-6(1) |
| 1 | Configure SSSD to Expire Offline Credentials | UBTU-24-400340 | IA-5(13) |
| Not captured | Ensure the audit Subsystem is Installed | UBTU-24-100400 | AU-7(1) |
| 1 | Enable auditd Service | UBTU-24-100410 | AU-3 |
| 1 | Record Events that Modify User/Group Information (/etc/passwd) | UBTU-24-200280 | AC-2(4) |
| 1 | Ensure auditd Collects Information on the Use of Privileged Commands (sudo) | UBTU-24-900170 | AC-6(9) |
| 1 | System Audit Logs Must Have Mode 0750 or Less Permissive | UBTU-24-901380 | AC-6(1) |
| 1 | Ensure auditd Collects Information on Kernel Module Loading (init_module) | UBTU-24-900340 | AC-6(9) |

## Notes

- CIS control numbers are drawn from the CIS Ubuntu Linux 24.04 LTS Benchmark, referenced via the same SCAP datastream (`cisecurity.org/benchmark/ubuntu_linux` reference href). A CIS value of "1" reflects the benchmark's internal section numbering as embedded in the content; several controls that map to the same underlying audit subsystem configuration share this reference.
- The rows were extracted programmatically from the same `<xccdf-1.2:Rule>` definition rather than hand-matched across frameworks.
- The CIS value for "Ensure the audit Subsystem is Installed" (UBTU-24-100400) was originally listed as "Req-10.1". That is the rule's PCI-DSS reference (`PCI-DSS-Req-10.1` in the tags of `stig_remediation.yml`), not a CIS section number. The CIS value has not been re-extracted from the datastream, so the cell is marked as not captured.
- Encrypt Partitions (UBTU-24-600090) is the one row here that is also an open POA&M item (POA-001) in this lab, since WSL2 does not support block-level disk encryption. Every other row listed passed on this host after Ansible remediation.
- In the full STIG profile, 333 rules carry both CIS and STIG references, and 158 of those also carry a resolvable NIST control ID. This table is a 10-row sample of that set. The full mapping can be regenerated from `content/build/ssg-ubuntu2404-ds.xml`, which is built from ComplianceAsCode source and not committed.
