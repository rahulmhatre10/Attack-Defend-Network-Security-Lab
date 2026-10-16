# Attack & Defend: Network Security Assessment Lab

## Overview
An authorized cybersecurity lab project combining network
reconnaissance, service identification, packet capture, and
defensive analysis.

## Environment
- Cisco Ethical Hacker Kali Linux
- Docker-based Metasploitable 2 lab target
- Nmap
- tcpdump
- Wireshark

## Methodology
1. Verified the lab network and target.
2. Identified exposed TCP services.
3. Captured traffic during the assessment.
4. Reviewed packets and documented observations.
5. Prepared remediation recommendations.

## Results

### 1. Network Reconnaissance and Service Identification

An Nmap TCP connect scan with service-version detection was performed against the authorized lab target, `192.168.0.10` (`metasploitable.pc`). The target was reachable during the scan, and Nmap identified the following open TCP ports and associated services.

| Port | Detected service | Version or observation |
|---|---|---|
| 21/tcp | FTP | vsftpd 2.3.4 |
| 22/tcp | SSH | OpenSSH 4.7p1 |
| 23/tcp | Telnet | Linux telnetd |
| 25/tcp | SMTP | Postfix smtpd |
| 80/tcp | HTTP | Apache 2.2.8 |
| 111/tcp | rpcbind | Service detected |
| 139/tcp | NetBIOS/SMB | Samba version range reported |
| 445/tcp | NetBIOS/SMB | Samba version range reported |
| 3306/tcp | MySQL | Service identification uncertain |
| 5432/tcp | PostgreSQL | Version range 8.3.0–8.3.7 reported |

These results show that multiple network services were exposed on the intentionally vulnerable lab target. The legacy software versions and availability of Telnet warrant further configuration and patch-status review. Service detection alone does not confirm that a vulnerability can be exploited.

### 2. Network Traffic Capture

Network traffic was intended to be captured using `tcpdump` while the Nmap assessment was performed. The capture file was designated as `captures/assessment.pcap`.

**Packet-level findings:** To be completed after inspecting the saved PCAP file in Wireshark. Record the source and destination IP addresses, observed TCP connection attempts, destination ports, and relevant packet numbers. Include only details confirmed by the capture.

### 3. Defensive Analysis

The initial scan highlights several areas for defensive review:

- Replace Telnet with SSH where remote administration is required.
- Review exposed services and disable those that are unnecessary.
- Verify software versions and apply supported security updates.
- Restrict database and file-sharing services to authorized systems.
- Review service configurations and monitor unusual connection attempts.

### 4. Evidence and Reproducibility

The assessment evidence consists of the saved Nmap output and the packet capture, where available. These files allow the observations to be reviewed and the assessment to be repeated in the same authorized lab environment.

### 5. Overall Result

The initial reconnaissance successfully identified multiple open TCP ports and several associated services on the lab target. This established a baseline for further traffic analysis and defensive review. Packet-level conclusions remain subject to verification against the saved capture.


## Limitations
This was a controlled lab assessment. Service detection does
not independently establish exploitability, and the traffic
capture does not prove a successful compromise.

## Ethics
Testing was restricted to the intentionally vulnerable
lab environment.
