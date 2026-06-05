# 📅 Day 15 – MITRE ATT&CK Basics

Today I explored the **MITRE ATT&CK Framework** and practiced transferring files between Windows and Kali.

---

## 📝 What I Learned

### 🔹 MITRE ATT&CK Framework
- Three matrices:
  - **Enterprise**
  - **Mobile**
  - **ICS**
- **Enterprise Matrix** has two components:
  - **Tactics** → Attacker objectives (gaining access, persistence, command & control).
 <img width="902" height="423" alt="{B31D9C79-1DDE-44C0-8D1A-E7BDB65B69AB}" src="https://github.com/user-attachments/assets/9e9ac287-dd6d-48fe-a6e1-809248a8e5fb" />

  - **Techniques** → Specific methods attackers use to achieve those objectives.
 <img width="899" height="459" alt="{BC52F98B-97D8-453C-9465-FA93411254D9}" src="https://github.com/user-attachments/assets/44f5206c-2bb7-40c4-aba4-6984bb063f3c" />

### 🔹 File Transfer (Windows → Kali)
Steps I practiced:
1. Configure both VM network adapters as **Bridge Adapter**.
2. Start **SSH service** in Kali and check IP.
 ```bash
   sudo service ssh start
   ```
3. On Windows 10 VM, use `scp` in CMD:
   ```bash
   scp filename.txt username@ip:/location_where_to_save_the_file
   ```
4. succesfully transferred file.

### 🔹 What is the use of scp command?
The scp (Secure Copy) command is a command-line utility used to securely transfer files and directories between two locations on a network. It uses SSH (Secure Shell) for data transfer, providing the same level of encryption and authentication as an SSH connection
