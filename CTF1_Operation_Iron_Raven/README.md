# 🦅 Operation Iron Raven

## CIP-A105 — Black-Box Penetration Testing

> **CTF/Lab:** `CIP-A105_CTF1_Iron-Raven`  
> **Assessment Type:** Black-Box Penetration Testing  
> **Target:** `192.168.56.102`  
> **Application:** Raven Security  
> **Environment:** Isolated VirtualBox Laboratory  
> **Student:** Modu Kunjo  
> **Status:** Assessment Completed  
> **Classification:** Training / Academic Use Only

---

## 📌 Overview

**Operation Iron Raven** is a black-box penetration-testing assessment conducted as part of the **CIP-A105** practical laboratory.

The objective was to assess the target from an external attacker's perspective, beginning with limited knowledge and progressively building an understanding of the target through:

- Network reconnaissance
- Port and service enumeration
- Web application enumeration
- Content discovery
- Technology identification
- WordPress enumeration
- Username discovery
- Authentication testing
- Vulnerability validation
- Evidence collection
- Risk assessment
- Remediation planning

The assessment was performed against an isolated laboratory target and was not conducted against production infrastructure.

---

# 🎯 Objectives

The primary objectives of Operation Iron Raven were to:

1. Identify the target system.
2. Enumerate exposed network services.
3. Identify technologies and service versions.
4. Map the web application's attack surface.
5. Discover hidden files, directories, and endpoints.
6. Identify authentication interfaces and potential attack paths.
7. Validate security weaknesses where possible.
8. Attempt controlled authentication testing.
9. Document confirmed findings and unsuccessful hypotheses.
10. Produce a professional penetration-testing report.

---

# 🖥️ Target Information

| Item | Details |
|---|---|
| Target IP | `192.168.56.102` |
| Target Name | Raven Security |
| Network | VirtualBox Host-Only |
| Assessment Type | Black-Box |
| Primary Web Service | HTTP |
| SSH | TCP/22 |
| HTTP | TCP/80 |
| Web Server | Apache 2.4.10 |
| SSH Service | OpenSSH 6.7p1 |
| Operating System Indicator | Debian |
| Application | WordPress / Raven Security |

---

# 🔎 Attack Surface

Initial service enumeration identified the following exposed services:

```text
22/tcp   SSH
80/tcp   HTTP
```

Service identification revealed:

```text
OpenSSH 6.7p1 Debian 5+deb8u4
Apache/2.4.10 (Debian)
```

The HTTP service became the primary focus because it exposed a larger application attack surface.

---

# 🌐 Web Enumeration

Content discovery identified multiple pages, files, and directories.

### Discovered Resources

```text
/about.html
/service.html
/team.html
/contact.php
/blog-single.html
/wordpress/
/wp-admin/
/wp-login.php
/wp-signup.php
```

Additional enumeration identified:

- WordPress-related resources
- Application usernames
- `.htpasswd`-related resources
- An exposed Google Maps API key
- Additional web content and endpoints

Some sensitive-looking resources returned `403 Forbidden`, demonstrating that the server was denying direct access.

---

# 🔐 Authentication Testing

After identifying authentication surfaces, controlled password testing was performed against a discovered username.

Approximately:

```text
3,559 password candidates
```

were tested.

### Result

No successful credential compromise is recorded in the available evidence.

Therefore, this assessment does **not** claim successful SSH or WordPress authentication.

This distinction is intentional: attempted exploitation is documented separately from confirmed compromise.

---

# 🛡️ Key Security Observations

The assessment identified several areas requiring security attention:

| ID | Observation | Severity* |
|---|---|---|
| F-01 | Legacy Apache HTTP Server version | Medium |
| F-02 | Legacy OpenSSH service exposed | Medium |
| F-03 | WordPress authentication/admin interfaces exposed | Medium |
| F-04 | Google Maps API key exposed in application | Medium |

> **Note:** Severity ratings should be validated against the assessment methodology/CVSS requirements where applicable. Software-version age alone does not prove exploitability of a specific vulnerability.

---

# ⚠️ Confirmed vs. Unconfirmed

A major principle followed during this assessment was separating **observations** from **confirmed exploitation**.

### Confirmed

- Target `192.168.56.102` identified.
- TCP/22 exposed.
- TCP/80 exposed.
- Apache 2.4.10 identified.
- OpenSSH 6.7p1 identified.
- Raven Security application identified.
- WordPress resources identified.
- WordPress authentication endpoints identified.
- Usernames discovered.
- Additional web content discovered.
- Google Maps API key observed.
- Controlled password testing performed.

### Not Confirmed

The following are **not claimed** without supporting evidence:

- Successful SSH login
- Successful WordPress login
- Valid password discovery
- Remote shell
- Reverse shell
- Command execution
- Root access
- Privilege escalation
- Credential dumping
- Persistence
- Lateral movement
- Full system compromise

---

# 🧪 Methodology

The assessment followed a progressive black-box methodology:

