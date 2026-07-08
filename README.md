# PCAP-Based Malware Traffic Analysis & IR Reporting

A home Incident Response lab conducting real-world malware traffic 
investigations using network packet captures sourced from 
Malware-Traffic-Analysis.net. Each investigation follows a 
structured SOC analyst workflow — from initial SIEM alert context 
through host identification, IOC extraction, threat intelligence 
enrichment, MITRE ATT&CK mapping, and formal IR reporting.

---

## Lab Environment

| Component | Details |
|-----------|---------|
| Analysis Tool | Wireshark |
| Threat Intelligence | VirusTotal, AbuseIPDB |
| Attack Framework | MITRE ATT&CK Enterprise |
| PCAP Source | Malware-Traffic-Analysis.net |
| OS | Windows 11 |

---

## Investigations

| # | Date | Malware Family | Delivery Method | C2 IPs Found |
|---|------|---------------|-----------------|--------------|
| 1 | 2026-02-28 | NetSupport Manager RAT | Direct C2 communication | 1 |
| 2 | 2025-01-22 | Unknown — Fake Software Delivery | Typosquatting phishing site | 4 |

---

## Investigation 1 — NetSupport Manager RAT

**Source:** 2026-02-28 Traffic Analysis Exercise — Easy As 123

**Summary:** SIEM flagged signature hits for NetSupport Manager 
RAT activity from an internal IP communicating with a known 
malicious external server over TCP port 443. Investigation 
identified the infected host, responsible user, and confirmed 
C2 infrastructure using VirusTotal.

**Key Findings:**
- Infected Host: 10.2.28.88 (DESKTOP-TEYQ2NR)
- User: Becka Rolf (brolf)
- C2 Server: 45.131.214[.]85
- Malware: NetSupport Manager RAT

[Full Report](investigation-01/investigation_report.md) | 
[IOC List](investigation-01/ioc_list.md)

---

## Investigation 2 — Fake Google Authenticator Phishing Campaign

**Source:** 2025-01-22 Traffic Analysis Exercise — Download from 
Fake Software Site

**Summary:** SOC received a report of a user downloading a 
suspicious file after searching for Google Authenticator. 
Investigation traced the full attack chain from initial phishing 
lure through fake software download to post-infection C2 
communication across 4 separate C2 servers — indicating fallback 
channel behavior.

**Key Findings:**
- Infected Host: 10.1.17.215 (DESKTOP-L8C5GSJ)
- User: shutchenson
- Phishing Domain: authenticatoor[.]org (typosquatting)
- C2 Servers: 4 IPs identified
- Technique: Typosquatting + Malicious File Delivery

[Full Report](investigation-02/investigation_report.md) | 
[IOC List](investigation-02/ioc_list.md)

---

## Tools Used

| Tool | Purpose |
|------|---------|
| Wireshark | PCAP analysis, protocol filtering, stream following |
| VirusTotal | IP and domain reputation, malware vendor detections |
| MITRE ATT&CK Navigator | TTP visualization and mapping |

---

## Skills Demonstrated

- Network packet capture analysis using Wireshark
- Protocol-level investigation — DHCP, NTLMSSP, HTTP, DNS, Kerberos
- Infected host identification — IP, MAC, hostname, username
- IOC extraction and defanging
- Threat intelligence enrichment using open-source platforms
- Typosquatting domain identification
- Multi-stage attack chain reconstruction
- MITRE ATT&CK TTP mapping
- Formal incident response report writing
- IOC list production for operational use

---

## Screenshots

All investigation evidence screenshots are organized by 
investigation in the [screenshots](screenshots/) folder.
