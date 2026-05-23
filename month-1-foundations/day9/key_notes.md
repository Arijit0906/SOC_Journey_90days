# 📝 Intro to Logs – Quick Notes

- **Logs = digital records of system activity**  
  Every action (login, file access, network connection, errors) creates a log entry.

- **Why logs are important?**  
  They help answer key investigation questions:  
  - What happened?  
  - When?  
  - Where?  
  - Who did it?  
  - Was it successful?  
  - What was the impact?  

- **Basic components of a log entry:**  
  - 🕒 Timestamp (when event occurred)  
  - 💻 Source (system/app name)  
  - 📌 Event type (login, error, request)  
  - 🌐 Extra details (IP address, username, user-agent)

---

## 🚨 Log Severity Levels (Must Know for Interviews)

| Level | Meaning                | SOC Priority Example |
|-------|------------------------|----------------------|
| 0     | Emergency              | System unusable |
| 1     | Alert                  | Immediate action required (e.g., critical DB corruption) |
| 2     | Critical               | Serious issue (e.g., primary hard drive full) |
| 3     | Error                  | Operational problem (e.g., app failed to start) |
| 4     | Warning                | Suspicious (e.g., high memory usage) |
| 5     | Notice                 | Normal but significant |
| 6     | Info                   | Standard logs (e.g., service restarted) |
| 7     | Debug                  | Troubleshooting |

---

## ⚙️ systemd & Journald

- **systemd** → Master control program of Linux. First process that starts at boot, stays until shutdown.  
- **journald (daemon)** → Collects logs from the OS into one central place.  
- **journalctl (utility)** → Command to view/search logs collected by journald.  

**Difference:**  
- `journald` = background worker collecting logs.  
- `journalctl` = tool to read those logs.  

---

## 📖 Common journalctl Commands

- View all logs: `journalctl`  
- Real-time logs: `journalctl -f`  
- Logs for a service: `journalctl -u apache2`  
- Current boot logs: `journalctl -b`  
- Errors only: `journalctl -p err`  

**Filter by Time:**  
- Today: `journalctl --since today`  
- Yesterday: `journalctl --since yesterday --until today`  
- Last hour: `journalctl --since "1 hour ago"`

---

## 🔧 systemctl Basics (Service Control)

Using Apache as example:  
- Check status: `systemctl status apache2`  
- Start: `systemctl start apache2`  
- Stop: `systemctl stop apache2`  
- Restart: `systemctl restart apache2`  
- Enable at boot: `systemctl enable apache2`

---

## 👀 Live Log Monitoring

- Watch brute force attempts in real time:  
  - `tail -f /var/log/auth.log`  
  - `journalctl -f`

---

# 🧪 Lab Notes: Tracking Failed Local Sudo Logins

## 📌 Context & Problem
During local login tests using `sudo su`, the terminal locked after three failed entries with the message:  
`sudo: 3 incorrect password attempts`

Running `grep "Failed password"` found nothing. This is because **"Failed password" only tracks remote network logins (like SSH)**. Local command failures use different tracking keywords hidden inside the system logs.

---

## 🗂️ How the System Logs the 3 Attempts (`/var/log/auth.log`)
- **Attempts 1 & 2 (Password Typing Errors):** Stored as `authentication failure` or `password check failed`.
- **Attempt 3 (System Lockout):** Stored as `incorrect password attempts`.

### 🔍 Commands
```bash
# 1. Find individual typing mistakes (Attempts 1 & 2)
sudo grep -E "authentication failure|password check failed" /var/log/auth.log

# 2. Find the final lockout event (Attempt 3)
sudo grep "incorrect password attempts" /var/log/auth.log

# 3. Universal Search (Finds ALL local and remote login failures)
sudo grep -E "authentication failure|password check failed|incorrect password attempts|Failed password" /var/log/auth.log
```
---
# Core `grep` Options (Must Know)

