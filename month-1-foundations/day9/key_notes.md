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
Core grep Options (Must Know)
Command	Purpose
-i	Ignore case (insensitive)
-n	Show line numbers
-v	Invert match
-c	Count matches
-r	Recursive search
-E	Extended regex
-w	Exact word
-A	Lines after
-B	Lines before
-C	Context lines

---

	• Error

-c Count Failed Logins
grep -c "Failed password" /var/log/auth.log

🚀 The Command to Hide Errors
Run this command to search for "success" while ignoring case, and automatically filter out anything containing "error"
grep -i "success" /var/log/syslog | grep -iv "error"

grep -iv "error": Inverts the match. It throws away any line containing error, Error, or ERROR, leaving you with pure success messages.

-E -Extended regex
grep -E "(sshd|cron|systemd)" /var/log/syslog

Basic Regex Symbols
Symbol	Meaning
^	Start of line( grep "^Jan" auth.log )
$	End of line( grep "root$" auth.log )
.	Any character
*	Zero or more
+	One or more
[]	Character set
`	`
\	Escape

Common Beginner Mistakes
Wrong - uniq file
Better - sort file | uniq


LAB

grep "Failed password" auth.log | awk '{print $11}' | sort | uniq -c | sort -nr | head

• grep "Failed password": Filters the log to show only lines containing failed login attempts.
• awk '{print $11}': Extracts the 11th column of those lines, which is typically the attacker's IP address.
• sort: Alphabetically groups identical IP addresses together so they can be counted.
• uniq -c: Counts the consecutive occurrences of each IP address, creating a frequency list.
• sort -nr: Sorts the counted list numerically (-n) and in reverse order (-r) from highest to lowest.
• head: Displays only the top 10 results, revealing your most frequent attackers

