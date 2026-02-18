Alerts Triggered During Attack

## Alert 1: Multiple Failed Logins
**Time:** Throughout attack  
**Event ID:** 4625  
**Count:** 10+ failures  
**Indicates:** Password spraying attempt  

## Alert 2: Successful Admin Login from Unusual IP
**Time:** During password spraying success  
**Event ID:** 4624  
**Source IP:** 192.168.56.30 (Kali)  
**Target:** Administrator account  
**Indicates:** Valid credential discovery  

## Alert 3: NTDS.dit Access
**Time:** Post-compromise  
**Event:** Volume Shadow Copy access  
**Indicates:** Credential dumping (T1003.003)  

## Alert 4: Remote WMI Connection
**Time:** Lateral movement phase  
**Event ID:** 4688 (WMIC.exe)  
**Source:** 192.168.56.30  
**Target:** WIN10-CLIENT  
**Indicates:** Lateral movement (T1021.006)  

## Alert 5: Kerberos Service Ticket Request
**Time:** Post-compromise  
**Event ID:** 4769  
**Target:** svc.backup account  
**Indicates:** Kerberoasting attempt (T1558.003)  

## Detection Gaps Identified
- No SIEM for centralized alerting
- Default logging only (no Sysmon)
- No account lockout policy
- No alerting on volume shadow copies
