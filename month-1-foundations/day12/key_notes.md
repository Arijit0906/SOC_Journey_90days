# Sysmon (System Monitor)

Sysmon is a free Microsoft tool that acts like a surveillance camera for your operating system's internal activity. Unlike standard logs, it records deep, hidden details about what programs are doing in the background.

## Why Sysmon is Important for Security

### 1. Catches Hidden Hackers
Sysmon logs:
- Network connections
- File changes
- Loaded code/modules
- Process activities

These are activities that normal antivirus software often misses.

### 2. Creates a Digital Paper Trail
If a system becomes infected, Sysmon helps investigators understand:
- How the malware entered
- What processes were executed
- What files or registry keys were changed
- What network communications occurred

### 3. Feeds Security Systems
Sysmon structures detailed system activity into logs that can be forwarded to:
- SIEM platforms
- Security monitoring tools
- Threat detection systems

This allows automated alerting and faster incident response.

---

# The Core Difference

## Windows Security Logs
Windows Security Logs focus on:
- System status
- System health
- User authentication
- Login and logout events
- Access management

## Sysmon Logs
Sysmon focuses on deep technical behavior such as:
- Processes launching hidden child processes
- Background network connections
- DLL/module loading
- File creation activity
- Registry modifications
- PowerShell execution tracking

---

# Simple Summary

| Feature | Windows Security Logs | Sysmon Logs |
|---|---|---|
| Focus | User & system activity | Deep process behavior |
| Tracks Logins | ✅ Yes | ⚠️ Limited |
| Tracks Network Connections | ❌ Minimal | ✅ Detailed |
| Malware Investigation | ⚠️ Basic | ✅ Excellent |
| SIEM Integration | ✅ Yes | ✅ Advanced |
| Process Monitoring | ⚠️ Limited | ✅ Deep visibility |
****


## Sysmon Event IDs
<img width="1738" height="640" alt="image" src="https://github.com/user-attachments/assets/7b122ba2-b189-40db-a460-8746d6796571" />

## Sysmon Step-by-Step Workflow

## 1. The Trigger Event
An activity occurs on the endpoint.

### Example
A user accidentally runs a malicious script:
- `cmd.exe` launches
- The process attempts to download a malicious file from the internet

---

## 2. Kernel Interception
The Sysmon driver (`SysmonDrv.sys`) operates at the Windows kernel level.

It immediately intercepts the activity using:
- Windows Kernel Callbacks
- Low-level event monitoring

This happens before the malicious process can hide itself or terminate.

---

## 3. Filtering and Enrichment
The Sysmon driver passes the raw event data to the Sysmon service (`Sysmon.exe`).

The service then:

### Applies XML Configuration Rules
Sysmon checks the custom XML configuration file to determine:
- Whether the event should be ignored
- Or whether it should be logged

### Enriches the Event Data
If the event is kept, Sysmon adds valuable forensic details such as:
- SHA256 file hashes
- MD5/SHA1 hashes
- Process GUIDs
- Parent-child process relationships
- User context
- Network metadata

---

## 4. Local Logging
Sysmon writes the enriched event into:
- Windows Event Viewer
- `Applications and Services Logs/Microsoft/Windows/Sysmon/Operational`

### Common Event IDs
| Event ID | Description |
|---|---|
| 1 | Process Creation |
| 3 | Network Connection |
| 7 | Image/DLL Loaded |
| 11 | File Creation |
| 13 | Registry Modification |

---

## 5. SIEM Aggregation
A log forwarding agent continuously monitors Sysmon logs.

### Common Forwarders
- Winlogbeat
- Splunk Universal Forwarder
- Microsoft Sentinel Agent
- NXLog
- Fluent Bit

The forwarder sends the logs to a centralized SIEM platform.

### SIEM Platforms
- Splunk
- Microsoft Sentinel
- QRadar
- Elastic SIEM
- ArcSight

---

## 6. Analyst Detection
The SIEM analyzes incoming Sysmon events using:
- Detection rules
- Threat intelligence
- Behavioral analytics

### Example Detection
The SIEM flags:
```text
cmd.exe → outbound internet connection
```
<img width="896" height="646" alt="image" src="https://github.com/user-attachments/assets/a14bf989-0f2e-450a-bdcf-dca3fd1e6265" />

---
# Sysmon Event Field Descriptions
| Parameter | Meaning |
|---|---|
| RuleName | Name of the Sysmon rule that matched the event. |
| UtcTime | Exact event timestamp in UTC format. |
| ProcessGuid | Unique identifier assigned to the process instance. |
| ProcessId | Numeric Process ID (PID) of the created process. |
| Image | Full path of the executable that started. |
| FileVersion | Version number of the executable file. |
| Description | Human-readable description of the executable. |
| Product | Software product name associated with the executable. |
| Company | Company that created/signed the executable. |
| OriginalFileName | Original filename embedded inside the binary. |
| CommandLine | Exact command used to launch the process. |
| CurrentDirectory | Working directory from which process executed. |
| User | User account that launched the process. |
| LogonGuid | Unique identifier for the user logon session. |
| LogonId | Hexadecimal ID representing login session. |
| TerminalSessionId | Session number of the logged-in user session. |
| IntegrityLevel | Security privilege level of the process. |
| Hashes | Cryptographic hashes used for file identification. |
| ParentProcessGuid | Unique identifier of the parent process. |
| ParentProcessId | PID of the process that launched this process. |
| ParentImage | Full path of the parent executable. |
| ParentCommandLine | Exact command line of parent process. |
| ParentUser | User account running the parent process. |
