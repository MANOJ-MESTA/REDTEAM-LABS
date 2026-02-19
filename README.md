#  Active Directory Red vs Blue Team Simulation

##  Project Overview
A complete enterprise-grade Active Directory lab built from scratch to simulate real-world attacks and defensive detection. This project demonstrates the full attack lifecycle from initial access to domain compromise, with corresponding Blue Team detection and MITRE ATT&CK mapping.

##  Lab Architecture
┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐
│ KALI │ │ DC01 │ │ WIN10-CLIENT │
│ 192.168.56.30 │────│ 192.168.56.10 │────│ 192.168.56.20 │
│ Attacker │ │ Domain Ctrl │ │ Victim │
└─────────────────┘ └─────────────────┘ └─────────────────┘
│ │ │
└───────────────────────┴───────────────────────┘
Internal Network: AD-Lab
192.168.56.0/24

text

##  Repository Structure
├── 00-Lab-Setup/ # Environment architecture & configuration
├── 01-Red-Team-Attack/ # Attack techniques & commands used
├── 02-Blue-Team-Detection/ # Logs, alerts, and detection methods
├── 03-Attack-vs-Detection/ # MITRE ATT&CK mapping
├── 04-Lessons-Learned/ # Improvements & takeaways
├── screenshots/ # Visual evidence
└── README.md

text

##  Key Achievements
 Built isolated AD environment with Windows Server 2019 DC  
 Created vulnerable domain with intentional misconfigurations  
 Performed password spraying → Domain Admin compromise  
 Dumped NTDS.dit with all domain user hashes  
 Cracked passwords: john.doe, it.admin, svc.backup  
 Lateral movement to WIN10 via Pass-the-Hash  
 wmiexec shell on remote workstation  
 Analyzed Windows Event Logs for attack evidence  
 Mapped all techniques to MITRE ATT&CK

##  Tools Used
| Category | Tools |
|----------|-------|
| **Recon** | Nmap, enum4linux-ng |
| **Exploitation** | CrackMapExec, Impacket |
| **Post-Exploitation** | wmiexec, secretsdump |
| **Password Cracking** | John the Ripper |
| **Detection** | Windows Event Viewer, PowerShell |

##  Screenshots
![Lab Topology](screenshots/lab-topology.png)
![Domain Compromise](screenshots/pwn3d.png)
![NTDS Dump](screenshots/ntds-dump.png)
![Lateral Movement](screenshots/wmiexec-shell.png)

## Disclaimer
This project was created for **educational purposes only**. All techniques demonstrated should only be used in authorized environments with proper permissions.

##  Author
Manoj Mesta  
 | [GitHub](https://github.com/yourusername)
