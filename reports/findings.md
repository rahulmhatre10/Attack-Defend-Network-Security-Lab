# Network Vulnerability Assessment

## Scope
Target: 192.168.0.10
Environment: Authorized local Docker lab
Date: [enter date]

## Method
- TCP connect scan
- Lightweight service-version detection
- Selected-port verification

## Findings
For each confirmed finding, record:
Finding 1: FTP Service
- Port and protocol:21/tcp
- Detected service/version:vsftpd 2.3.4
- Evidence from Nmap: Port 21 is open; service identified as vsftpd 2.3.4.
- Risk and rationale:Potentially high risk because this legacy FTP version is associated with a historically documented backdoor vulnerability. The scan alone does not confirm exploitability.
- Recommended remediation:Disable FTP if unnecessary. Otherwise, replace it with a supported, patched service and prefer SFTP for secure file transfer.
- Verification required:Confirm the installed package version and patch status; verify that the vulnerable behavior is absent.

Finding 2: SSH Service
- Port and protocol:22/tcp
- Detected service/version:OpenSSH 4.7p1 Debian 8ubuntu1
- Evidence from Nmap:Port 22 is open; SSH protocol 2.0 reported.
- Risk and rationale:Legacy SSH software may lack current security fixes. The scan does not establish which vulnerabilities, if any, are exploitable.
- Recommended remediation:Upgrade to a supported SSH version, disable weak authentication methods, and restrict access.
- Verification required:Check the installed package version and effective SSH configuration.

Finding 3: Telnet Service
- Port and protocol:23/tcp
- Detected service/version:Linux telnetd
- Evidence from Nmap:Port 23 is open.
- Risk and rationale:Telnet does not encrypt login credentials or session traffic, creating a risk of credential exposure.
- Recommended remediation:Disable Telnet and use SSH instead.
- Verification required:Confirm port 23 is no longer accessible from unauthorized hosts.

Finding 4: SMTP Service
- Port and protocol:25/tcp
- Detected service/version:Postfix smtpd
- Evidence from Nmap:Port 25 is open; Postfix smtpd identified.
- Risk and rationale:The scan does not establish whether the mail service is misconfigured.Unnecessary exposure or insecure relay settings could increase risk.
- Recommended remediation:Restrict access as appropriate, patch Postfix, and verify relay and TLS settings.
- Verification required:Review the effective mail-server configuration and authorized relay behavior.

Finding 5: HTTP Service
- Port and protocol:80/tcp
- Detected service/version:Apache httpd 2.2.8 (Ubuntu), DAV/2
- Evidence from Nmap:Port 80 is open; Apache 2.2.8 and DAV/2 were reported.
- Risk and rationale:Apache 2.2.8 is an obsolete release. WebDAV may expose additional write or file-management functionality if improperly configured. The scan does not confirm a specific exploitable flaw.
- Recommended remediation:Upgrade to a supported web-server version, disable unnecessary WebDAV functionality, and review access controls.
- Verification required:Confirm the package and patch status, WebDAV configuration, and permitted HTTP methods.

Finding 6: RPC Service
- Port and protocol:111/tcp
- Detected service/version:rpcbind
- Evidence from Nmap:Port 111 is open; rpcbind identified.
- Risk and rationale:Exposed RPC services may disclose service information or enable access to unnecessary network services.
- Recommended remediation:Disable rpcbind if not needed or restrict it to trusted networks.
- Verification required:Identify registered RPC services and confirm that access is appropriately restricted.

Finding 7: SMB / NetBIOS Services
- Port and protocol:139/tcp and 445/tcp
- Detected service/version:Samba smbd 3.X–4.X; workgroup WORKGROUP
- Evidence from Nmap:Ports 139 and 445 are open; Samba was identified.
- Risk and rationale:SMB exposure may permit information disclosure or unauthorized file access if permissions or configuration are weak. The version range reported by Nmap is not an exact installed version.
- Recommended remediation:Upgrade Samba, restrict SMB access, disable SMBv1 if enabled and unnecessary, and audit share permissions.
- Verification required:Determine the exact Samba version and inspect share permissions and protocol settings.

Finding 8: MySQL Service
- Port and protocol:3306/tcp
- Detected service/version:MySQL service suspected; version not identified
- Evidence from Nmap:Port 3306 is open; service identification is uncertain (mysql?).
- Risk and rationale:An exposed database may allow unauthorized access if network restrictions or authentication are weak. The scan does not establish that unauthorized access is possible.
- Recommended remediation:Restrict database access to authorized hosts, patch the database, and enforce strong authentication.
- Verification required:Confirm the database product/version and inspect network access controls.

Finding 9: PostgreSQL Service
- Port and protocol:5432/tcp
- Detected service/version:PostgreSQL 8.3.0–8.3.7
- Evidence from Nmap:Port 5432 is open; PostgreSQL version range was reported.
- Risk and rationale:This is a legacy database version range and may lack modern security fixes. The scan does not confirm a specific vulnerability or successful unauthorized access.
- Recommended remediation:Migrate to a supported PostgreSQL version and restrict access to trusted clients.
- Verification required:Confirm the exact installed version, patch status, and database access rules.

## Limitations
- Service detection may be incomplete.
- An open port does not prove a vulnerability.
- Findings apply only to this lab target.

