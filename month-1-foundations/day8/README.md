# 📅 Day 8 – SOC Analyst 90-Day Challenge

Today was all about diving into **Linux fundamentals** and connecting them back to SOC analyst skills. I wanted to understand not just how to run commands, but how the OS works under the hood and why it matters in security operations.

---

## 📝 Topics I Covered
- What Linux is, a bit of **UNIX history**, and the difference between **kernel vs OS**
- How Linux works internally: kernel, shell, terminal, processes, userspace
- Popular **Linux distributions** (Ubuntu, Kali, CentOS, Arch) and why they matter in SOC work
- Filesystem hierarchy: `/`, `/etc`, `/var`, `/home`, `/bin`, `/proc`, `/tmp`
- Navigation mastery: `pwd`, `ls`, `cd`, `tree`
- File operations: `cp`, `mv`, `rm`, `mkdir`, `touch`
- Reading files: `cat`, `less`, `more`, `head`, `tail`
- Search mastery: `grep`, `find`, `locate`, `which`
- Permissions in depth: `chmod`, `chown`, rwx basics, octal notation
- Users & groups: `sudo`, `useradd`, `passwd`, `usermod`

---

## ⚙️ Hands-On Practice
- Explored the filesystem with `ls -la` and `tree` to see how directories are structured.
- Created and moved files around with `mkdir`, `touch`, `cp`, and `mv`.
- Practiced reading logs using `less` and `tail -f` (super useful for monitoring in real time).
- Used `grep` to search inside log files — this feels like the bread and butter of SOC work.
- Played with permissions using `chmod 755` and `chown`, and tested how access changes.
- Added a new user with `useradd` and set a password, then modified it with `usermod`.

---

## 💡 Key Takeaways
- Linux isn’t just another OS — understanding the **kernel vs userspace** helps explain how processes interact.
- The **filesystem hierarchy** is predictable, which makes log hunting and incident response faster.
- **Permissions** are critical: misconfigured `chmod` or `chown` can open doors for attackers.
- SOC analysts need to be comfortable with **searching logs efficiently** — `grep` is a lifesaver.
- Managing **users and groups** ties directly into access control and privilege escalation scenarios.

---

## 🎯 Next Steps
Tomorrow I’ll move deeper into **process monitoring, networking commands, and security tools** on Linux. The goal is to connect these fundamentals with real SOC workflows like log analysis and threat detection.

---

### 🔗 Resources
- [Linux Filesystem Hierarchy](ca://s?q=Explain_Linux_filesystem_hierarchy)
- [Linux Permissions](ca://s?q=Learn_Linux_permissions)
- [Linux Distributions](ca://s?q=Overview_of_Linux_distributions)
- [SOC Analyst Skills](ca://s?q=SOC_analyst_core_skills)

---

🔥 *Day 8 done! Feeling more confident with Linux basics — these commands already feel like the building blocks of SOC work.*
