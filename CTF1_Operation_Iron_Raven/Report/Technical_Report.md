# Operation Iron Raven — Technical Penetration Testing Report

## CIP-A105 Black-Box Penetration Testing

**CTF/Lab:** `CIP-A105_CTF1_Iron-Raven`  
**Operation:** Iron Raven  
**Target:** `192.168.56.102`  
**Application:** Raven Security  
**Student:** Modu Kunjo  
**Assessment Date:** September 2026  
**Classification:** Training / Academic Use Only

---

# 1. Cover Page

## Operation Iron Raven

### Black-Box Penetration Testing Assessment

This report documents the technical activities performed against the authorized Iron Raven laboratory target.

The assessment was conducted using a black-box methodology, beginning with limited knowledge of the target and progressing through reconnaissance, enumeration, attack-surface analysis, authentication testing, evidence collection, and remediation planning.

---

# 2. Executive Summary

Operation Iron Raven assessed the security posture of the target system at `192.168.56.102`.

The initial reconnaissance identified TCP/22 and TCP/80 as accessible services. Service enumeration identified OpenSSH 6.7p1 and Apache 2.4.10 on Debian.

The HTTP service hosted the Raven Security application. Continued enumeration identified WordPress components, administrative and authentication interfaces, application pages, usernames, `.htpasswd`-related resources, and a Google Maps API key.

Controlled authentication testing was subsequently performed using approximately 3,559 password candidates against a discovered username.

No successful authentication or system compromise is confirmed in the available evidence.

The principal findings concern legacy service exposure, publicly accessible WordPress authentication interfaces, and application information exposure.

---

# 3. Scope and Rules of Engagement

## 3.1 Scope

The assessment was restricted to the authorized laboratory target:

```text
192.168.56.102
```

### In-Scope Services

```text
TCP/22 – SSH
TCP/80 – HTTP
```

## 3.2 Testing Objectives

The assessment aimed to:

- Identify exposed services.
- Enumerate service versions.
- Discover the web application attack surface.
- Identify hidden directories and files.
- Identify authentication interfaces.
- Discover usernames where possible.
- Test potential authentication weaknesses.
- Validate security observations.
- Collect evidence.
- Document remediation.

## 3.3 Testing Restrictions

Testing was performed within the provided educational laboratory.

The assessment did not target unrelated production systems.

---

# 4. Laboratory Architecture

The assessment was performed within an isolated VirtualBox laboratory environment.

The attacker/testing machine was a Kali Linux system connected to the laboratory network.

The Iron Raven target was identified at:

```text
192.168.56.102
```

The target exposed web and SSH services to the testing environment.

---

# 5. Methodology

The assessment followed a progressive black-box methodology.

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

The assessment emphasized evidence-driven validation.

A discovered service or resource was not automatically classified as a confirmed vulnerability.

---

# 6. Attack-Surface Analysis

## 6.1 Network Attack Surface

The target exposed:

| Port | Service | Version |
|---|---|---|
| 22/TCP | SSH | OpenSSH 6.7p1 Debian 5+deb8u4 |
| 80/TCP | HTTP | Apache 2.4.10 Debian |

---

## 6.2 Web Attack Surface

The web application was identified as **Raven Security**.

The following resources were discovered:

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

These resources expanded the attack surface beyond the initially visible application pages.

---

# 7. Service Enumeration

## 7.1 SSH

The SSH service was identified on TCP/22.

Observed version:

```text
OpenSSH 6.7p1 Debian 5+deb8u4
```

The service provides remote authentication functionality and therefore represents an important attack surface.

No successful SSH authentication is claimed in this report.

---

## 7.2 HTTP

The HTTP service was identified on TCP/80.

Observed server:

```text
Apache/2.4.10 (Debian)
```

The server exposed the Raven Security application.

---

# 8. Web Application Enumeration

The Raven Security web application was enumerated to identify available functionality and hidden content.

The initial application included pages such as:

```text
about.html
service.html
team.html
contact.php
blog-single.html
```

Further content discovery identified WordPress resources.

---

# 9. WordPress Enumeration

The presence of WordPress significantly expanded the attack surface.

Identified resources included:

```text
/wordpress/
/wp-admin/
/wp-login.php
/wp-signup.php
```

## 9.1 WordPress Login

The following endpoint was identified:

```text
/wp-login.php
```

The endpoint returned HTTP 200 and provided a WordPress authentication interface.

