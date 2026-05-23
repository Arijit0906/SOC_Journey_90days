# 📝 Key Notes – Windows Fundamentals + Registry

## 📂 Filesystem Basics
- A **filesystem** is the structure Windows uses to store, organize, and manage files/folders on disk.
- Windows mainly uses **NTFS (New Technology File System)**  
  Features: Permissions, Encryption, Compression, Logging, File Ownership

### Important Directories
- **C:\Windows\System32** → Most important Windows folder  
  Contains: core system files, DLLs, drivers, administrative tools, critical executables
- **SysWOW64** → Located at `C:\Windows\SysWOW64` on 64‑bit systems  
  Despite the “64” in its name, it stores **32‑bit system files** (DLLs/executables) to allow older programs to run on modern 64‑bit PCs.

---

## 🔐 Least Privilege
- **Why it matters:** Reduces attack surface by giving users only the permissions necessary to perform tasks.
- **Why attackers escalate privileges:** To gain full system access, disable defenses, steal credentials, and maintain persistence.

---

## 🛡️ UAC (User Account Control)
- Windows security feature that prevents unauthorized system‑level changes.
- **Why UAC exists:** Prevents malware from silently:
  - Installing software  
  - Modifying registry  
  - Disabling antivirus  

---

## 🧠 Windows Registry
- A hierarchical database storing:
  - System settings  
  - User configurations  
  - Installed software info  
  - Startup programs  
- Think of it as the **“brain/configuration database of Windows.”**

### Main Registry Hives
- **HKLM (HKEY_LOCAL_MACHINE)**  
  Contains system‑wide configs, drivers, services, installed software → affects **all users**
- **HKCU (HKEY_CURRENT_USER)**  
  Contains current logged‑in user settings, desktop configs, startup entries → affects **only current user**

- **Regedit** = Registry Editor (GUI tool to navigate/edit registry)

---

## ⚙️ Task Manager
- Built‑in Windows utility used to:
  - Monitor processes  
  - Check CPU/RAM usage  
  - Kill applications  
  - View startup apps  
  - Analyze performance  
- **Open using:** `taskmgr`

---

✅ These fundamentals are critical for SOC analysts because attackers often abuse **registry keys, services, scheduled tasks, and startup entries** for persistence. Knowing where to look helps detect compromises faster.
