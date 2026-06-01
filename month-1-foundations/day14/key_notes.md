# What is Active Directory (AD)?

## Definition

Active Directory (AD) is a directory service developed by Microsoft that stores and manages information about users, computers, groups, printers, and other resources in a network.

It provides:
- Centralized Authentication
- Centralized Authorization
- Centralized Management

## Think of AD as:

> The central identity database of an organization.

## Why do SOC Analysts care so much about it?

Because if a hacker sneaks past the front door, their ultimate goal is to break into that Central Security Desk (Active Directory). If the hacker takes over AD, they can create a fake ID badge that lets them into every single room, server, and file in the entire company.

# Active Directory Core Components
<img width="1220" height="703" alt="image" src="https://github.com/user-attachments/assets/b18f657b-6a80-44e9-84b0-c8d486bc2b5c" />

## 1. Domain

A Domain is a logical collection of users, computers, groups, and resources managed by Active Directory.

### Example

Company ABC has:

- Employees
- Laptops
- Servers
- Printers

All are managed under:

`abc.local`

This becomes the AD Domain.

---

## 2. Domain Controller (DC)

A Domain Controller (DC) is a server that runs Active Directory Domain Services (AD DS) and authenticates users within a domain.

### Think:

> Active Directory lives on the Domain Controller.

---

## 3. Objects

### Definition

Everything stored in Active Directory is called an Object.

### Examples

#### User

- arijit
- john
- admin

#### Computer

- PC001
- LAPTOP01
- SERVER01

#### Group

- Domain Admins
- IT Team
- HR Team

---

## 4. Organizational Unit (OU)

An Organizational Unit (OU) is a container used to organize Active Directory objects.

### Think of OUs as folders.

### Example Company

```text
Company
│
├── HR
├── Finance
├── IT
└── Sales
```

---

## 5. Forest

A Forest is the highest-level AD structure containing one or more domains.

### Example

```text
Forest
│
├── company.local
│
├── europe.company.local
│
└── asia.company.local
```


# Active Directory Protocols

Active Directory primarily relies on three major protocols for identity management, authentication, and communication:

---

## 1. LDAP (Lightweight Directory Access Protocol)

LDAP is used to communicate with Active Directory and retrieve information.

### Purpose

Query and manage AD objects such as:

- Users
- Groups
- Computers
- Organizational Units (OUs)

### Think:

> LDAP = Search Engine for Active Directory

---

## 2. Kerberos

Kerberos is a ticket-based computer network authentication protocol designed to securely verify the identity of users and servers over an untrusted network.

### Purpose

- Authenticates users
- Authenticates services
- Prevents password transmission across the network
- Uses tickets instead of repeatedly sending credentials

---

## 3. DNS (Domain Name System)

### What does DNS do?

DNS helps systems locate resources on a network.

### Purpose

- Resolves hostnames to IP addresses
- Helps clients locate Domain Controllers
- Enables communication between systems and services

### Example

```text
dc01.company.local
        ↓
   192.168.1.10
```

Without DNS, clients would not know where to find Active Directory services.

---

# Kerberos Components

| Component | Meaning |
|-----------|---------|
| KDC | Key Distribution Center (It issues tickets.) |
| TGT | Ticket Granting Ticket (It is the first ticket received.) |
| TGS | Ticket Granting Service (Allows access to specific services such as file servers and email servers.) |
| SPN | Service Principal Name |

---

## Kerberos Authentication Flow

```text
User Login
    │
    ▼
Request TGT from KDC
    │
    ▼
KDC Issues TGT
    │
    ▼
Request TGS using TGT
    │
    ▼
KDC Issues Service Ticket
    │
    ▼
Access File Server / Email Server / Other Services
```

<img width="1175" height="490" alt="image" src="https://github.com/user-attachments/assets/89b66b4b-a5c2-4eaa-80e7-5feb7fa9ef77" />

# NTLM (NT LAN Manager)

NTLM (NT LAN Manager) is a suite of Microsoft security protocols used for user authentication and network resource access.

It was the primary authentication protocol in older Windows environments before Kerberos became the default authentication protocol in Active Directory.

---

## Purpose of NTLM

NTLM is used to:

- Authenticate users
- Verify credentials
- Allow access to network resources
- Support authentication when Kerberos cannot be used

---

## How NTLM Works

