Attack Techniques vs Detection

| Attack Phase | Technique | MITRE ID | Detection Method | Event ID |
|--------------|-----------|----------|------------------|----------|
| **Recon** | Network Scanning | T1046 | Network logs | Firewall logs |
| **Initial Access** | Password Spraying | T1110.003 | Failed logins | 4625 |
| **Privilege Escalation** | Valid Accounts | T1078.002 | Successful logins | 4624 |
| **Credential Access** | NTDS Dumping | T1003.003 | Volume Shadow Copy | 4662 |
| **Credential Access** | Kerberoasting | T1558.003 | Kerberos tickets | 4769 |
| **Lateral Movement** | WMI | T1021.006 | Process creation | 4688 |
| **Execution** | Remote Commands | T1059.001 | PowerShell logs | 4104 |

## Attack Chain Visualization
Recon (T1046)
↓
Password Spraying (T1110.003) → [DETECTED: 4625]
↓
Valid Account Access (T1078.002) → [DETECTED: 4624]
↓
NTDS Dumping (T1003.003) → [DETECTED: Volume Shadow]
↓
Lateral Movement via WMI (T1021.006) → [DETECTED: 4688]
↓
Kerberoasting (T1558.003) → [DETECTED: 4769]

text

## Detection Coverage
| Tactic | Techniques Attempted | Techniques Detected | Coverage |
|--------|---------------------|---------------------|----------|
| Initial Access | 2 | 2 | 100% |
| Execution | 3 | 2 | 66% |
| Persistence | 1 | 1 | 100% |
| Privilege Escalation | 2 | 2 | 100% |
| Credential Access | 3 | 2 | 66% |
| Lateral Movement | 2 | 1 | 50% |
| **Overall** | **13** | **10** | **77%** |