## 9.2 WordPress Administration

The following administrative endpoint was identified:

```text
/wp-admin/
```

The existence of an administrative endpoint provides an identifiable authentication target.

## 9.3 WordPress Registration

The following endpoint was identified:

```text
/wp-signup.php
```

The endpoint redirected toward the `raven.local` hostname.

---

# 10. Content Discovery

Content discovery identified additional files, directories, and application resources.

Notable discoveries included:

```text
about.html
service.html
team.html
contact.php
blog-single.html
wordpress/
wp-admin/
wp-login.php
wp-signup.php
```

Additional enumeration identified `.htpasswd`-related resources.

These resources returned:

```text
HTTP 403 Forbidden
```

The HTTP 403 response indicates that access was denied.

It does not demonstrate successful access to the protected resource.

---

# 11. Information Disclosure

Several pieces of information were obtainable through enumeration.

These included:

- Server software information.
- SSH software information.
- WordPress presence.
- WordPress authentication endpoints.
- Usernames.
- Application structure.
- Google Maps API key.

Information disclosure can assist attackers by reducing the amount of reconnaissance required before attempting further attacks.

---

# 12. Authentication Testing

Authentication testing was conducted after identifying usernames and authentication interfaces.

Approximately:

```text
3,559 password candidates
```

were tested against the selected username.

The objective was to determine whether weak credentials could provide an initial foothold.

## Result

No successful authentication is confirmed in the available evidence.

Therefore, this assessment does not claim that:

- SSH access was obtained.
- WordPress access was obtained.
- A valid password was discovered.

---

# 13. Confirmed Findings

## F-01 — Legacy Apache HTTP Server

### Asset

```text
192.168.56.102:80
```

### Observation

Apache 2.4.10 on Debian was identified.

### Risk

Legacy server software may contain publicly documented vulnerabilities or unsupported components depending on the operating-system package state and enabled modules.

### Impact

Potential impact could include unauthorized access or application compromise if an applicable vulnerability exists.

### Evidence

Service enumeration identified:

```text
Apache/2.4.10 (Debian)
```

### Recommendation

Upgrade Apache and the underlying operating system to supported versions and establish regular patch management.

---

# F-02 — Legacy OpenSSH Service

### Asset

```text
192.168.56.102:22
```

### Observation

OpenSSH 6.7p1 Debian 5+deb8u4 was exposed.

### Risk

An exposed and outdated remote administration service increases the potential attack surface.

### Impact

Depending on configuration and vulnerabilities, attackers may attempt credential attacks or exploit weaknesses in the service.

### Evidence

Service enumeration identified:

```text
OpenSSH 6.7p1 Debian 5+deb8u4
```

### Recommendation

Upgrade OpenSSH, disable unnecessary authentication methods, restrict SSH access, and implement strong authentication.

---

# F-03 — Exposed WordPress Authentication and Administrative Interfaces

### Asset

```text
192.168.56.102
```

### Observation

The following WordPress endpoints were discoverable:

```text
/wp-login.php
/wp-admin/
/wp-signup.php
```

### Risk

Publicly discoverable authentication endpoints provide attackers with identifiable targets for credential attacks and application enumeration.

### Impact

If weak credentials or vulnerable WordPress components exist, attackers may potentially obtain unauthorized access.

### Evidence

WordPress enumeration identified the above endpoints.

### Recommendation

Implement:

- Multi-factor authentication.
- Authentication rate limiting.
- Strong passwords.
- Administrative access restrictions.
- WordPress security updates.
- Plugin/theme review.
- Monitoring of failed authentication attempts.

---

# F-04 — Google Maps API Key Exposure

### Asset

Raven Security web application

### Observation

A Google Maps API key was observed within the application.

### Risk

Client-visible API keys must be appropriately restricted. An unrestricted key may potentially be abused.

### Impact

Potential consequences include:

- Unauthorized API usage.
- Quota consumption.
- Unexpected billing.
- Abuse of associated Google services.

### Evidence

The API key was observed during web application inspection.

### Recommendation

- Restrict the key by domain/referrer.
- Restrict enabled APIs.
- Apply quota limits.
- Monitor usage.
- Rotate the key if necessary.

---

# 14. Initial-Access Narrative

The initial attack surface consisted primarily of SSH and HTTP.

The web service provided more opportunities for enumeration and therefore became the primary investigation path.

