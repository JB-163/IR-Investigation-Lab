# Incident Response Investigation Report — Investigation 02

**Date of Analysis:** July 2026

**Exercise Source:** Malware-Traffic-Analysis.net — 2025-01-22

**Exercise Title:** Download from Fake Software Site

**PCAP File:** 2025-01-22-traffic-analysis-exercise.pcap

---

## Scenario

A SOC analyst received a report from a colleague that a coworker downloaded a suspicious file after searching for Google Authenticator online. Initial information confirmed an infection had occurred. A packet capture of the associated traffic was 
retrieved for full investigation to identify the infected host, delivery mechanism, and post-infection C2 infrastructure.

---

## Infected Host Identification

| Field | Value |
|-------|-------|
| IP Address | 10.1.17.215 |
| MAC Address | 00:d0:b7:26:4a:74 |
| Hostname | DESKTOP-L8C5GSJ |
| User Account | shutchenson |

---

## Threat Identification

| Field | Value |
|-------|-------|
| Delivery Method | Typosquatting — fake Google Authenticator site |
| Phishing Domain | authenticatoor[.]org |
| C2 IP 1 | 5.252.153[.]241 |
| C2 IP 2 | 45.125.66[.]32 |
| C2 IP 3 | 45.125.66[.]252 |
| C2 IP 4 | 82.221.136[.]26 |
| VirusTotal Status | All C2 IPs flagged malicious |

---

## Attack Chain Reconstruction

```
User searches "Google Authenticator download"
        ↓
Malicious ad serves fake download site
        ↓
User visits authenticatoor[.]org (typosquatting domain)
        ↓
User downloads and executes malicious file
        ↓
Malware establishes C2 communication with 4 servers
        ↓
Fallback channel behavior — multiple C2 IPs for resilience
```

---

## Investigation Methodology

**Step 1 — Protocol Hierarchy and Conversation Analysis:**
Reviewed traffic composition and identified external IPs with sustained connections from infected internal host 10.1.17.215.

**Step 2 — Phishing Domain Identification:**
Traced pre-infection HTTP traffic to identify the fake software delivery site. Identified authenticatoor[.]org as the typosquatting domain impersonating Google Authenticator, deliberate double "o" designed to evade casual inspection by users.

**Step 3 — C2 Infrastructure Identification:**
Applied filters to isolate post-infection traffic and identified 4 separate external C2 IPs. Multiple C2 servers indicate deliberate fallback channel architecture. If one IP is blocked, malware switches to another automatically.

**Step 4 — Threat Intelligence Enrichment:**
Verified all 4 C2 IPs individually on VirusTotal. All confirmed malicious with multiple vendor detections.

**Step 5 — Host Identification:**
Identified infected host through conversation analysis, MAC address extraction via Ethernet II frame, hostname via NBNS traffic, and username via KERBEROS authentication packets.

---

## Containment Recommendations

1. Isolate DESKTOP-L8C5GSJ from network immediately
2. Reset credentials for user account shutchenson
3. Block all 4 C2 IPs at perimeter firewall
4. Block domain authenticatoor[.]org at DNS/proxy level
5. Search proxy logs for other internal hosts visiting authenticatoor[.]org and identify any additional infections
6. Issue internal security advisory warning staff about fake software download sites and typosquatting domains
7. Run full endpoint scan on infected machine

---

## Evidence Screenshots

| Screenshot | Description |
|------------|-------------|
| inv2_infected_ip | Wireshark showing infected host IP 10.1.17.215 |
| inv2_infected_mac | MAC address 00:d0:b7:26:4a:74 extracted |
| inv2_infected_hostname | Hostname DESKTOP-L8C5GSJ from DHCP traffic |
| inv2_infected_username | Username shutchenson from NTLMSSP traffic |
| inv2_fakedomain_name | authenticatoor[.]org identified in HTTP traffic |
| inv2_c2ip_1 | C2 IP 5.252.153[.]241 |
| inv2_c2ip_2_3 | C2 IPs 45.125.66[.]32 and 45.125.66[.]252 |
| inv2_c2ip_4 | C2 IP 82.221.136[.]26 |
| inv2_virustotal_result1 | VirusTotal result — C2 IP 1 |
| inv2_virustotal_result2 | VirusTotal result — C2 IP 2 |
| inv2_virustotal_result3 | VirusTotal result — C2 IP 3 |
| inv2_virustotal_result4 | VirusTotal result — C2 IP 4 |
