# MITRE ATT&CK Framework – 14 Tactics

The MITRE ATT&CK Framework is a globally recognized knowledge base of adversary tactics and techniques based on real-world observations. It helps security professionals understand, detect, and defend against cyber threats throughout the attack lifecycle.

---

## 1. Reconnaissance

**Description:**
The attacker gathers information about the target before launching an attack.

**Examples:**

* Open-Source Intelligence (OSINT)
* Google searches
* LinkedIn research
* DNS lookups
* WHOIS queries

**Objective:**
Identify potential targets and collect valuable information for future attack stages.

---

## 2. Resource Development

**Description:**
The attacker acquires, creates, or compromises resources required to support an operation.

**Examples:**

* Registering domains
* Purchasing VPS servers
* Creating malware
* Setting up phishing infrastructure
* Obtaining stolen credentials

**Objective:**
Prepare the tools and infrastructure needed to conduct an attack.

---

## 3. Initial Access

**Description:**
The attacker gains an initial foothold within the target environment.

**Examples:**

* Phishing attacks
* Exploiting vulnerabilities
* Malicious USB devices
* Drive-by downloads
* Supply chain compromise

**Objective:**
Establish the first point of entry into the victim's network.

---

## 4. Execution

**Description:**
The attacker runs malicious code on a compromised system.

**Examples:**

* PowerShell commands
* Batch scripts
* Command Prompt (CMD)
* Malware execution
* Scheduled task execution

**Objective:**
Execute payloads to advance the attack.

---

## 5. Persistence

**Description:**
The attacker maintains access to the system even after reboots or user logouts.

**Examples:**

* Registry Run Keys
* Startup folders
* Scheduled tasks
* Service installation
* Web shells

**Objective:**
Ensure long-term access to compromised systems.

---

## 6. Privilege Escalation

**Description:**
The attacker gains higher-level permissions than initially obtained.

**Examples:**

* UAC bypass
* Exploiting local vulnerabilities
* Token manipulation
* Credential abuse

**Objective:**
Obtain administrative or elevated privileges.

---

## 7. Defense Evasion

**Description:**
The attacker attempts to avoid detection by security controls and monitoring tools.

**Examples:**

* Antivirus evasion
* Log deletion
* File obfuscation
* Process injection
* Masquerading

**Objective:**
Remain undetected while conducting malicious activities.

---

## 8. Credential Access

**Description:**
The attacker seeks to steal account credentials and authentication material.

**Examples:**

* Keylogging
* Password dumping
* Credential harvesting
* Browser credential theft
* LSASS memory dumping

**Objective:**
Gain access to user and administrative accounts.

---

## 9. Discovery

**Description:**
The attacker gathers information about systems, users, and network resources after gaining access.

**Examples:**

* `whoami`
* `hostname`
* `ipconfig`
* `net user`
* Network scanning

**Objective:**
Understand the environment and identify valuable targets.

---

## 10. Lateral Movement

**Description:**
The attacker moves from one compromised system to another within the network.

**Examples:**

* Remote Desktop Protocol (RDP)
* PsExec
* SMB shares
* Remote services
* SSH sessions

**Objective:**
Expand access throughout the environment.

---

## 11. Collection

**Description:**
The attacker gathers information of interest from compromised systems.

**Examples:**

* Documents
* Emails
* Screenshots
* Browser data
* Database records

**Objective:**
Collect sensitive or valuable information.

---

## 12. Command and Control (C2)

**Description:**
The attacker communicates with compromised systems through an external control channel.

**Examples:**

* HTTPS beaconing
* Reverse shells
* DNS tunneling
* Web-based C2 channels
* Encrypted communications

**Objective:**
Maintain remote control over compromised devices.

---

## 13. Exfiltration

**Description:**
The attacker transfers stolen data outside the organization's environment.

**Examples:**

* Cloud storage uploads
* FTP transfers
* Web uploads
* Email attachments
* Data synchronization tools

**Objective:**
Remove collected data from the victim's network.

---

## 14. Impact

**Description:**
The attacker achieves their final objective and causes disruption, destruction, or financial damage.

**Examples:**

* Ransomware deployment
* Data destruction
* Service disruption
* System shutdowns
* Data manipulation

**Objective:**
Achieve the intended effect of the attack.

---

## Attack Flow Overview

```text
Reconnaissance
      ↓
Resource Development
      ↓
Initial Access
      ↓
Execution
      ↓
Persistence
      ↓
Privilege Escalation
      ↓
Defense Evasion
      ↓
Credential Access
      ↓
Discovery
      ↓
Lateral Movement
      ↓
Collection
      ↓
Command and Control (C2)
      ↓
Exfiltration
      ↓
Impact
```
# ATT&CK Navigator

## Overview

ATT&CK Navigator is a web-based visualization tool developed to help security teams analyze and map ATT&CK techniques across their environment.

### SOC Team Use Cases

