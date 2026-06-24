# Day 19 – Python for SOC Analysts

Today I focused on practical Python skills used in SOC operations. I worked with log files, searched for security events, and extracted useful data from logs.

## What I Learned

* Reading and processing log files
* Using Regex to extract IP addresses
* Validating IPs with `ipaddress`
* Removing duplicates using sets
* Counting failed login attempts
* Detecting malware-related log entries
* Identifying IOC matches

## Mini Project: SOC Log Analyzer

Built a simple SOC Log Analyzer that can:

* Parse log files
* Extract IP addresses
* Detect suspicious activity and IOCs


```python
import re 
import ipaddress
valid_ips=set()
#IOC list
ioc_list = {
    "8.8.8.8",
    "185.220.101.1",
}
try:
	with open("logfile.txt","r") as f:
		for line in f:
			matches=re.findall(r"\d+\.\d+\.\d+.\d+", line)
			for ip in matches:
				try:
					ipaddress.IPv4Address(ip)
					valid_ips.add(ip)
					
					# 2. INSTANT ALERT: Check against IOC list immediately
					if ip in ioc_list:
						print(f"🚨 ALERT! Critical IOC detected: {ip} found in line: \n{line.strip()}\n")	
				except ValueError:
					#print(f"[{ip}] not Valid : ",line)
					continue
		print("ALL Valid IPs are : ",valid_ips)
		
except FileNotFoundError:
	print("Find not found in the system")
```
## Day 21 Goal – Regex Deep Dive

### Topics

* Regex fundamentals and syntax
* Extracting IPs, domains, URLs, hashes, and emails
* Parsing Windows, Linux, and firewall logs
* Threat hunting with Regex
* SIEM use cases
* SOC-focused Regex challenges and mini projects

### Target

By the end of Day 21, I want to confidently use Regex for log analysis, IOC extraction, and threat detection tasks commonly performed by SOC analysts.