| Command Option | Purpose                          |
|----------------|----------------------------------|
| `-i`           | Ignore case (insensitive)        |
| `-n`           | Show line numbers                |
| `-v`           | Invert match                     |
| `-c`           | Count matches                    |
| `-r`           | Recursive search                 |
| `-E`           | Extended regex                   |
| `-w`           | Exact word match                 |
| `-A`           | Show lines after match           |
| `-B`           | Show lines before match          |
| `-C`           | Show context lines around match  |

---

# Advanced `grep` Examples & Regex Cheat Sheet

## Count Failed Logins

```bash
grep -c "Failed password" /var/log/auth.log
```

- `-c` → Counts how many matching lines exist.
- Useful for checking failed SSH login attempts.

---

# Ignore Errors While Searching Success Logs

```bash
grep -i "success" /var/log/syslog | grep -iv "error"
```

### Explanation

| Command Part | Meaning |
|---|---|
| `grep -i "success"` | Searches for `success` ignoring case |
| `grep -iv "error"` | Removes lines containing `error`, `Error`, or `ERROR` |

### Result
Shows only clean success messages without any errors.

---

# Extended Regex (`-E`)

```bash
grep -E "(sshd|cron|systemd)" /var/log/syslog
```

### Explanation

- `-E` → Enables Extended Regular Expressions.
- `(sshd|cron|systemd)` → Matches any one of these words.

### Matches
- `sshd`
- `cron`
- `systemd`

---

# Basic Regex Symbols

| Symbol | Meaning | Example |
|---|---|---|
| `^` | Start of line | `grep "^Jan" auth.log` |
| `$` | End of line | `grep "root$" auth.log` |
| `.` | Any single character | `grep "r..t" file.txt` |
| `*` | Zero or more characters | `grep "lo*g" file.txt` |
| `+` | One or more characters | `grep -E "lo+g" file.txt` |
| `[]` | Character set | `grep "[0-9]" file.txt` |
| `\` | Escape special character | `grep "\$HOME" file.txt` |

---

# Quick Tips

## Search Recursively

```bash
grep -r "password" /etc/
```

## Show Line Numbers

```bash
grep -n "root" /etc/passwd
```

## Exact Word Match

```bash
grep -w "root" /etc/passwd
```

## Show Context Lines

```bash
grep -C 2 "error" /var/log/syslog
```

- `-C 2` → Shows 2 lines before and after the match.
---
# Common Beginner Mistakes

| Wrong Command | Better Command | Why? |
|---|---|---|
| `uniq file` | `sort file | uniq` | `uniq` only removes consecutive duplicate lines, so sorting first groups duplicates together. |

---

# LAB — Find Top Failed Login Attackers

```bash
grep "Failed password" auth.log | awk '{print $11}' | sort | uniq -c | sort -nr | head
```

---

# Step-by-Step Breakdown

| Command | Purpose |
|---|---|
| `grep "Failed password"` | Filters the log to show only failed login attempts |
| `awk '{print $11}'` | Extracts the 11th column, usually the attacker's IP address |
| `sort` | Groups identical IP addresses together |
| `uniq -c` | Counts repeated IP addresses |
| `sort -nr` | Sorts numerically in reverse order (highest first) |
| `head` | Displays the top 10 attackers |

---

# Example Output

```bash
120 192.168.1.10
85  10.0.0.5
44  172.16.0.2
```

### Meaning
- `120` → Number of failed login attempts
- `192.168.1.10` → Attacker IP address

---

# Why This Pipeline Is Powerful

This command helps:

- Detect brute-force SSH attacks
- Identify suspicious IP addresses
- Analyze authentication logs quickly
- Practice real-world Linux log analysis

---

To save the results into a file:

```bash
grep "Failed password" auth.log | awk '{print $11}' | sort | uniq -c | sort -nr | head > attackers.txt
```

This creates a report named `attackers.txt`.

