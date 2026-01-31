
## Attack vs Detection Mapping

| Attack Technique | Log Evidence | Detected |
|------------------|--------------|----------|
| Initial Access   | Event ID logs | Partial  |
| Priv Esc         | Sysmon logs   | Yes      |
| Lateral Movement | SMB logs      | No       |

### Key Insight
Attackers can successfully operate when monitoring and correlation are insufficient.
