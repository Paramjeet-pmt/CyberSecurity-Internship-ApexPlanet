# Linux Fundamentals — Task 1

Part of **Foundation & Environment Setup** (Days 1–12), ApexPlanet Cybersecurity & Ethical Hacking Internship.

All commands below were run on Kali Linux inside the VMware lab environment set up for this internship.

---

## 1. File System Navigation

The Linux file system is navigated using `pwd`, `ls`, and `cd` commands.

| Command | Purpose |
|---|---|
| `pwd` | Prints the current working directory |
| `ls` | Lists files and directories |
| `ls -la` | Lists all files (including hidden) with permissions, owner, size, and date |
| `cd <dir>` | Changes to the specified directory |
| `cd ..` | Moves up one directory level |
| `cd ~` | Returns to the home directory |

### Example
```bash
pwd
# /home/kali

ls -la
# drwxr-xr-x  5 kali kali 4096 Jul 13 10:02 .
# drwxr-xr-x  3 root root 4096 Jul 11 09:00 ..
# -rw-r--r--  1 kali kali  220 Jul 11 09:00 .bash_logout

cd Desktop
pwd
# /home/kali/Desktop
```

📸 Screenshot: `screenshots/linux-navigation.png`

---

## 2. File & Directory Permissions

Linux permissions use `rwx` flags for three groups: **owner**, **group**, and **others**.

| Command | Purpose |
|---|---|
| `chmod` | Changes file or directory permissions |
| `chown` | Changes the owner and group of a file or directory |

### Permission notation
- `r` = read
- `w` = write
- `x` = execute

### Permission values
- `4` = read
- `2` = write
- `1` = execute

Example: `chmod 755 file` sets:
- owner: `rwx`
- group: `r-x`
- others: `r-x`

### Example
```bash
ls -l script.sh
# -rw-r--r-- 1 kali kali 0 Jul 13 10:05 script.sh

chmod 755 script.sh
ls -l script.sh
# -rwxr-xr-x 1 kali kali 0 Jul 13 10:05 script.sh

chown kali:kali script.sh
```

📸 Screenshot: `screenshots/linux-permissions.png`

**Security note:** Misconfigured permissions, such as world-writable files or unnecessary execute bits, are common privilege escalation vectors during penetration testing.

---

## 3. Package Management

Use `apt` and `dpkg` to manage software packages on Kali Linux.

| Command | Purpose |
|---|---|
| `apt update` | Refreshes package index metadata |
| `apt upgrade` | Upgrades installed packages |
| `apt install <package>` | Installs a package |
| `apt remove <package>` | Removes a package |
| `dpkg -l` | Lists installed packages |
| `dpkg -i <file.deb>` | Installs a local `.deb` package |

### Example
```bash
sudo apt update
sudo apt install net-tools
dpkg -l | grep net-tools
```

📸 Screenshot: `screenshots/linux-package-management.png`

---

## 4. Networking Commands

Basic networking commands are used to verify connectivity and inspect network interfaces.

| Command | Purpose |
|---|---|
| `ifconfig` | Displays network interface configuration (IP address, MAC, netmask) |
| `ping <host>` | Tests network connectivity to a target host |
| `netstat -tulnp` | Shows active listening ports and network connections |
| `traceroute <host>` | Traces the path packets take to a destination |

### Example
```bash
ifconfig eth0
# eth0: inet 192.168.56.101  netmask 255.255.255.0

ping -c 4 192.168.56.102
# 4 packets transmitted, 4 received, 0% packet loss

netstat -tulnp
# Proto  Local Address       State    PID/Program
# tcp    0.0.0.0:22          LISTEN   612/sshd

traceroute 192.168.56.102
```

📸 Screenshot: `screenshots/linux-networking-commands.png`

**Lab relevance:** The `ping` test confirms connectivity between the Kali Linux attacker machine and Metasploitable2 over the host-only network.

---

## Key Takeaways

- File system navigation and permission management are foundational skills for working safely in Linux.
- Package management (`apt` and `dpkg`) is essential for installing the security tools used during the internship.
- Networking commands are the first step in diagnostics and reconnaissance during penetration testing.
