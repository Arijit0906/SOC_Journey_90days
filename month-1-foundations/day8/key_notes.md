# What is Operating System (OS)?

OS is a software responsible for managing hardware and software resources of a system.

## Example
Think of the OS like the conductor of an orchestra. The conductor doesn't play the instruments, but they ensure every musician (hardware) and every piece of music (software) works together at the right time.

| Resource Type | Examples | OS Management Role |
|---|---|---|
| Hardware | CPU, RAM, Disk, GPU | Allocation: Ensuring every app has the "power" it needs to run |
| Software | Files, Drivers, Apps | Coordination: Ensuring apps don't conflict and have access to data |

---
# What is Kernel?

The kernel is the core of the operating system(OS) that manages hardware and system resources.

---

<img width="506" height="600" alt="image" src="https://github.com/user-attachments/assets/301bdec2-f077-4708-9f39-ee82aa61d014" />

---
# What is Terminal?

A Terminal is essentially a text-based user interface for interacting with computers. It allows users to execute commands and view the results, as well as control applications running on the computer.

A terminal can be used to access the command line interface (CLI) of an operating system, such as Windows or Linux.

---

# What is Shell?

A computer shell is a program that acts as a user interface for an operating system (OS), serving as an intermediary between the user and the core system (kernel). It interprets commands typed by the user or read from a script to interact with system resources.

- The shell is the program running inside the terminal.
- The shell is a user interface that takes your commands and translates them for the kernel.

---

# What is Linux?

Linux is an operating system kernel — the core software that connects hardware (CPU, RAM, disk, network card) to software (apps, browsers, tools).

---

# What Happens When Linux Boots?
Linux boot process is like watching a relay race where each runner passes a baton to the next.

## 1. BIOS / UEFI (The Hardware Check)

When you press the power button, the BIOS (or modern UEFI) wakes up.

- Checks if hardware (RAM, Keyboard, Disk) is working.
- Finds the hard drive containing the operating system.

## 2. Bootloader / GRUB (The Menu)

Once the hardware is ready, it hands control to a small program called GRUB.

- Shows boot menu if multiple OS are installed.
- Loads the Linux Kernel into memory.

## 3. The Kernel (The Brain)

The Kernel is the core of Linux.

- Sets up CPU, memory, and device drivers.
- Prepares the system to run software.

## 4. systemd / Init (The Manager)

The Kernel starts one program called systemd.

- Starts background services like networking, sound, and login manager.
- Turns a running kernel into a working system.

## 5. Login Prompt (The Finish Line)

The system presents a GUI login screen or CLI prompt.

- Waits for the user to log in and start working.

---

# Linux Filesystem Hierarchy Cheat Sheet

## `/`
Root directory — the top of the Linux filesystem.

---

## `/etc`
System-wide configuration files.

| File/Directory | Purpose |
|---|---|
| `/etc/passwd` | stores public user account information (like UIDs, home directories, and shells) and is readable by all users |
| `/etc/shadow` | Stores encrypted passwords. It is highly secured and restricted, readable only by the root user|
| `/etc/hostname` | System hostname |
| `/etc/network` | Network configuration |
| `/etc/ssh` | SSH configuration |

---

## `/var`
Variable data written during system operation.

### `/var/log`
System and application logs.

| File | Purpose |
|---|---|
| `/var/log/auth.log` | Authentication logs (like SSH logins, sudo usage, failed password attempt)|
| `/var/log/syslog` | General system logs (like Kernel messages, service starts/stops, system errors, and hardware events)|
| `/var/log/kern.log` | Kernel logs (Hardware faults, out-of-memory (OOM) kills, firewall drops)|
| `/var/log/nginx/` | Nginx logs (Web traffic routing, reverse proxy errors)|
| `/var/log/apache2/` | Apache logs (Virtual host configurations, .htaccess blocks, PHP errors)|

### `/var/www`
Default web server directory.

- Stores website files.
- Attackers may upload malicious web shells here.

### `/var/tmp`
Temporary files that survive reboot.

- Common malware hiding location.

### `/var/spool`
Stores queued tasks.

| Path | Purpose |
|---|---|
| `/var/spool/cron` | Scheduled cron jobs |

### `/var/run` or `/run`
Stores runtime information since boot.

---

## `/usr`
User programs and libraries.

### `/usr/bin`
Main user command binaries.

| Common Commands |
|---|
| python |
| gcc |
| git |
| curl |
| wget |
| vim |

### `/usr/sbin`
Administrative binaries.

| Common Commands |
|---|
| sshd |
| iptables |
| tcpdump |

### `/usr/lib`
Shared libraries (`.so` files).

- Linux equivalent of Windows `.dll` files.

---

## `/sys`
Hardware and kernel interface.

- Provides information about devices and drivers.

---

## `/run`
Runtime system information.

- Stores temporary runtime data since boot.

---

## `/proc`
Virtual filesystem for live process and kernel information.

- Used for process analysis and system monitoring.

---

