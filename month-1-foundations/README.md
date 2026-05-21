# 📅 Day 9 – SOC Analyst 30-Day Challenge

Today was all about **Linux log analysis** — the part that really connects system administration with SOC investigations. Logs are the lifeblood of detection, so I focused on understanding how they’re generated, stored, rotated, and analyzed with tools like `grep`, `awk`, and `sed`.

---

## 📝 Topics I Covered
- Linux logging architecture: log flow, syslog/rsyslog/journald, severity levels
- Critical log locations: `auth.log`, `syslog`, `secure`, Apache/Nginx logs, `faillog`, `lastlog`
- Log rotation, retention, compression, and attacker log‑clearing techniques
- Threat hunting with `grep`: recursive search, regex, failed logins, timestamps, IP extraction
- `awk` for parsing logs: filtering fields, extracting usernames/IPs, counting SSH failures, identifying top attacker IPs, analyzing web server logs

---

## ⚙️ Hands-On Practice
- Checked `/var/log/auth.log` for failed SSH login attempts with `grep "Failed password"`.
- Used regex in `grep` to pull out timestamps and IP addresses from logs.
- Parsed logs with `awk '{print $1,$2,$3,$11}'` to extract usernames and IPs.
- Counted failed SSH attempts per IP with `awk` + `sort | uniq -c` to spot brute force patterns.
- Looked at Apache access logs to identify top attacker IPs hitting the server.

---

## 💡 Key Takeaways
- Logs tell the **story of the system** — knowing where they live and how they flow is critical for SOC work.
- Attackers often try to **clear logs** to hide tracks; understanding rotation and compression helps spot gaps.
- `grep` is powerful for quick hunts, but `awk` makes structured parsing way more efficient.
- SOC analysts must be comfortable moving between raw logs and filtered views to spot anomalies fast.

---

## 🎯 Next Steps
Tomorrow I’ll:
- Dive deeper into **`sed` fundamentals** for log manipulation and pattern replacement.
- Start exploring **Windows fundamentals** to balance Linux knowledge with SOC relevance across platforms.

---

### 🔗 Resources
- [Linux Log Analysis](ca://s?q=Linux_log_analysis_basics)
- [grep for Threat Hunting](ca://s?q=grep_threat_hunting_examples)
- [awk for Log Parsing](ca://s?q=awk_log_parsing_tutorial)
- [Log Rotation in Linux](ca://s?q=Linux_log_rotation_explained)

---

🔥 *Day 9 complete! Feeling the SOC vibe now — logs don’t look like random noise anymore, they’re evidence waiting to be read.*

