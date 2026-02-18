
## Lab Architecture

The lab simulates a small enterprise environment to demonstrate both red team attacks and blue team detection.

### Environment
- Attacker: Kali Linux
- Victim: Windows 10 (Domain Joined)
- Domain Controller: Windows Server
- Logging: Windows Event Logs / Sysmon

### Objective
Simulate realistic attacks and analyze how defensive controls respond.
# 🏗️ Lab Architecture

## Virtual Machine Specifications
| VM | OS | IP Address | Role |
|-----|-----|------------|------|
| DC01 | Windows Server 2019 | 192.168.56.10 | Domain Controller |
| WIN10-CLIENT | Windows 10 Pro | 192.168.56.20 | Domain Workstation |
| Kali | Kali Linux | 192.168.56.30 | Attacker |

## Network Configuration
- **VirtualBox Network:** Internal Network (AD-Lab)
- **Subnet:** 192.168.56.0/24
- **DHCP:** Disabled (Static IPs)

## Domain Setup
- **Domain Name:** `corp.local`
- **Functional Level:** Windows Server 2016
- **Users Created:**
  - `john.doe` (standard user)
  - `it.admin` (overprivileged IT admin)
  - `svc.backup` (service account with SPN)
  - `Administrator` (domain admin)

## Intentional Misconfigurations
- Weak passwords (`Password@123`, `Admin@123`)
- Service account with SPN (Kerberoastable)
- Overprivileged IT users
- Default Windows logging only
- SMBv1 enabled
- Firewall disabled for lab

## 📸 Screenshots
![Network Connectivity](screenshots/ping-test.png)
