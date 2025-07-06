# 🧭 Strategic Overview – Phases of Ethical Hacking

This document outlines the **five core phases** of an ethical hacking engagement, structured to reflect real-world offensive security methodologies. These steps align with both **penetration testing standards (e.g., PTES)** and **bug bounty workflows**.

---

## 1. 🕵️ Reconnaissance

> Goal: Gather as much information as possible about the target

- **Passive Recon**: WHOIS, Google Dorking, DNS enumeration, Shodan
- **Active Recon**: Nmap scanning, subdomain brute-force, service enumeration

💡 Tools: `nmap`, `amass`, `recon-ng`, `shodan`, `crt.sh`

---

## 2. 🧪 Scanning & Enumeration

> Goal: Map the attack surface and uncover live services or technologies

- Port and service scanning
- Banner grabbing and protocol versioning
- Directory brute-forcing (e.g., Gobuster)

💡 Tools: `nmap`, `nikto`, `gobuster`, `whatweb`, `netcat`

---

## 3. 💣 Gaining Access

> Goal: Exploit vulnerabilities to gain unauthorized access

- Exploiting web vulnerabilities (XSS, SQLi, RCE)
- Exploiting misconfigurations or outdated software
- Credential spraying or brute-forcing

💡 Tools: `sqlmap`, `hydra`, `msfconsole`, `exploit-db`, `searchsploit`

---

## 4. 🎯 Privilege Escalation

> Goal: Move from limited access to higher privileges

- Kernel exploits
- SUID binary abuse
- Misconfigured services (e.g., cronjobs, NFS)

💡 Tools: `linPEAS`, `sudo -l`, `GTFOBins`, `pspy`

---

## 5. 🧹 Covering Tracks & Reporting

> Goal: Minimize footprint, report findings clearly

- Clean up dropped shells/backdoors
- Document each finding with:
  - Vulnerability name
  - CVSS score
  - PoC
  - Mitigation recommendation

---

## 📌 Example Application

If the target is a PHP-based web application:

- Recon → Find exposed admin panel via `/admin`
- Scanning → Detect outdated Apache server
- Access → Upload PHP shell via file upload flaw
- PrivEsc → Find weak cronjob calling user script as root
- Reporting → Deliver CVE-mapped report

---

## 🛡️ Best Practices

- Always define **Rules of Engagement** before testing
- Perform **Non-Destructive Scans** unless explicitly authorized
- Use **secure channels** for report submission
- Respect target scope at all times

---

## 📚 References

- PTES – Penetration Testing Execution Standard: https://www.pentest-standard.org/
- NIST SP 800-115 – Technical Guide to Information Security Testing
- OWASP Testing Guide v4

