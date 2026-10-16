# Network Traffic Investigation

## Objective
Capture and inspect network traffic generated during an authorized Nmap assessment of the intentionally vulnerable Metasploitable 2 lab target.

## Evidence
- **PCAP:** `captures/assessment.pcap`
- **Nmap report:** `scans/captured-assessment.nmap`
- **Target:** `192.168.0.10` (`metasploitable.pc`)
- **Scanning tool:** Nmap

## Observations

### Source and Destination IPs
- **Target IP:** `192.168.0.10`
- **Source IP:** `192.168.0.10`
- **Destination IP:** `192.168.0.1`.

### TCP Connection Attempts Observed
The original Nmap assessment reported open TCP ports 21, 22, 23, 25, 80, 111, 139, 445, 3306 and 5432.

The packet capture must be inspected to confirm which TCP connection attempts occurred during the recorded assessment.

### Services Contacted
The original Nmap scan identified the following services:

- FTP — port 21
- SSH — port 22
- Telnet — port 23
- SMTP — port 25
- HTTP — port 80
- rpcbind — port 111
- Samba/SMB — ports 139 and 445
- MySQL — port 3306 (service identification uncertain)
- PostgreSQL — port 5432

These services were identified by the original scan. Confirm which ports appear in the packet capture before stating that they were contacted during the captured scan.

### Other Relevant Packet Details
Inspect the capture for TCP SYN packets, connection establishment, connection resets, retransmissions and any application-layer data that is actually present. Record the relevant packet numbers and timestamps as evidence.

## Security Interpretation

The original Nmap results indicate that multiple network services are exposed on the lab target. This increases the number of services that should be reviewed for secure configuration, access control and software maintenance.

TCP connection attempts in the packet capture can provide evidence of reconnaissance activity. However, a connection attempt does not by itself establish that a login succeeded, a vulnerability was exploited or a system was compromised.

The final interpretation should distinguish directly observed packet details from conclusions that require additional verification.

## Defensive Recommendations

- Disable unnecessary network services and restrict exposed ports.
- Limit administrative access to trusted hosts and networks.
- Replace insecure protocols such as Telnet with secure alternatives.
- Review service configurations, software versions and patch status.
- Monitor repeated connection attempts and unusual traffic patterns.
- Retest after remediation to verify that unnecessary exposure has been reduced.

## Limitations

- The conclusions depend on the packets captured and the completeness of the PCAP file.
- Nmap service identification may be incomplete or uncertain.
- A packet capture alone does not prove a successful compromise.
- The original Nmap results do not establish that every identified service was contacted during the captured assessment.
- Findings apply to the authorized lab environment and should not be generalized to other systems without further testing.
