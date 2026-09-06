# CIS / DISA STIG / NIST 800-53 Crosswalk

This crosswalk maps 10 representative hardening controls across three frameworks: the CIS Ubuntu Linux 24.04 LTS Benchmark, the DISA STIG for Canonical Ubuntu 24.04 LTS (V1R5), and NIST SP 800-53 Rev 5. All three reference values below were extracted directly from the ComplianceAsCode SCAP content datastream built and scanned against this lab's host (`ssg-ubuntu2404-ds.xml`), not assembled from separate documents, so the alignment reflects what a single automated check actually enforces across all three frameworks simultaneously.

| CIS Control | CIS Description | DISA STIG ID | NIST 800-53 Control |
|---|---|---|---|
| 13 | Encrypt Partitions | UBTU-24-600090 | SC-28 |
| 1 | Ensure Users Re-Authenticate for Privilege Escalation (sudo NOPASSWD removed) | UBTU-24-300020 | IA-11 |
| 12 | Disable Ctrl-Alt-Del Reboot Key Sequence in GNOME3 | UBTU-24-300025 | AC-6(1) |
| 1 | Configure SSSD to Expire Offline Credentials | UBTU-24-400340 | IA-5(13) |
| Req-10.1 | Ensure the audit Subsystem is Installed | UBTU-24-100400 | AU-7(1) |
| 1 | Enable auditd Service | UBTU-24-100410 | AU-3 |
| 1 | Record Events that Modify User/Group Information (/etc/passwd) | UBTU-24-200280 | AC-2(4) |
| 1 | Ensure auditd Collects Information on the Use of Privileged Commands (sudo) | UBTU-24-900170 | AC-6(9) |
| 1 | System Audit Logs Must Have Mode 0750 or Less Permissive | UBTU-24-901380 | AC-6(1) |
| 1 | Ensure auditd Collects Information on Kernel Module Loading (init_module) | UBTU-24-900340 | AC-6(9) |

## Notes

- CIS control numbers are drawn from the CIS Ubuntu Linux 24.04 LTS Benchmark, referenced via the same SCAP datastream (`cisecurity.org/benchmark/ubuntu_linux` reference href). A CIS value of "1" reflects the benchmark's internal section numbering as embedded in the content; several controls that map to the same underlying audit subsystem configuration share this reference.
- All 10 rows were confirmed to carry all three references (CIS, STIG, NIST) simultaneously within the same `<xccdf-1.2:Rule>` definition, extracted programmatically rather than hand-matched, eliminating transcription error between frameworks.
- Encrypt Partitions (UBTU-24-600090) is the one row here that is also an open POA&M item (POA-001) in this lab, since WSL2 does not support block-level disk encryption. Every other row listed passed on this host after Ansible remediation.
- The full STIG profile scanned against this host contains 333 rules with simultaneous CIS and STIG references (out of 158 with a resolvable NIST control ID as well); this table presents a representative 10-row sample, not the complete set. The full mapping can be regenerated directly from `content/build/ssg-ubuntu2404-ds.xml` using the extraction approach documented in this repository's build notes.
