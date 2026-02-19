
Overview
This document maps each attack technique used in the Red Team exercise to the MITRE ATT&CK framework, along with corresponding detection methods from the Blue Team perspective.

---

## 📊 Attack Techniques vs Detection

| Attack Phase | Technique | MITRE ID | Tactic | Detection Method | Windows Event ID |
|--------------|-----------|----------|--------|------------------|------------------|
| **Reconnaissance** | Network Scanning | T1046 | Discovery | Firewall logs, IDS | 5156 |
| **Initial Access** | Password Spraying | T1110.003 | Credential Access | Multiple failed logins | 4625 |
| **Privilege Escalation** | Valid Accounts | T1078.002 | Persistence | Successful logins | 4624 |
| **Credential Access** | OS Credential Dumping | T1003.003 | Credential Access | Volume Shadow Copy access | 4662 |
| **Credential Access** | Kerberoasting | T1558.003 | Credential Access | Kerberos service ticket requests | 4769 |
| **Lateral Movement** | Windows Remote Management | T1021.006 | Lateral Movement | WMI process creation | 4688 |
| **Execution** | Command and Scripting Interpreter | T1059.001 | Execution | PowerShell logs | 4104 |
| **Persistence** | Create Account | T1136.001 | Persistence | New user creation | 4720 |
| **Defense Evasion** | Disable Windows Firewall | T1562.001 | Defense Evasion | Firewall rule changes | 2003 |

---

## 🔴 Red Team Attack Chain (MITRE Mapped)
Reconnaissance (T1046)
↓

Password Spraying (T1110.003) → [DETECTED: 4625]
↓

Valid Account Login (T1078.002) → [DETECTED: 4624]
↓

NTDS Dumping (T1003.003) → [DETECTED: 4662, Volume Shadow]
↓

Pass-the-Hash / WMI (T1021.006) → [DETECTED: 4688]
↓

Kerberoasting Attempt (T1558.003) → [DETECTED: 4769]

text

---

## 🛡️ Blue Team Detection Coverage

| Tactic | MITRE ID | Techniques Attempted | Techniques Detected | Coverage |
|--------|----------|---------------------|---------------------|----------|
| Reconnaissance | TA0043 | 1 | 0 | 0% |
| Initial Access | TA0001 | 1 | 1 | 100% |
| Execution | TA0002 | 2 | 2 | 100% |
| Persistence | TA0003 | 1 | 1 | 100% |
| Privilege Escalation | TA0004 | 1 | 1 | 100% |
| Defense Evasion | TA0005 | 1 | 0 | 0% |
| Credential Access | TA0006 | 3 | 2 | 66% |
| Discovery | TA0007 | 1 | 0 | 0% |
| Lateral Movement | TA0008 | 1 | 1 | 100% |
| **Overall** | | **12** | **8** | **66%** |

---

## 📋 Detailed Technique Breakdown

### T1110.003 - Password Spraying
- **Command Used:** `crackmapexec smb 192.168.56.10 -u users.txt -p 'password@123'`
- **Detection:** Multiple Event ID 4625 (failed logons) from same source IP
- **Evidence:** 10+ failed login attempts in short time window

### T1078.002 - Valid Accounts (Domain Admin)
- **Success:** `[+] corp.local\Administrator:password@123 (Pwn3d!)`
- **Detection:** Event ID 4624 with elevated privileges
- **Evidence:** Successful login from 192.168.56.30 (Kali)

### T1003.003 - NTDS.dit Dumping
- **Command Used:** `crackmapexec smb 192.168.56.10 --ntds`
- **Detection:** Volume Shadow Copy creation (Event ID 4662)
- **Evidence:** Access to ntds.dit file detected

### T1558.003 - Kerberoasting
- **Command Used:** `impacket-GetUserSPNs -request -dc-ip 192.168.56.10`
- **Target:** `svc.backup` account with SPN
- **Detection:** Event ID 4769 (Kerberos service ticket requested)

### T1021.006 - Lateral Movement via WMI
- **Command Used:** `impacket-wmiexec -hashes :<hash> corp.local/Administrator@192.168.56.20`
- **Detection:** Event ID 4688 (process creation) with wmiexec
- **Evidence:** Remote process execution on WIN10-CLIENT

---

## 🔍 Detection Gaps Identified

| Gap | Impact | Recommendation |
|-----|--------|----------------|
| No alerting on multiple failed logins | Password spraying undetected in real-time | Implement SIEM rule for 4625 threshold |
| No monitoring for Volume Shadow Copies | NTDS dumping goes unnoticed | Monitor VSSadmin/WMIC usage |
| No Kerberoasting alerts | Service account targeting invisible | Alert on unusual 4769 events |
| No centralized logging | Hard to correlate attacks | Deploy Sysmon + SIEM |

---

## 📌 MITRE ATT&CK Navigator Layer

```json
{
  "name": "Red Team Attack Layer",
  "techniques": [
    { "techniqueID": "T1110.003", "color": "#ff6666" },
    { "techniqueID": "T1078.002", "color": "#ff6666" },
    { "techniqueID": "T1003.003", "color": "#ff6666" },
    { "techniqueID": "T1558.003", "color": "#ff6666" },
    { "techniqueID": "T1021.006", "color": "#ff6666" },
    { "techniqueID": "T1059.001", "color": "#ff6666" }
  ]
}
