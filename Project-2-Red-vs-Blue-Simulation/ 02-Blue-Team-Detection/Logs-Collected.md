 Windows Event Logs Collected

## Event IDs Monitored

| Event ID | Description | Attack Detected |
|----------|-------------|-----------------|
| 4624 | Successful Logon | Admin access gained |
| 4625 | Failed Logon | Password spraying |
| 4648 | Logon with explicit credentials | Lateral movement |
| 4688 | Process Creation | Remote command execution |
| 4768 | Kerberos TGT requested | Kerberoasting attempt |
| 4769 | Kerberos service ticket | Service account targeting |

## Sample Log Queries
```powershell
# Check failed logins (password spraying)
Get-WinEvent -FilterHashtable @{LogName='Security'; ID=4625} -MaxEvents 20 | 
    Format-Table TimeCreated, Message -AutoSize

# Check successful admin logins
Get-WinEvent -FilterHashtable @{LogName='Security'; ID=4624} -MaxEvents 5 | 
    Where-Object {$_.Message -like "*Administrator*"} |
    Format-Table TimeCreated, Message -AutoSize

# Check process creation (remote commands)
Get-WinEvent -FilterHashtable @{LogName='Security'; ID=4688} -MaxEvents 10 |
    Where-Object {$_.Message -like "*wmiexec*" -or $_.Message -like "*crackmapexec*"} |
    Format-Table TimeCreated, Message -AutoSize
