# IOC List — Investigation 01

**Date:** June 2026

**Source:** 2026-02-28 Traffic Analysis Exercise

**Malware Family:** NetSupport Manager RAT

---

## Network IOCs

| Type | Value | Description |
|------|-------|-------------|
| IP | 45.131.214[.]85 | C2 server — NetSupport Manager RAT |
| URI | /fakeurl[.]htm | C2 checkin path |
| Port | TCP 443 | C2 communication port |

## Host IOCs

| Type | Value | Description |
|------|-------|-------------|
| Internal IP | 10.2.28.88 | Infected Windows client |
| Hostname | DESKTOP-TEYQ2NR | Infected machine hostname |
| Username | brolf | Logged-in user account |
| Full Name | Becka Rolf | Identity of affected user |

---

## Threat Intelligence

| IOC | Platform | Result |
|-----|----------|--------|
| 45.131.214[.]85 | VirusTotal | Multiple vendor detections — confirmed malicious |
| 45.131.214[.]85 | AbuseIPDB | Reported for malware C2 activity |

---

*All external IPs and domains are defanged using bracket 
notation to prevent accidental resolution.*
