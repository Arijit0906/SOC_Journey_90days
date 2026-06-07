# What is Threat Intelligence?

Threat intelligence, also known as **Cyber Threat Intelligence (CTI)**, is evidence-based knowledge about cybersecurity threats, attackers, and their methods.

It transforms raw data into predictive, actionable guidance so that security teams can proactively block attacks rather than just reacting to breaches.

## Simple Definition

> Threat Intelligence is knowledge about cyber threats that helps security teams make better security decisions.

---

# Why Organizations Need Threat Intelligence

Without Threat Intelligence, security teams only react after attacks occur.

Threat Intelligence helps organizations:

## 1. Detect Threats Faster

- Identify malicious IPs, domains, and file hashes.
- Reduce investigation time.

## 2. Improve Incident Response

- Understand attacker behavior.
- Respond more effectively.

## 3. Prioritize Risks

- Focus on threats that actually affect the organization.
- Avoid wasting time on irrelevant alerts.

## 4. Enhance Threat Hunting

- Search proactively for known attacker activities.
- Discover hidden compromises.

## 5. Improve Security Controls

- Update firewall rules.
- Improve SIEM detection rules.
- Strengthen EDR monitoring.

---

# Data vs Information vs Intelligence

This is one of the most commonly asked interview questions.

| Level | Meaning | Example |
|---------|---------|---------|
| Data | Raw facts with no context | IP: 192.168.1.10 |
| Information | Data with context | IP contacted a malicious domain |
| Intelligence | Analyzed information leading to action | Domain is associated with a phishing campaign targeting banks |

---

# Summary

- Threat Intelligence converts threat data into actionable knowledge.
- Helps SOC teams detect and respond to attacks faster.
- Data → Information → Intelligence is a key concept.
- Good intelligence is actionable, relevant, accurate, timely, and contextual.
- The Intelligence Lifecycle consists of Direction, Collection, Processing, Analysis, Dissemination, and Feedback.

---

# Types of Threat Intelligence

## Strategic Intelligence (Why)

Business-focused intelligence used by management and executives for long-term security decisions.

## Tactical Intelligence (How)

Focuses on attacker TTPs and helps improve detection and defensive controls.

## Operational Intelligence (What)

Provides information about active attack campaigns, threats, and adversary activities.

## Technical Intelligence (Which)

Contains Indicators of Compromise (IOCs) such as:

- IP addresses
- Domains
- URLs
- File hashes

---

# What is a Threat Actor?

A **Threat Actor** is any individual, group, or organization that performs malicious activities against systems, networks, or organizations.

## Simple Definition

> A Threat Actor is the person or group behind a cyber attack.

---

# Hacktivists

## Definition

Hacktivists conduct cyber attacks to promote political, social, or ideological causes.

## Objectives

- Spread messages
- Protest organizations
- Gain publicity
- Disrupt services

---

# Insider Threats

## Definition

An Insider Threat is someone within the organization who intentionally or unintentionally causes harm.

### Types of Insider Threats

#### Malicious Insider

Purposefully steals data or damages systems.

**Example:**

- Employee steals customer database before leaving.

#### Negligent Insider

Causes incidents accidentally.

**Examples:**

- Clicking a phishing link.
- Sharing sensitive files improperly.

#### Compromised Insider

An attacker gains access to an employee account.

**Example:**

- Stolen credentials used by attackers.

---

# What is an IOC?

An **Indicator of Compromise (IOC)** is a piece of forensic evidence that suggests a system, network, or account may have been compromised by an attacker.

## Simple Definition

> IOCs are clues left behind by attackers that help security teams detect malicious activity.

Think of an IOC as a **fingerprint left at a crime scene**.

---

# IOC Lifecycle

An IOC generally follows this process:

```text
Threat Detected
       ↓
IOC Created
       ↓
Shared Through Threat Intelligence
       ↓
Added to SIEM/EDR
       ↓
Detection & Hunting
```

---

# What are TTPs?

**TTPs = Tactics + Techniques + Procedures**

They describe how attackers operate during an attack.

## Simple Definition

> TTPs are the methods and behaviors attackers use to achieve their objectives.

### Tactic (Why)

The attacker's goal or objective.

### Technique (How)

The method used to achieve the goal.

### Procedure (Implementation)

The exact implementation or step used by the attacker to perform a technique.

---

# Quick Reference

| Component | Meaning |
|------------|---------|
| Tactic | Why the attacker acts |
| Technique | How the attacker acts |
| Procedure | Exact steps taken |
| IOC | Evidence of compromise |
| Threat Intelligence | Actionable knowledge about threats |
| Threat Actor | Individual or group conducting attacks |

---

## Key Takeaways

- Threat Intelligence helps organizations move from reactive to proactive defense.
- Threat Actors can include hackers, insiders, hacktivists, cybercriminals, and nation-state groups.
- IOCs help identify compromised systems.
- TTPs explain how attackers operate.
- Effective Threat Intelligence improves detection, response, hunting, and risk management.
