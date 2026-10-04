# Security Onion SOC Lab

This repository documents hands-on security operations investigations performed in an isolated cybersecurity training lab using Security Onion, Suricata, Zeek, Hunt, packet capture, MITRE ATT&CK, and AI-assisted analysis.

The objective is to practice the complete analyst workflow:

**Detection → Investigation → Evidence Validation → Analyst Judgment → Response/Remediation → Documentation**

Exercises include known synthetic test traffic, controlled attack simulations against intentionally vulnerable systems, and analyst-blind investigations.

All offensive or suspicious activity documented in this repository is generated within an isolated training environment or obtained from legitimate cybersecurity training datasets.

## Investigations

Selected SOC investigations demonstrating alert triage, network/log analysis, evidence validation, MITRE ATT&CK mapping, and analyst judgment:



### [Case 001 — Security Onion so-test BitTorrent Alert Investigation](investigations/case-001-so-test-bittorrent/README.md)

Known-synthetic validation exercise involving Suricata alert triage, evidence interpretation, ATT&CK hypothesis evaluation, and AI-assisted analysis.



### [Case 002 — Security Onion so-test NetBIOS Alert Investigation](investigations/case-002-so-test-gpl-netbios/README.md)

Known-synthetic validation exercise involving Suricata alert triage, evidence interpretation, ATT&CK hypothesis evaluation, and AI-assisted analysis.



### [Case 003 — Imported PCAP Investigation](investigations/case-003-pcap/README.md)

Known-synthetic validation exercise involving packet capture imports, Zeek alert triage, evidence interpretation, ATT&CK hypothesis evaluation, and AI-assisted analysis.



### [Case 004 — Metasploitable Penetration and Detection](investigations/case-004-metasploitable/README.md)

Controlled attack exercise against an imported virtual machine involving network reconnaissance, vulnerable protocol exploitation, Security Onion alert triage, and system hardening.


### [Case 005 — OWASP Juice Shop Exploitation](investigations/case-005-owasp-juice-shop/README.md)

Controlled attack exercise against an Ubuntu Server virtual machine running OWASP Juice Shop. Involves finding vulnerabilities in a web application, exploiting the vulnerabilities, and detecting the exploitation.



## Lab Architecture



[View Lab Architecture](architecture/lab-architecture.md)
