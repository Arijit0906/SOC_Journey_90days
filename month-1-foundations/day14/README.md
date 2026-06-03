# 📅 Day 13 – Active Directory(AD) Basics

Today I studied **Active Directory (AD)** and why it is critical for SOC analysts.

---

## 📝 What I Learned
- **Active Directory (AD):** Centralized authentication, authorization, and management system.
- **Core Components:** Forest → Domain → OU → Objects (Users, Computers, Groups).
- **Domain Controller (DC):** Stores AD database, authenticates users, issues Kerberos tickets.
- **Accounts:** User Accounts, Computer Accounts (e.g., `PC01$`), Service Accounts.
- **Privileged Groups:** Domain Admins, Enterprise Admins, Administrators.
- **Protocols:** LDAP (query AD), Kerberos (authentication), DNS (find DCs), NTLM (legacy auth).
- **Kerberos Basics:** KDC, TGT (master ticket), TGS (service ticket).
- **Important Event IDs:** 4672, 4720, 4728, 4768, 4769, 4771.
- **GPO:** Centralized security policy enforcement.
- **LDAP:** Used for AD enumeration and management.
- **Major Attacks:** Pass‑the‑Hash, Pass‑the‑Ticket, Kerberoasting, AS‑REP Roasting, DCSync, Golden Ticket, Silver Ticket.

---

## 💡 SOC Analyst Focus
- Authentication monitoring  
- Privilege escalation detection  
- Group membership changes  
- Service account abuse  
- Kerberos anomalies  
- AD attack detection  

---

## 🎯 Next Steps
Tomorrow I’ll:
- Continue with **revision** of everything learned in the last 6–7 days (Windows fundamentals, Event Logs, Sysmon, Log formats, Log management, PowerShell, Active Directory).
- Start learning a new topic **MITRE att&ck** framwork 
---

### 🔗 Resources
- [Active Directory Basics](ca://s?q=Active_Directory_basics_for_SOC)
- [Kerberos Authentication](ca://s?q=Kerberos_authentication_basics)
- [AD Attack Techniques](ca://s?q=Active_Directory_attack_techniques)

---

🔥 *Day 14 complete — Active Directory is the backbone of enterprise security, and understanding it is key for SOC investigations.*