The discovery of WordPress significantly expanded the attack surface.

The following sequence summarizes the investigation:

```text
Target identified
      ↓
22/SSH and 80/HTTP discovered
      ↓
Apache and OpenSSH versions identified
      ↓
Raven Security web application identified
      ↓
Content discovery performed
      ↓
WordPress discovered
      ↓
wp-login.php identified
      ↓
wp-admin identified
      ↓
wp-signup.php identified
      ↓
Usernames discovered
      ↓
Controlled password testing performed
      ↓
No confirmed successful authentication
```

---

# 15. Post-Exploitation

Post-exploitation requires an established foothold.

No successful authenticated shell or equivalent access is confirmed in the available evidence.

Therefore, the following activities are **not claimed**:

- Local enumeration after compromise.
- Credential dumping.
- Sensitive-file extraction.
- Persistence.
- Lateral movement.
- Internal network pivoting.

---

# 16. Privilege Escalation

Privilege escalation was not confirmed.

No evidence is currently available demonstrating:

- Sudo abuse.
- SUID exploitation.
- Kernel exploitation.
- Service misconfiguration exploitation.
- Credential-based privilege escalation.
- Root/administrator access.

The lack of a confirmed initial foothold prevented privilege escalation from being established as a successful attack stage.

---

# 17. Mission Objectives and Proof of Completion

| Objective | Status |
|---|---|
| Identify target | Completed |
| Enumerate ports | Completed |
| Identify services | Completed |
| Identify web technologies | Completed |
| Perform content discovery | Completed |
| Identify WordPress | Completed |
| Identify authentication endpoints | Completed |
| Discover usernames | Completed |
| Perform controlled authentication testing | Completed |
| Confirm credentials | Not confirmed |
| Obtain initial access | Not confirmed |
| Post-exploitation | Not confirmed |
| Privilege escalation | Not confirmed |
| Document findings | Completed |
| Develop remediation | Completed |

---

# 18. Remediation Roadmap

## Immediate

1. Restrict WordPress administrative access.
2. Implement MFA.
3. Review the Google Maps API key.
4. Remove unnecessary exposed resources.
5. Monitor authentication attempts.

## Short Term

1. Upgrade Apache.
2. Upgrade OpenSSH.
3. Update WordPress.
4. Review plugins and themes.
5. Implement rate limiting.
6. Review SSH configuration.
7. Reduce unnecessary service exposure.

## Strategic

1. Implement continuous patch management.
2. Establish vulnerability-management procedures.
3. Implement centralized security monitoring.
4. Perform regular penetration testing.
5. Maintain secure configuration baselines.
6. Establish incident-response procedures.

---

# 19. Evidence Requirements

The final evidence package should contain screenshots or terminal output corresponding to the following:

| Evidence ID | Evidence |
|---|---|
| EV-01 | Target discovery |
| EV-02 | Port/service enumeration |
| EV-03 | Apache version identification |
| EV-04 | Raven Security application |
| EV-05 | Content discovery |
| EV-06 | WordPress discovery |
| EV-07 | `/wp-login.php` |
| EV-08 | `/wp-admin/` |
| EV-09 | `/wp-signup.php` |
| EV-10 | `.htpasswd` 403 response |
| EV-11 | Username discovery |
| EV-12 | API key observation |
| EV-13 | Authentication testing |
| EV-14 | Final validation |

---

# 20. Technical Limitations

The report is intentionally limited to information supported by the available assessment evidence.

The following are not reported as successful results:

- Successful credentials.
- SSH compromise.
- WordPress compromise.
- Remote command execution.
- Reverse shell.
- Root access.
- Privilege escalation.
- Persistence.
- Lateral movement.
- Complete system takeover.

Additional evidence can be added to this report if these stages were successfully completed and documented during the laboratory operation.

---

# 21. Conclusion

Operation Iron Raven demonstrated the methodology required to perform a black-box penetration test against an unknown target.

The assessment successfully progressed from target discovery to service enumeration, web application enumeration, content discovery, WordPress enumeration, username discovery, and authentication testing.

The most significant lesson was the importance of systematic enumeration. The initial two exposed services led to discovery of a substantially larger application attack surface.

The operation also demonstrated the importance of evidence-based reporting. Potential weaknesses must be validated before being classified as confirmed vulnerabilities, and unsuccessful attack attempts should be documented as such rather than represented as successful compromise.

---

**End of Technical Report**