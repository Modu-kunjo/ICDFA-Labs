# Operation Iron Raven — Risk Register

## CIP-A105 Black-Box Penetration Testing

**CTF/Lab:** `CIP-A105_CTF1_Iron-Raven`  
**Target:** `192.168.56.102`  
**Student:** Modu Kunjo  
**Assessment Date:** September 2026  
**Classification:** Training / Academic Use Only

---

# 1. Risk Register Overview

This register records the security findings and observations identified during Operation Iron Raven.

The register distinguishes between:

- Confirmed security observations.
- Potential risks requiring further validation.
- Evidence supporting each finding.
- Recommended remediation.

Severity ratings should be validated against the course's required methodology or CVSS scoring requirements where applicable.

---

# 2. Risk Summary

| ID | Finding | Asset | Likelihood | Impact | Severity | Status |
|---|---|---|---|---|---|---|
| F-01 | Legacy Apache HTTP Server | `192.168.56.102:80` | Medium | Medium–High | Medium* | Open |
| F-02 | Legacy OpenSSH Service | `192.168.56.102:22` | Medium | High | Medium* | Open |
| F-03 | Exposed WordPress Authentication/Admin Interfaces | `192.168.56.102` | Medium | Medium–High | Medium | Open |
| F-04 | Google Maps API Key Exposure | Raven Security | Medium | Medium | Medium* | Open |

> `*` Severity should be finalized after mapping the exact software versions, configurations, and applicable vulnerabilities to the required scoring methodology.

---

# 3. Detailed Risk Register

## F-01 — Legacy Apache HTTP Server

### Asset

```text
192.168.56.102:80
```

### Finding

Legacy Apache HTTP Server version identified.

### Evidence

```text
Apache/2.4.10 (Debian)
```

### Description

The web server disclosed an Apache HTTP Server version that is significantly old compared with currently supported releases.

Running outdated software can expose an environment to known vulnerabilities depending on the operating-system package state, enabled modules, configuration, and applicable security patches.

### Likelihood

**Medium**

The service is publicly accessible within the assessment environment and the version is identifiable.

### Impact

**Medium–High**

A vulnerable web-server component could potentially provide unauthorized access or facilitate further attacks.

### Severity

**Medium – pending exact vulnerability validation**

### Evidence Reference

```text
EV-03
```

### Recommendation

- Upgrade Apache to a supported version.
- Upgrade the underlying Debian system where required.
- Apply security patches.
- Disable unnecessary modules.
- Reduce version disclosure.
- Establish regular patch management.

### Status

**Open**

---

# F-02 — Legacy OpenSSH Service

### Asset

```text
192.168.56.102:22
```

### Finding

Legacy OpenSSH service exposed to the network.

### Evidence

```text
OpenSSH 6.7p1 Debian 5+deb8u4
```

### Description

SSH provides remote administration functionality and therefore represents a high-value authentication surface.

The identified version is old and should be reviewed for applicable vulnerabilities and security updates.

### Likelihood

**Medium**

The service is exposed and provides an authentication interface.

### Impact

**High**

Successful compromise of a remote administration service could provide direct system access.

### Severity

**Medium – pending configuration and vulnerability validation**

### Evidence Reference

```text
EV-02
```

### Recommendation

- Upgrade OpenSSH.
- Upgrade the underlying operating system.
- Disable direct root login.
- Prefer SSH-key authentication.
- Disable unnecessary authentication mechanisms.
- Restrict SSH to trusted management networks.
- Implement rate limiting.
- Monitor authentication failures.

### Status

**Open**

---

# F-03 — Exposed WordPress Authentication and Administrative Interfaces

### Asset

```text
192.168.56.102
```

### Finding

Publicly discoverable WordPress authentication and administration endpoints.

### Evidence

```text
/wordpress/
/wp-admin/
/wp-login.php
/wp-signup.php
```

### Description

WordPress authentication and administrative resources were identified during content discovery.

The availability of these endpoints allows an attacker to identify authentication targets and perform further enumeration or credential attacks.

### Likelihood

**Medium**

The endpoints were directly discoverable through web enumeration.