```text
User Enters Password
        │
        ▼
Password Converted to Hash
        │
        ▼
Client Sends Authentication Request
        │
        ▼
Server Sends Challenge
        │
        ▼
Client Responds Using Password Hash
        │
        ▼
Server Verifies Response
        │
        ▼
Access Granted
```

---

# NTLM vs Kerberos

| Feature | NTLM | Kerberos |
|----------|----------|----------|
| Speed | Slower (verifies every request) | Faster (reuses tickets) |
| Security | Weaker (vulnerable to relay attacks) | Stronger (uses advanced cryptography) |
| Trust Model | Peer-to-peer verification | Centralized (Key Distribution Center) |
| Authentication | Client proves identity to server | Mutual authentication (both prove identity to each other) |
| Credentials | Uses password hashes | Uses encrypted tickets |
| Scalability | Less efficient in large environments | Better suited for enterprise environments |

---

## Encryption and Hashing

### NTLM

NTLM relies primarily on hashing functions rather than ticket-based authentication.

Commonly associated with:

- NT Hashes
- Challenge-Response Authentication

### Kerberos

Kerberos uses true symmetric-key encryption algorithms and ticket-based authentication.

Commonly associated with:

- AES Encryption
- Ticket Granting Tickets (TGTs)
- Service Tickets

---

## Why SOC Analysts Care About NTLM

NTLM is frequently targeted by attackers because it can be abused in several attacks, including:

- NTLM Relay Attacks
- Pass-the-Hash (PtH)
- Credential Theft
- Lateral Movement

### Example

```text
Attacker Steals NTLM Hash
          │
          ▼
Uses Hash Instead of Password
          │
          ▼
Authenticates to Other Systems
          │
          ▼
Moves Across Network
```

This is known as a **Pass-the-Hash (PtH)** attack.

---


# Group Policy (GPO)

## What is GPO?

### Definition

A Group Policy Object (GPO) is a set of rules and configurations that can be applied to users and computers in an Active Directory environment.

### Think:

> GPO = Centralized Security Settings

Instead of configuring 1000 computers individually:

```text
Admin
  ↓
Create GPO
  ↓
Apply to Domain
  ↓
1000 Computers Updated
```

### Common GPO Uses

- Password Policies
- Account Lockout Policies
- Desktop Restrictions
- Software Deployment
- Windows Firewall Configuration
- Security Settings
- Login Scripts
- USB Device Restrictions

---

# Active Directory Attacks & Detection

## 1. Pass-the-Hash (PtH)

One of the most famous Windows attacks.

### Concept

Normally:

```text
User
  ↓
Password
  ↓
Authentication
```

But in Pass-the-Hash:

```text
Attacker
     ↓
Steals NTLM Hash
     ↓
Uses Hash Directly
     ↓
Authentication Success
     ↓
No Password Needed
```

---

## Why It Works

Windows stores NTLM hashes in memory and system databases.

Attackers can extract these hashes using tools such as:

- Mimikatz
- secretsdump

Once the hash is stolen, the attacker may authenticate without ever knowing the user's actual password.

---

## Attack Flow

```text
Compromised PC
      ↓
Dump NTLM Hash
      ↓
Use Hash on Another System
      ↓
Lateral Movement
      ↓
Privilege Escalation
      ↓
Domain Compromise
```

---

## Detection

SOC analysts should look for:

- Authentication from unusual hosts
- Multiple systems accessed rapidly
- NTLM authentication spikes
- Credential dumping activity
- Lateral movement behavior
- Suspicious administrative logins

### Indicators of Compromise (IOCs)

```text
Unusual NTLM Logons
        +
Credential Dumping
        +
Rapid Lateral Movement
        =
Potential Pass-the-Hash Attack
```

---

## SOC Alert Example

```text
Alert Name: Credential Dumping Detected

Process:
mimikatz.exe

Severity:
🚨 High Severity

Recommended Action:
- Isolate Host
- Investigate User Activity
- Check Lateral Movement
- Reset Compromised Credentials
- Review Domain Controller Logs
```

---
# 2. Pass-the-Ticket (PtT)

Pass-the-Ticket (PtT) is the Kerberos version of Pass-the-Hash.

## Concept

Instead of stealing a password or NTLM hash, the attacker steals a Kerberos ticket and reuses it to authenticate.

### Attack Flow

