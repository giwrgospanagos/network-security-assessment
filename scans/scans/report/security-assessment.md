# Network Security Assessment Report

## 1. Executive Summary

A network security assessment was performed against a Windows host in a controlled local environment.

The assessment focused on identifying exposed TCP services, enumerating service information, analyzing SMB protocol support, and reviewing potential security considerations.

Four open TCP ports were identified: 135, 139, 445 and 5985.

No specific vulnerability was confirmed during the assessment. The findings represent services that should be reviewed and appropriately restricted according to the host's intended purpose.

---

## 2. Scope

**Target:** Local Windows host

**IP Address:** 192.168.1.6

**Operating System:** Microsoft Windows

**Assessment Type:** Network service enumeration

**Tool:** Nmap 7.99.1

All testing was performed on a system under my control.

---

## 3. Methodology

The assessment was conducted using the following steps:

### Step 1 — Port Scanning

A basic TCP scan was performed to identify open ports.

Command:

```text
nmap 192.168.1.6
```

### Step 2 — Service Enumeration

Service and version detection was performed using:

```text
nmap -sV 192.168.1.6
```

### Step 3 — SMB Protocol Enumeration

The SMB protocol versions supported by the host were examined using:

```text
nmap --script smb-protocols -p445 192.168.1.6
```

### Step 4 — WinRM Service Enumeration

The service running on TCP/5985 was examined using:

```text
nmap -sV -p5985 192.168.1.6
```

---

## 4. Findings

### Finding 01 — SMB Service Exposed

**Port:** 445/TCP

**Service:** Microsoft-DS / SMB

**Risk Level:** Medium

SMB was detected as an exposed service on TCP/445.

SMB is commonly used for Windows file and printer sharing. If unnecessarily exposed to untrusted networks, SMB can increase the attack surface of a Windows system.

### Recommendation

* Restrict SMB access using Windows Firewall.
* Allow SMB connections only from trusted networks or hosts.
* Keep Windows security updates current.
* Keep SMBv1 disabled when it is not required.

---

### Finding 02 — NetBIOS Service Exposed

**Port:** 139/TCP

**Service:** Microsoft NetBIOS-SSN

**Risk Level:** Low–Medium

NetBIOS was detected on TCP/139.

NetBIOS is a legacy Windows networking technology and may not be required on modern systems depending on the environment.

### Recommendation

* Disable NetBIOS over TCP/IP if it is not required.
* Restrict access to trusted networks.
* Review whether legacy Windows networking functionality is necessary.

---

### Finding 03 — Windows Remote Management Exposed

**Port:** 5985/TCP

**Service:** Microsoft HTTPAPI httpd 2.0

**Risk Level:** Medium

A Microsoft HTTPAPI service was detected on TCP/5985. This port is commonly associated with Windows Remote Management (WinRM).

Remote management services should be restricted to authorized systems and administrators.

### Recommendation

* Restrict WinRM access to authorized hosts.
* Apply appropriate Windows Firewall rules.
* Review authentication and access-control configuration.
* Avoid unnecessary exposure of remote management services.

---

### Finding 04 — Microsoft RPC Exposed

**Port:** 135/TCP

**Service:** Microsoft Windows RPC

**Risk Level:** Low–Medium

Microsoft RPC was detected on TCP/135.

RPC is an important component of Windows networking and is commonly required for legitimate Windows functionality. However, unnecessary exposure can increase the network attack surface.

### Recommendation

* Restrict RPC access using firewall rules where appropriate.
* Allow access only from trusted networks.
* Keep the Windows operating system patched.

---

## 5. SMB Protocol Analysis

The SMB protocol enumeration identified the following dialects:

* SMB 2.0.2
* SMB 2.1
* SMB 3.0
* SMB 3.0.2
* SMB 3.1.1

SMBv1 was not detected during the assessment.

This is a positive security observation because SMBv1 is an obsolete protocol and should generally remain disabled when not required.

---

## 6. Risk Summary

| Finding                   |     Port | Risk       |
| ------------------------- | -------: | ---------- |
| SMB Service               |  445/TCP | Medium     |
| NetBIOS                   |  139/TCP | Low–Medium |
| Windows Remote Management | 5985/TCP | Medium     |
| Microsoft RPC             |  135/TCP | Low–Medium |

The risk ratings represent an initial assessment based on service exposure. They do not confirm the existence of exploitable vulnerabilities.

---

## 7. Recommendations

Based on the assessment:

1. Restrict unnecessary network services using Windows Firewall.
2. Limit SMB access to trusted systems and networks.
3. Keep SMBv1 disabled.
4. Review whether NetBIOS is required.
5. Restrict WinRM to authorized hosts.
6. Keep Windows security updates up to date.
7. Regularly review exposed network services.

---

## 8. Conclusion

The assessment demonstrated the use of Nmap for network reconnaissance, TCP port scanning, service enumeration and SMB protocol analysis.

The exercise provided practical experience in identifying network services and evaluating their potential security impact.

The assessment did not identify a confirmed exploitable vulnerability. Instead, it identified exposed services that should be reviewed and appropriately restricted according to the system's operational requirements.

## Disclaimer

This assessment was performed for educational purposes on a system under my control.

No unauthorized systems or networks were targeted.