```text
Reconnaissance
      ↓
Target Identification
      ↓
Port Scanning
      ↓
Service Enumeration
      ↓
Web Enumeration
      ↓
Content Discovery
      ↓
Technology Identification
      ↓
WordPress Enumeration
      ↓
Username Discovery
      ↓
Authentication Testing
      ↓
Validation
      ↓
Evidence Collection
      ↓
Risk Assessment
      ↓
Remediation
```

The methodology prioritized enumeration before exploitation and required evidence before classifying an issue as confirmed.

---

# 📂 Repository Structure

```text
CIP-A105_CTF1_Iron-Raven/
│
├── README.md
│
├── REPORT/
│   ├── Executive_Report.md
│   └── Technical_Report.md
│
├── EVIDENCE/
│   ├── screenshots/
│   ├── scans/
│
├── LOGS/
│   └── operator-activity-log.md
│
└── RISK/
    └── risk-register.md
```

### Directory Description

**`README.md`**  
Provides a high-level overview of the operation.

**`REPORT/`**  
Contains the detailed executive and technical assessment reports.

**`EVIDENCE/`**  
Contains screenshots, scan results, command outputs, and other supporting evidence.

**`LOGS/`**  
Contains the chronological operator activity log.

**`RISK/`**  
Contains the risk register and documented remediation actions.

---

# 📑 Documentation

The complete assessment documentation contains:

### Executive Report

Provides a non-technical summary covering:

- Overall security risk
- Business impact
- Attack summary
- Priority actions

### Technical Report

Documents:

- Scope
- Rules of engagement
- Laboratory architecture
- Methodology
- Attack surface
- Findings
- Initial-access investigation
- Authentication testing
- Post-exploitation assessment
- Privilege-escalation assessment
- Remediation
- Evidence
- Lessons learned

### Operator Activity Log

Chronological record of:

- Actions
- Commands
- Observations
- Decisions
- Outcomes
- Testing progression

### Evidence Appendix

Contains supporting material such as:

- Screenshots
- Scan output
- Enumeration results
- HTTP responses
- Authentication-testing evidence
- Relevant artifacts

### Risk Register

Maps findings to:

- Asset
- Likelihood
- Impact
- Severity
- Evidence
- Remediation

---

# 🧠 Lessons Learned

Operation Iron Raven reinforced several important penetration-testing principles.

### 1. Enumeration Comes First

Initial service discovery provided limited information. Continued web enumeration exposed a significantly larger attack surface.

### 2. Discovery Is Not Exploitation

Finding an endpoint, username, software version, or API key does not automatically prove that it is exploitable.

Each potential weakness must be validated.

### 3. Evidence Matters

A professional penetration test requires evidence supporting each important claim.

Commands, screenshots, timestamps, and HTTP responses should be preserved throughout the assessment.

### 4. Failed Attacks Are Valuable

The controlled authentication testing did not produce confirmed credentials. This is still a useful result because it documents an investigated attack path and prevents unsupported claims of compromise.

### 5. Attack Paths Must Be Evidence-Driven

The assessment demonstrated the importance of moving from:

```text
Discovery → Hypothesis → Validation → Evidence → Finding
```

rather than:

```text
Discovery → Assumption → Finding
```

---

# 🛠️ Recommended Remediation Priorities

Based on the assessment observations, recommended actions include:

### Immediate

- Protect administrative interfaces.
- Implement MFA where possible.
- Review exposed API keys.
- Remove unnecessary public resources.
- Monitor authentication attempts.

### Short Term

- Upgrade Apache.
- Upgrade OpenSSH.
- Update WordPress.
- Review WordPress plugins and themes.
- Restrict administrative access.
- Implement authentication rate limiting.

### Strategic

- Establish continuous patch management.
- Implement centralized security logging.
- Conduct periodic vulnerability assessments.
- Perform regular penetration testing.
- Establish secure configuration baselines.
- Maintain an incident-response process.

---

# 📊 Assessment Outcome

| Assessment Area | Status |
|---|---|
| Target identification | ✅ Completed |
| Port enumeration | ✅ Completed |
| Service enumeration | ✅ Completed |
| Web enumeration | ✅ Completed |
| Content discovery | ✅ Completed |
| WordPress enumeration | ✅ Completed |
| Username discovery | ✅ Completed |
| Authentication testing | ✅ Completed |
| Confirmed credential compromise | ❌ Not confirmed |
| Confirmed initial access | ❌ Not confirmed |
| Post-exploitation | ❌ Not confirmed |
| Privilege escalation | ❌ Not confirmed |
| Evidence documentation | ✅ Completed |
| Risk assessment | ✅ Completed |
| Remediation planning | ✅ Completed |

---

# ⚖️ Disclaimer

This project was conducted strictly within an authorized educational laboratory environment.

The techniques, commands, and procedures documented in this repository are intended for cybersecurity education, authorized security testing, and controlled laboratory environments.

No unauthorized production systems were targeted as part of this assessment.

---

# 👤 Author

**Modu Kunjo**

Cybersecurity Practitioner | IT Support Specialist | Ethical Hacking Learner

**Focus Areas:**

- Cybersecurity
- Ethical Hacking
- Network Security
- Web Application Security
- Penetration Testing
- Security Awareness

---

## 🦅 Operation Iron Raven

> **Enumerate. Validate. Document. Remediate.**