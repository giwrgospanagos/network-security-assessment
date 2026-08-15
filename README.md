# Network Security Assessment Lab

## Overview

This project documents a hands-on network security assessment performed on a Windows host in a controlled local environment.

The objective was to identify exposed TCP ports, enumerate running services, examine SMB protocol support, and document potential security considerations.

## Objectives

* Perform network reconnaissance
* Identify open TCP ports
* Enumerate services and versions
* Analyze SMB protocol support
* Identify potential security risks
* Document findings and recommendations

## Environment

* **Operating System:** Microsoft Windows
* **Target:** Local Windows host
* **Network:** Private/local network
* **Tool:** Nmap 7.99.1

> All testing was performed on a system under my control in a controlled environment.

## Methodology

The assessment was performed in several stages:

1. Host discovery and basic port scanning
2. Service and version detection
3. SMB protocol enumeration
4. Windows Remote Management service enumeration
5. Security assessment and documentation

## Tools Used

* Nmap
* Windows Command Prompt

## Findings

### 1. Open TCP Ports

The initial Nmap scan identified four open TCP ports:

| Port | Service      | Description                         |
| ---- | ------------ | ----------------------------------- |
| 135  | MSRPC        | Microsoft Windows RPC               |
| 139  | NetBIOS-SSN  | Windows NetBIOS networking          |
| 445  | Microsoft-DS | SMB file and printer sharing        |
| 5985 | HTTP         | Windows Remote Management / HTTPAPI |

### 2. SMB Protocols

The SMB service on TCP/445 was examined using Nmap's `smb-protocols` script.

The following SMB dialects were detected:

* SMB 2.0.2
* SMB 2.1
* SMB 3.0
* SMB 3.0.2
* SMB 3.1.1

SMBv1 was not detected during the assessment.

### 3. Windows Remote Management

TCP/5985 was identified as:

`Microsoft HTTPAPI httpd 2.0`

This service is associated with Windows Remote Management (WinRM).

## Security Considerations

### SMB — TCP/445

SMB is commonly used for Windows file and printer sharing. Exposure of this service should be limited to trusted networks and systems where possible.

**Recommendation:**

* Restrict SMB access using Windows Firewall.
* Allow SMB only from trusted networks or hosts.
* Keep Windows security updates up to date.
* Keep SMBv1 disabled when it is not required.

### NetBIOS — TCP/139

NetBIOS is a legacy Windows networking protocol.

**Recommendation:**

* Disable NetBIOS over TCP/IP where it is not required.
* Restrict access to trusted networks.

### WinRM — TCP/5985

Windows Remote Management provides remote management capabilities.

**Recommendation:**

* Restrict WinRM access to authorized hosts.
* Use appropriate authentication and firewall rules.
* Prefer secure configurations and avoid unnecessary exposure.

## Risk Assessment

The identified services do not by themselves prove that the host is vulnerable.

The assessment identified services that should be reviewed and appropriately restricted depending on the intended use of the system.

Further testing would be required to determine whether specific vulnerabilities or misconfigurations are present.

## Conclusion

This project provided hands-on experience with network reconnaissance, TCP port scanning, service enumeration, SMB protocol analysis, and basic security assessment using Nmap.

The results were documented and analyzed from a defensive security perspective, with recommendations for reducing unnecessary network exposure.

## Disclaimer

This project was performed for educational purposes on a system under my control.

No unauthorized systems or networks were targeted.