* Map security detections to ATT&CK techniques
* Measure detection coverage
* Identify visibility gaps
* Prioritize defensive improvements
* Track threat hunting activities

### Benefits

* Visual representation of security coverage
* Easy identification of blind spots
* Supports threat intelligence analysis
* Improves detection engineering

---

# ATT&CK Groups

## Overview

ATT&CK Groups represent threat actor organizations that conduct cyber operations. These groups are tracked based on their known behaviors, tools, and attack patterns.

### Examples of Threat Groups

* APT29 (Cozy Bear)
* Lazarus Group
* FIN7
* APT28 (Fancy Bear)
* MuddyWater

### MITRE Tracks

* Group profiles and aliases
* Attack techniques used
* Malware and tools associated with the group
* Campaign activities
* Historical attack patterns

### Why It Matters

Understanding threat groups helps defenders anticipate attacker behavior and improve detection strategies.

---

# ATT&CK Software

## Overview

ATT&CK Software refers to tools, malware, frameworks, and utilities used by attackers during cyber operations.

| Tool          | Purpose                      |
| ------------- | ---------------------------- |
| Mimikatz      | Credential dumping           |
| PsExec        | Remote execution             |
| Cobalt Strike | Command & Control (C2)       |
| Empire        | PowerShell post-exploitation |
| Metasploit    | Exploitation framework       |
| BloodHound    | Active Directory enumeration |

### SOC Analyst Usage

Security analysts map detected tools to ATT&CK techniques to better understand attacker activities.

---

# EDR Alert → ATT&CK Mapping

## Overview

Endpoint Detection and Response (EDR) alerts are frequently mapped to ATT&CK techniques during investigations.

### Example Workflow

```text
EDR Alert
    ↓
Identify Suspicious Activity
    ↓
Map Activity to ATT&CK Technique
    ↓
Determine ATT&CK Tactic
    ↓
Assess Impact
    ↓
Investigate and Respond
```

### Example

```text
Alert: PowerShell Executed with Encoded Command
        ↓
Technique: Command and Scripting Interpreter
        ↓
ATT&CK ID: T1059.001
        ↓
Tactic: Execution
```

### Benefits

* Standardized investigations
* Faster incident response
* Better threat intelligence correlation
* Improved reporting and documentation

---

# The 7 Stages of the Cyber Kill Chain

## Overview

The Cyber Kill Chain is a security model developed to describe the stages of a cyber attack from planning to execution.

### 1. Reconnaissance

The attacker gathers information about the target.

**Examples:**

* OSINT research
* Domain enumeration
* Employee profiling

---

### 2. Weaponization

The attacker creates or prepares a malicious payload.

**Examples:**

* Malware creation
* Exploit packaging
* Weaponized documents

---

### 3. Delivery

The payload is delivered to the target.

**Examples:**

* Phishing emails
* Malicious attachments
* Drive-by downloads

---

### 4. Exploitation

The vulnerability is triggered to gain access.

**Examples:**

* Software exploits
* Macro execution
* Browser vulnerabilities

---

### 5. Installation

Malware is installed on the victim's system.

**Examples:**

* Trojans
* Backdoors
* Persistence mechanisms

---

### 6. Command & Control (C2)

The attacker establishes communication with the compromised system.

**Examples:**

* HTTPS beaconing
* Reverse shells
* DNS tunneling

---

### 7. Actions on Objectives

The attacker performs their final mission.

**Examples:**

* Data theft
* Ransomware deployment
* Data destruction
* Espionage

---

# Cyber Kill Chain Attack Flow

```text
Reconnaissance
      ↓
Weaponization
      ↓
Delivery
      ↓
Exploitation
      ↓
Installation
      ↓
Command & Control
      ↓
Actions on Objectives
```

---

# MITRE ATT&CK vs Cyber Kill Chain

## Comparison Table

| Cyber Kill Chain                 | MITRE ATT&CK                     |
| -------------------------------- | -------------------------------- |
| High-level attack stages         | Detailed attacker behaviors      |
| 7 stages                         | 14 tactics                       |
| Focuses on attack lifecycle      | Focuses on attacker techniques   |
| Simpler framework                | More comprehensive framework     |
| Strategic perspective            | Operational perspective          |
| Linear attack model              | Flexible attack model            |
| Useful for understanding attacks | Useful for detection and defense |

---

## Key Difference

### Cyber Kill Chain

Answers:

```text
"Where is the attacker in the attack lifecycle?"
```

### MITRE ATT&CK

Answers:

```text
"How is the attacker performing the attack?"
```

---

# Summary

* ATT&CK Navigator helps visualize ATT&CK techniques and security coverage.
* ATT&CK Groups represent tracked threat actor organizations.
* ATT&CK Software includes tools and malware used by attackers.
* SOC analysts map EDR alerts to ATT&CK techniques during investigations.
* The Cyber Kill Chain describes the seven major stages of a cyber attack.
* MITRE ATT&CK provides a deeper and more detailed understanding of attacker behaviors than the Cyber Kill Chain.
