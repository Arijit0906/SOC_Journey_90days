# 📅 Day 12 – SOC Analyst 30-Day Challenge

Today I focused on **Sysmon (System Monitor)** and why it’s one of the most important telemetry tools for SOC analysts, threat hunters, and DFIR teams.

---

## 📝 What I Learned
- Understood what **Sysmon** is and how it extends visibility beyond normal Windows Event Logs.
- Difference between **native Windows logs** vs **Sysmon logs**:
  - Windows logs → basic events (logon, system, application).
  - Sysmon logs → deep visibility into processes, network activity, registry changes, DNS queries, persistence mechanisms.
- Sysmon architecture:
  - Kernel driver
  - Windows service
  - XML configuration
  - Event logging workflow
- Practiced installing Sysmon with configuration files.
- Located Sysmon operational logs inside **Event Viewer**.
- Learned how Sysmon captures events and converts them into detailed telemetry for SIEM platforms (Splunk, Elastic, Microsoft Sentinel).
- Important Sysmon Event IDs:
  - **1** → Process Creation  
  - **3** → Network Connection  
  - **10** → Process Access  
  - **11** → File Create  
  - **12/13/14** → Registry Events  
  - **22** → DNS Query
- Understood **parent-child process relationships** (e.g., `WINWORD.EXE → powershell.exe`) and why they matter for detection.
- Practiced analyzing a real Sysmon Event ID 1 log:
  - Looked at fields like `Image`, `CommandLine`, `ParentImage`, `IntegrityLevel`, and `Hashes`.
- Learned the importance of **baselining, noise reduction, and XML filtering** in real SOC environments.

---

## 💡 Key Takeaways
- Sysmon provides **richer telemetry** than native Windows logs.
- Parent-child process tracking is critical for spotting suspicious activity.
- Baselining and filtering are necessary to avoid drowning in noise.

---

## 🎯 Next Steps
Tomorrow I’ll:
- Dive into **PowerShell fundamentals** (commands, scripting, and usage).
- Learn how attackers use PowerShell and how SOC teams detect it.

---

### 🔗 Resources
- [Sysmon Basics](ca://s?q=Sysmon_basics_for_SOC)
- [Sysmon Event IDs](ca://s?q=Sysmon_event_IDs_explained)

---

🔥 *Day 12 complete! Sysmon feels like the SOC analyst’s microscope — tomorrow I’ll switch gears to PowerShell.*