# What’s the Difference Between `/` and `/root`?

| Directory | Meaning |
|---|---|
| `/` | Root directory — top of entire filesystem |
| `/root` | Home directory of the root user |

### Analogy
`/` is the entire building, while `/root` is the CEO’s private office inside that building.

---

# Why is `/tmp` Dangerous?

The `/tmp` directory is considered dangerous because it is world-writable, meaning every user and process can create files there.

## Reasons

- Malware Staging: Attackers download malicious files here.
- Execution Hub: Scripts can often run directly from `/tmp`.
- Wiping Evidence: Files are deleted after reboot.

## SOC Analyst Tip

```bash
ls -la /tmp
```

Use this command to check for hidden or suspicious files.

---

# Important Definitions

| Term | Full Form |
|---|---|
| BIOS | Basic Input/Output System |
| UEFI | Unified Extensible Firmware Interface |
| GRUB | GRand Unified Bootloader |

---
# AWK Command Cheat Sheet

## Basic Syntax

```bash
awk '{print $1}' file
```

- `$1` = First column
- `$2` = Second column

---

## Extract Usernames

```bash
awk -F":" '{print $1}' /etc/passwd
```

- `-F:` = Use `:` as separator

---

## Print Specific Columns

```bash
awk '{print $1, $2, $3}' auth.log
```

---

## Count Lines

```bash
awk 'END {print NR}' file.txt
```

- `NR` = Number of Records (lines)

---

## Extract Failed Login Username

```bash
grep "Failed password" /var/log/auth.log | awk '{print $(NF-3)}'
```

- `NF` = Number of fields

---

# FIND Command Cheat Sheet

## Find a File

```bash
find / -name "TempData.txt" 2>/dev/null
```

---

## Find Log Files

```bash
find /var/log -name "*.log" 2>/dev/null
```

---

## Find Exact File

```bash
find /home -name notes.txt
```

---

## Case-Insensitive Search

```bash
find /home -iname notes.txt
```

---

## Find Files Only

```bash
find /var/log -type f
```

---

## Find Directories Only

```bash
find /etc -type d
```

---

# Find by Size

## Bigger Than 100MB

```bash
find / -size +100M
```

---

## Smaller Than 10KB

```bash
find / -size -10k
```

### Useful Units

- `k` = KB
- `M` = MB
- `G` = GB

---

# Find by Time

## Modified in Last 1 Day

```bash
find /home -mtime -1
```

---

## Modified More Than 30 Days Ago

```bash
find /var/log -mtime +30
```

---

# Find by Permissions

```bash
find / -perm 777
```

## SOC Note

World-writable files can be risky.

---

# GREP Command Cheat Sheet

## Basic Syntax

```bash
grep "pattern" file
```

---

## Search Text

```bash
grep "Failed password" /var/log/auth.log
```

---

## Ignore Case Sensitivity

```bash
grep -i "error" logfile.txt
```

---

## Show Line Numbers

```bash
grep -n "root" /etc/passwd
```

---

## Recursive Search

```bash
grep -r "password" /etc
```

---

## Count Matches

```bash
grep -c "Failed password" /var/log/auth.log
```

---

# GREP Regex Example

## Match IP Addresses

```bash
grep -E "[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+" access.log
```

---

# SORT Command Options

| Option | Purpose |
|---|---|
| `-r` | Reverse sorting |
| `-n` | Numeric sorting |
| `-k` | Sort by specific column |
| `-u` | Remove duplicates |
| `-t` | Specify delimiter |

---

# CHOWN Command

## Change Ownership

```bash
sudo chown arijit report.txt
```

---

# TAIL Command Cheat Sheet

| Option | Purpose |
|---|---|
| `-n [number]` | Show last number of lines |
| `-f` | Follow file updates live |
| `-c [number]` | Show last number of bytes |
| `--pid=[pid]` | Stop after process ends |
| `--retry` | Retry opening inaccessible file |

---

# Kill Command

Learn more:

- https://www.w3schools.com/bash/bash_kill.php

---

# Linux File Permissions

```bash
-rw-rw-r--
```

## Meaning

| Symbol | Meaning |
|---|---|
| `-` | Regular file |
| `d` | Directory |

## Permission Groups

- Owner
- Group
- Others

---

# Interview Questions

## What is the Difference Between Linux and Unix?

| Feature | Unix | Linux |
|---|---|---|
| Licensing | Proprietary, paid license | Open-source, GNU GPL |
| Source Code | Closed-source | Open-source |
| Development | Commercial vendors | Community-driven |
| Hardware | Enterprise-specific hardware | Highly portable |
| Common Variants | AIX, HP-UX, Solaris | Ubuntu, CentOS, Fedora, Debian |

---

# What Happens When You Type a Command in the Terminal?

When you type a command and press Enter:

1. The terminal sends the command to the shell.
2. The shell parses the command.
3. Variables and paths are resolved.
4. The shell locates the executable.
5. A child process is created.
6. The command runs.
7. Output or errors are displayed on the screen.