```text
User Login
     ↓
Receives TGT
     ↓
Attacker Steals TGT
     ↓
Attacker Reuses Ticket
     ↓
Authentication Success
```

### Why It Works

Kerberos trusts valid tickets issued by the Key Distribution Center (KDC).

If an attacker obtains a valid Ticket Granting Ticket (TGT) or service ticket, they may be able to impersonate the user without knowing the password.

### Detection

Look for:

- Ticket usage from different hosts
- Unusual Kerberos activity
- Lateral movement patterns
- Abnormal ticket lifetimes
- Logins occurring from unexpected systems

### SOC Indicators

```text
Kerberos Ticket Used
       +
Different Source Host
       +
Multiple Systems Accessed
       =
Potential Pass-the-Ticket Attack
```

---

# 3. Kerberoasting

## What is Kerberoasting?

Kerberoasting is a post-exploitation attack that targets Service Accounts associated with Service Principal Names (SPNs).

### Why Service Accounts?

Many organizations use service accounts such as:

- SQLService
- BackupService
- WebService

These accounts often have:

- Old passwords
- Weak passwords
- Elevated privileges

### Attack Flow

```text
Find SPN
    ↓
Request TGS
    ↓
Extract Ticket
    ↓
Offline Crack
    ↓
Password Recovered
```

### Why It Works

A user can request a Ticket Granting Service (TGS) ticket for a service account.

The ticket contains data encrypted using the service account's password hash.

Attackers can extract the ticket and perform offline password cracking without generating additional authentication attempts.

### Detection

Look for:

- Large numbers of TGS requests
- Requests for multiple service accounts
- Abnormal Kerberos activity
- Unusual service ticket requests

### SOC Indicators

```text
Many TGS Requests
        +
Service Accounts Targeted
        +
Password Cracking Activity
        =
Potential Kerberoasting
```

---

# 4. AS-REP Roasting

## What is AS-REP Roasting?

AS-REP Roasting is similar to Kerberoasting but targets accounts that have Kerberos pre-authentication disabled.

### Why It Works

Normally:

```text
User
   ↓
Pre-Authentication
   ↓
KDC Issues Response
```

With pre-authentication disabled:

```text
Attacker
    ↓
Requests AS-REP
    ↓
Receives Encrypted Response
    ↓
Offline Password Cracking
```

### Attack Flow

```text
Find Vulnerable User
        ↓
Request AS-REP
        ↓
Receive Response
        ↓
Offline Crack
        ↓
Password Recovered
```

### Detection

Look for:

- Accounts with pre-authentication disabled
- Unusual AS-REQ requests
- Enumeration of user accounts
- Password cracking activity

### SOC Indicators

```text
AS-REP Requests
        +
No Pre-Authentication
        +
Password Cracking
        =
Potential AS-REP Roasting
```

---

# 5. DCSync Attack

## What is DCSync?

A DCSync attack occurs when an attacker pretends to be a Domain Controller and requests password hashes from a legitimate Domain Controller.

### Visual

```text
Attacker
    ↓
"I am DC"
    ↓
Request Password Hashes
    ↓
Domain Controller Responds
```

### Result

The attacker can obtain:

- All User Hashes
- Domain Administrator Hashes
- Service Account Hashes
- KRBTGT Hash

Including:

- KRBTGT
- Administrator
- Domain Admins

### Why It Is Dangerous

The KRBTGT account is used by Kerberos to sign tickets.

If attackers obtain the KRBTGT hash, they may create forged Kerberos tickets and maintain long-term access to the domain.

### Attack Flow

```text
Compromise Privileged Account
          ↓
Gain Replication Rights
          ↓
Perform DCSync
          ↓
Receive Password Hashes
          ↓
Domain Compromise
```

### Detection

Look for:

- Directory replication requests from non-Domain Controllers
- Replication activity originating from workstations
- Unusual use of replication privileges
- Requests for sensitive account hashes

### SOC Indicators

```text
Replication Request
         +
Non-DC Source
         +
Sensitive Account Access
         =
Potential DCSync Attack
```

### Severity

```text
Alert Name: DCSync Activity Detected

Severity:
🚨 Critical

Impact:
Potential Full Domain Compromise

Recommended Action:
- Investigate Source System
- Reset Compromised Credentials
- Review Replication Permissions
- Monitor Domain Controllers
- Consider KRBTGT Password Reset
```
