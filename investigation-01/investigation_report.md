# Incident Response Investigation Report — Investigation 01

**Date of Analysis:** June 2026

**Exercise Source:** Malware-Traffic-Analysis.net — 2026-02-28

**Exercise Title:** Easy As 123

**PCAP File:** 2026-02-28-traffic-analysis-exercise.pcap

---

## Scenario

The Security Operations Center received SIEM alerts showing multiple signature hits for NetSupport Manager RAT activity. Alerts indicated an internal IP was communicating with known malicious external infrastructure at 45.131.214[.]85 over TCP port 443. Activity began at 19:55 UTC on 2026-02-28. A packetcapture was retrieved from the flagged internal IP for analysis.

---

## Infected Host Identification

| Field | Value |
|-------|-------|
| IP Address | 10.2.28.88 |
| MAC Address | 00:19:d1:b2:4d:ad |
| Hostname | DESKTOP-TEYQ2NR |
| User Account | brolf |
| Full Name | Becka Rolf |

---

## Threat Identification

| Field | Value |
|-------|-------|
| Malware Family | NetSupport Manager RAT |
| C2 IP | 45.131.214[.]85 |
| C2 Port | TCP 443 |
| Suspicious URI | /fakeurl.htm |
| Protocol | HTTP over port 443 |
| VirusTotal Status | Flagged malicious — multiple vendor detections |

---

## Investigation Methodology

**Step 1 — Protocol Hierarchy Analysis:**
Reviewed Statistics -> Protocol Hierarchy to understand traffic composition and identify dominant protocols in the capture.

**Step 2 — Conversation Analysis:**
Reviewed Statistics -> Conversations -> IPv4 tab to identify high-duration external connections. Sorted by duration to surface sustained connections rather than relying on raw packet count alone.

**Step 3 — Suspicious IP Identification:**
Identified 45.131.214[.]85 as the primary suspicious external IP based on connection duration from capture start time and unusual HTTP activity over port 443.

**Step 4 — Threat Intelligence Enrichment:**
Verified 45.131.214[.]85 on VirusTotal and confirmed multiple security vendor detections as malicious C2 infrastructure.

**Step 5 — URI Analysis:**
Applied Wireshark filter `ip.addr == 45.131.214.85` and followed HTTP stream in which identified /fakeurl.htm as the C2 checkin URI, a strong indicator of NetSupport RAT traffic.

**Step 6 — Infected Host Identification:**
Isolated internal IP 10.2.28.88 as the infected machine from filtered packet results.

**Step 7 — MAC Address Extraction:**
Expanded Ethernet II frame in packet detail panel to extract MAC address of the infected host.

**Step 8 — Hostname Identification:**
Applied DHCP filter to locate hostname broadcast from infected host during network join. Identified DESKTOP-TEYQ2NR.

**Step 9 — Username and Full Name Identification:**
Applied KERBEROS filter to locate kerberos ticket authentication traffic. Extracted user account brolf and full name Becka Rolf from Kerberos TGT authentication packets.

---

## Containment Recommendations

1. Isolate DESKTOP-TEYQ2NR from network immediately
2. Reset credentials for user account brolf
3. Block C2 IP 45.131.214[.]85 at perimeter firewall and proxy
4. Scan all internal hosts for connections to same C2 IP
5. Review SIEM for any other hosts showing similar NetSupport RAT signature hits
6. Submit malware sample to AV vendor if binary recovered

---
