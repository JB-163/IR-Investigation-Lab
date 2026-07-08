# IOC List — Investigation 02

**Date:** July 2026

**Source:** 2025-01-22 Traffic Analysis Exercise

**Delivery Method:** Fake Software Site — Typosquatting

---

## Network IOCs

| Type | Value | Description |
|------|-------|-------------|
| Domain | authenticatoor[.]org | Fake Google Authenticator download site — typosquatting |
| IP | 5.252.153[.]241 | C2 server 1 |
| IP | 45.125.66[.]32 | C2 server 2 |
| IP | 45.125.66[.]252 | C2 server 3 |
| IP | 82.221.136[.]26 | C2 server 4 |

## Host IOCs

| Type | Value | Description |
|------|-------|-------------|
| Internal IP | 10.1.17.215 | Infected Windows client |
| MAC Address | 00:d0:b7:26:4a:74 | Infected machine MAC |
| Hostname | DESKTOP-L8C5GSJ | Infected machine hostname |
| Username | shutchenson | Logged-in user account |

---

## Threat Intelligence

| IOC | Platform | Result |
|-----|----------|--------|
| 5.252.153[.]241 | VirusTotal | Flagged malicious |
| 45.125.66[.]32 | VirusTotal | Flagged malicious |
| 45.125.66[.]252 | VirusTotal | Flagged malicious |
| 82.221.136[.]26 | VirusTotal | Flagged malicious |

---

*All external IPs and domains are defanged using bracket 
notation to prevent accidental resolution.*