### Impact

**Medium–High**

If weak credentials or vulnerable WordPress components are present, unauthorized access could potentially be obtained.

### Severity

**Medium**

### Evidence References

```text
EV-06
EV-07
EV-08
EV-09
```

### Recommendation

- Implement MFA.
- Restrict administrative access.
- Disable registration if not required.
- Apply rate limiting.
- Monitor failed login attempts.
- Update WordPress core.
- Update plugins and themes.
- Remove unused plugins and themes.
- Review WordPress user privileges.
- Disable unnecessary endpoints where appropriate.

### Status

**Open**

---

# F-04 — Google Maps API Key Exposure

### Asset

```text
Raven Security Web Application
```

### Finding

Google Maps API key exposed within the application.

### Description

An API key was observed during application inspection.

API keys that are intended for browser-side applications are not necessarily secret, but they should be restricted to prevent unauthorized use.

### Likelihood

**Medium**

The key was accessible through the publicly available application.

### Impact

**Medium**

If insufficiently restricted, an attacker may potentially abuse the key for unauthorized API requests, consume quota, or generate unexpected costs.

### Severity

**Medium – dependent on key restrictions and permissions**

### Evidence Reference

```text
EV-12
```

### Recommendation

- Restrict the key by HTTP referrer/domain.
- Restrict the key to required APIs only.
- Configure quota limits.
- Monitor API usage.
- Rotate the key where appropriate.
- Remove unnecessary keys.

### Status

**Open**

---

# 4. Security Observations Requiring Further Validation

The following observations were identified but should not automatically be treated as confirmed exploitable vulnerabilities.

## 4.1 `.htpasswd` Resources

`.htpasswd`-related resources were identified during content discovery.

The server returned:

```text
HTTP 403 Forbidden
```

This indicates that access was denied.

### Assessment

The presence of the resource is worth reviewing, but successful disclosure was **not confirmed**.

### Recommendation

Ensure sensitive authentication files are stored outside the web root and are inaccessible through HTTP.

---

## 4.2 Username Enumeration

Usernames were identified during the assessment.

### Assessment

Username disclosure can make authentication attacks easier, but username discovery alone does not demonstrate account compromise.

### Recommendation

Review WordPress user-enumeration behavior and minimize unnecessary disclosure of account information.

---

## 4.3 Password Testing

Approximately:

```text
3,559 password candidates
```

were tested against a discovered username.

### Result

No successful credential compromise was confirmed.

### Recommendation

Implement:

- Strong password requirements.
- MFA.
- Rate limiting.
- Authentication monitoring.
- Appropriate lockout or adaptive controls.

---

# 5. Risk Treatment Priority

## Immediate

### F-03 — WordPress Authentication/Admin Exposure

Protect administrative interfaces and strengthen authentication controls.

### F-04 — API Key Exposure

Review API restrictions and rotate the key if necessary.

---

## Short Term

### F-01 — Apache

Upgrade the web server and operating system.

### F-02 — OpenSSH

Upgrade and harden SSH.

---

## Strategic

Implement:

- Continuous patch management.
- Vulnerability management.
- Centralized logging.
- Security monitoring.
- Periodic penetration testing.
- Secure configuration management.
- Regular access reviews.

---

# 6. Risk Register Status

| Finding | Current Status | Recommended Owner |
|---|---|---|
| F-01 Apache | Open | System/Web Administrator |
| F-02 OpenSSH | Open | System Administrator |
| F-03 WordPress | Open | Web/Application Administrator |
| F-04 API Key | Open | Application/Web Administrator |

---

# 7. Final Risk Statement

The Iron Raven target presented a broad attack surface through exposed network services and web application functionality.

The primary risk-reduction strategy should be to:

1. Reduce unnecessary exposure.
2. Upgrade legacy software.
3. Harden authentication.
4. Protect administrative interfaces.
5. Restrict API credentials.
6. Monitor authentication activity.
7. Maintain continuous patch and vulnerability management.

No successful credential compromise, initial-access shell, or privilege escalation is recorded as confirmed in the available assessment evidence.

---

**End of Risk Register**