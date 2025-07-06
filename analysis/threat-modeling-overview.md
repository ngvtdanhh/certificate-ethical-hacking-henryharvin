# 🔍 Threat Modeling in Ethical Hacking

Threat modeling is a structured process to **identify**, **enumerate**, and **prioritize** potential threats to a system, network, or application — before or during a penetration test.

---

## 🎯 1. Objectives of Threat Modeling

- Understand the system's architecture and data flow
- Identify potential attacker goals and entry points
- Analyze security controls and their effectiveness
- Recommend mitigations early in the testing process

---

## 🧠 2. Common Threat Modeling Frameworks

| Model | Focus | Use Case |
|-------|-------|----------|
| **STRIDE** | Spoofing, Tampering, Repudiation, Info Disclosure, DoS, Elevation of Privilege | System-level analysis |
| **DREAD**  | Damage Potential, Reproducibility, Exploitability, Affected Users, Discoverability | Risk scoring |
| **PASTA**  | Process for Attack Simulation and Threat Analysis | Enterprise systems |
| **LINDDUN**| Privacy threats | Privacy-specific testing |

---

## 📌 3. STRIDE Example (Web Login Page)

| Threat        | Description                                 | Example                                  |
|---------------|---------------------------------------------|------------------------------------------|
| **Spoofing**  | Fake user pretending to be admin            | Login bypass with weak password          |
| **Tampering** | Alter data in transit or storage            | Modify JWT tokens or POST body           |
| **Repudiation**| Deny performing an action                  | No logging for failed logins             |
| **Info Disclosure** | Leak sensitive data                  | Verbose error message, debug info shown  |
| **DoS**       | Crash service or exhaust resources          | Login flood, resource starvation         |
| **EoP**       | Gain higher privileges than assigned        | IDOR to access another user's profile    |

---

## 🛠️ 4. Tools for Threat Modeling

- **Microsoft Threat Modeling Tool**
- **OWASP Threat Dragon**
- **Draw.io / Diagrams.net**
- **MITRE ATT&CK Navigator** (mapping TTPs)

---

## 🚨 5. Practical Use in Penetration Testing

- Use threat modeling to **scope** your test plan
- Helps focus testing on high-value targets
- Reveals flaws in design, not just implementation
- Essential for **pre-engagement** and **architecture reviews**

---

## 📘 6. Sample Use Case

For a **cloud-based file-sharing app**:

- STRIDE → reveals unencrypted S3 buckets, lack of MFA
- DREAD → scoring shows file injection is critical
- Report includes both **vulnerability findings** and **design flaws**

---

## 💡 7. Final Thoughts

Threat modeling bridges the gap between developers, architects, and pentesters. It’s not just a paperwork step – it guides meaningful, impactful testing.

---

## 📚 References

- OWASP Threat Modeling Cheat Sheet – https://cheatsheetseries.owasp.org
- STRIDE Threat Model – Microsoft Docs
- Threat Modeling Manifesto – https://www.threatmodelingmanifesto.org/

