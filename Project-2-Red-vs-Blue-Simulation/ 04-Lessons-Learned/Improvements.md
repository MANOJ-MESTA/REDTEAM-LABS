# 📈 Lessons Learned & Improvements

## What Went Well
✅ Complete AD lab built from scratch  
✅ Full domain compromise achieved  
✅ All domain hashes extracted  
✅ Passwords successfully cracked  
✅ Lateral movement to workstation  
✅ All attacks left evidence in logs  

## Critical Findings

### 1. Weak Passwords Are the #1 Risk
- Administrator had simple password `password@123`
- Users reused common passwords
- **Fix:** Enforce strong password policy, MFA

### 2. Service Accounts Are Prime Targets
- `svc.backup` was Kerberoastable
- Password never expires
- **Fix:** Managed service accounts (gMSA), rotate regularly

### 3. Default Logging Is Insufficient
- Attacks were logged but no alerts
- No centralized collection
- **Fix:** Deploy Sysmon, SIEM, create alert rules

### 4. Lateral Movement Too Easy
- Pass-the-Hash worked immediately
- No network segmentation
- **Fix:** Implement LAPS, restrict WMI/RDP, network segmentation

## Recommended Security Controls

| Priority | Control | MITRE Mapping |
|----------|---------|---------------|
| 🔴 HIGH | Enable MFA for all admins | T1078 |
| 🔴 HIGH | Deploy Sysmon + SIEM | T1046, T1003 |
| 🟠 MEDIUM | Implement LAPS for local admin | T1021 |
| 🟠 MEDIUM | Disable WMI unless needed | T1047 |
| 🟢 LOW | Regular penetration testing | All |

## Future Lab Enhancements
- [ ] Add Splunk/ELK for centralized logging
- [ ] Deploy Sysmon with SwiftOnSecurity config
- [ ] Implement Defender for Endpoint
- [ ] Add more workstations for complex lateral movement
- [ ] Create custom Sigma detection rules
- [ ] Add web server with additional vulnerabilities
