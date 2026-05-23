# 📅 Day 10 - Windows fundamentals

Today I shifted gears into **Windows fundamentals** and explored how attackers use persistence techniques. This was more about understanding the OS internals, registry, and common artifacts that SOC analysts investigate during incidents.

---

## 📝 Topics I Covered
- Windows filesystem basics → `C:\Windows`, `System32`, `SysWOW64`
- Important Windows directories & files
- User account types: Admin vs Standard User
- UAC (User Account Control) basics
- Windows Registry fundamentals: HKLM, HKCU, Run keys
- Registry persistence locations
- Windows Services basics
- Task Manager essentials
- Scheduled Tasks basics
- Basic Windows process understanding: `explorer.exe`, `svchost.exe`, `lsass.exe`
- Navigating Registry using `regedit`
- SOC analyst view of Windows persistence & detection
- Common Windows artifacts used during investigations
### 🔹 Linux `sed` Fundamentals
- Basic syntax: `sed 's/find/replace/' file`
- In-place editing with `-i`
- Deleting lines: `sed '/pattern/d' file`
- Printing specific lines: `sed -n '5p' file`
- Using regex with `sed` for log manipulation
- Combining `sed` with `grep`/`awk` for advanced parsing
- SOC relevance: cleaning logs, extracting fields, and detecting attacker 
---

## ⚙️ Hands-On Practice
- Explored **System32 vs SysWOW64** to understand 32‑bit vs 64‑bit binaries.
- Checked **UAC prompts** and how privilege escalation works.
- Navigated the **Registry Editor (regedit)** and looked at `HKLM\Software\Microsoft\Windows\CurrentVersion\Run` keys.
- Identified **persistence locations** often abused by malware.
- Used **Task Manager** to review running processes and spot suspicious ones.
- Practiced `sed` to:
  - Replace usernames in logs with placeholders.
  - Delete noisy lines to focus on failed login attempts.
  - Extract specific fields for analysis.
- Combined `sed` with `grep` to filter and clean log entries for threat 

---

## 💡 Key Takeaways
- The **Windows Registry** is a goldmine for persistence detection — Run keys are a favorite spot for malware.
- **UAC** is a line of defense, but attackers often try to bypass it.
- **Scheduled Tasks** and **Services** are common persistence techniques; SOC analysts must know how to spot unusual entries.
- Processes like `lsass.exe` are high‑value targets (credential dumping), so monitoring them is critical.
- Windows artifacts (registry entries, scheduled tasks, startup folders) are often the first indicators of compromise.
- `sed` is extremely powerful for **log manipulation** — useful for cleaning, filtering, and preparing data for analysis.
---

## 🎯 Next Steps
Tomorrow I’ll:
- Go deeper into **Windows top Event Logs and Event IDs**
- Learn why they are critical for SOC investigations
- Connect Event IDs to attacker techniques and detection workflows
---

### 🔗 Resources
- [Windows Registry Basics](ca://s?q=Windows_registry_basics)
- [Windows Persistence Techniques](ca://s?q=Windows_persistence_techniques)
- [Task Manager Essentials](ca://s?q=Windows_task_manager_basics)
- [SOC Analyst Windows Artifacts](ca://s?q=SOC_Windows_artifacts_for_investigations)

---

🔥 *Day 10 complete!

