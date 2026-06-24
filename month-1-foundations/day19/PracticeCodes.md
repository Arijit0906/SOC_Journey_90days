
# Find & Count all the Failed login's
```
with open('logfile.txt', 'r') as f:
	#print(f.read())
	lines=f.readlines() #readlines() method reads all the lines from a  file and return them as a list of strings
	failed = 0

	for line in lines:
		if "Failed" in line:
			print("[Alert] ", line)			
			failed+=1			
	print("Total Failed Logins: ",failed)

Output:
[Alert]  2026-06-23 09:02:30 ERROR Failed login for admin from 203.0.113.5

[Alert]  2026-06-23 09:02:45 ERROR Failed login for admin from 203.0.113.5

[Alert]  2026-06-23 09:03:02 ERROR Failed login for admin from 203.0.113.5

[Alert]  2026-06-23 09:03:18 ERROR Failed login for admin from 203.0.113.5

[Alert]  2026-06-23 09:03:35 ERROR Failed login for admin from 203.0.113.5

[Alert]  2026-06-23 09:03:50 ERROR Failed login for admin from 203.0.113.5

[Alert]  2026-06-23 09:04:05 ERROR Failed login for admin from 203.0.113.5

[Alert]  2026-06-23 09:13:10 ERROR Failed login for root from 45.33.32.1

[Alert]  2026-06-23 09:13:22 ERROR Failed login for root from 45.33.32.1

[Alert]  2026-06-23 09:13:35 ERROR Failed login for root from 45.33.32.1

[Alert]  2026-06-23 09:19:01 ERROR Failed login for administrator from 203.0.113.5

[Alert]  2026-06-23 09:19:15 ERROR Failed login for administrator from 203.0.113.5

Total Failed Logins:  12

```

# Find All the Malware Alerts
```
with open('logfile.txt', 'r') as f:
	lines=f.readlines()
	for line in lines:
		if "Malware" in line:
			print("[Critical] ",line)

Output :
[Critical]  2026-06-23 09:06:00 ALERT Malware detected on HOST-01

[Critical]  2026-06-23 09:14:10 ALERT Malware detected on HOST-02

[Critical]  2026-06-23 09:20:30 ALERT Malware detected on HOST-03

```

# Finding Logs through Input Keywards
```
keyword = input("Enter keyword: ")

with open("logfile.txt", "r") as file:
    for line in file:
        if keyword.lower() in line.lower():
            print(line.strip())

Output:
Enter keyword: logged in
2026-06-23 09:00:01 INFO User john logged in from 192.168.1.10
2026-06-23 09:01:15 INFO User alice logged in from 10.10.10.15
2026-06-23 09:08:01 INFO User david logged in from 172.16.1.20
2026-06-23 09:12:00 INFO User root logged in from 192.168.1.15
2026-06-23 09:16:45 INFO User mike logged in from 172.16.5.100
2026-06-23 09:21:10 INFO User sarah logged in from 192.168.1.55
2026-06-23 09:21:10 INFO User sarah logged in from 192.1682.1.552

```

# Counting Total Number of Lines 
```
with open("logfile.txt","r") as f:
	logs=f.readlines()
	total_log=0
	for log in logs:
		total_log+=1
	print("Total Log : ", total_log)

Output:
Total Log : 39
```

# Look for Unique Users in the logs
```

unique_users = set()
with open("logfile.txt","r") as f:
	for line in f:
	    # Scenario 1: Look for Successful Logins
		if "User " in line and " logged in" in line:
			parts = line.split("User ")
			username = parts[1].split(" ")[0]
			unique_users.add(username)
		
	    # Scenario 2: Look for Failed Logins
		elif "Failed login for " in line:
			parts = line.split("Failed login for ")
			username = parts[1].split(" ")[0]
			unique_users.add(username)

# Print the results
print(f"Total Unique Users Found: {len(unique_users)}")
print("List of Users:", unique_users)

Output:
Total Unique Users Found: 8
List of Users: {'david', 'sarah', 'john', 'administrator', 'root', 'admin', 'mike', 'alice'}
```
