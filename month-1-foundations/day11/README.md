# 📅 Day 11 – Windows Event Logs and IDs

Today I explored **Windows Event Logs and Event IDs** — the backbone of SOC investigations on Windows systems. These logs capture authentication attempts, process creation, service changes, and more, making them critical for detecting attacker activity.

---

## 📝 Topics I Covered
- Introduction to Windows Event Logs
- Types of Windows Logs (Security, System, Application, Setup, Forwarded Events)
- Windows Event Viewer basics
- Critical Windows Security Event IDs
- Logon Types deep dive
- SIEM relevance of Windows logs

---

## ⚙️ Hands-On Practice
- Navigated **Event Viewer** and explored Security/System/Application logs.
- Filtered for **Event ID 4625** to track failed login attempts.
- Reviewed **4624 (successful logon)** and **4672 (special privileges assigned)**.
- Checked **4688 (process creation)** events to spot suspicious binaries.
- Practiced identifying logon types (interactive, remote, network).
- Connected Event IDs to SIEM workflows for correlation and alerting.

---

## 💡 Key Takeaways
- Event IDs are **SOC gold** — they answer “who, what, when, where” during investigations.
- Failed logons (4625) and log clears (1102) are high‑priority alerts.
- Process creation (4688) and service installation (4697) often reveal persistence attempts.
- Understanding logon types helps distinguish between normal user activity and attacker behavior.
- SIEM platforms rely heavily on these logs for detection and correlation.

---

## 🎯 Future Work
Next day, I’ll dive into **Sysmon** to extend native logging:
- What Sysmon adds over native logging
- Key Event IDs:
  - 1 → ProcessCreate  
  - 3 → NetworkConnect  
  - 7 → ImageLoad  
  - 11 → FileCreate  
  - 13 → RegSet and many more
- Sysmon configuration files
- SwiftOnSecurity Sysmon config

---

### 🔗 Resources
- [Windows Event Logs](ca://s?q=Windows_event_logs_basics)
- [Important Event IDs](ca://s?q=Important_Windows_event_IDs_for_SOC)
- [Logon Types](ca://s?q=Windows_logon_types_explained)
- [Sysmon Basics](ca://s?q=Sysmon_basics_for_SOC)
- [SwiftOnSecurity Config](ca://s?q=SwiftOnSecurity_Sysmon_config)

---

🔥 *Day 11 complete!*
