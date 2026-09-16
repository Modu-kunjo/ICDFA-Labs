# Operation Iron Raven — Executive Report

## CIP-A105 Black-Box Penetration Testing

**CTF/Lab:** `CIP-A105_CTF1_Iron-Raven`  
**Target:** `192.168.56.102`  
**Application:** Raven Security  
**Student:** Modu Kunjo  
**Assessment Date:** September 2026  
**Classification:** Training / Academic Use Only

---

## 1. Executive Summary

Operation Iron Raven was conducted as a black-box penetration-testing assessment against an authorized laboratory target at `192.168.56.102`.

The assessment simulated an external attacker who initially had limited knowledge of the target. Testing progressed through network reconnaissance, service enumeration, web application enumeration, content discovery, WordPress enumeration, username discovery, and controlled authentication testing.

Two primary network services were identified:

- **TCP/22 – SSH**
- **TCP/80 – HTTP**

The exposed web service identified itself as **Apache 2.4.10 on Debian** and hosted the **Raven Security** application. Further enumeration identified a WordPress installation and several authentication and administrative endpoints, including `/wp-login.php`, `/wp-admin/`, and `/wp-signup.php`.

Additional content discovery identified application pages, usernames, `.htpasswd`-related resources, and a Google Maps API key.

Controlled authentication testing was subsequently performed against a discovered username using approximately **3,559 password candidates**. No successful credential compromise is confirmed in the evidence collected for this report.

The assessment therefore demonstrates a meaningful exposed attack surface, but does **not** claim complete system compromise, successful remote access, or privilege escalation without supporting evidence.

---

## 2. Overall Risk

The assessment identified several security concerns that would require attention in a real-world deployment:

1. Legacy Apache HTTP Server software was exposed.
2. A legacy OpenSSH service was exposed to the network.
3. WordPress authentication and administration interfaces were publicly discoverable.
4. Application information and usernames could be discovered through enumeration.
5. A Google Maps API key was present within the publicly accessible application.
6. Authentication endpoints were available for password-guessing activity.

The risk associated with these observations depends on configuration, patch status, authentication controls, and whether exploitable vulnerabilities exist in the specific versions and components.

Software-version age alone does not prove successful exploitation.

---

## 3. Business Impact

If similar weaknesses existed in a production environment and were successfully exploited, potential consequences could include:

- Unauthorized access to application accounts.
- Website defacement or unauthorized modification.
- Disclosure of application information.
- Abuse of exposed API resources.
- Compromise of administrative accounts.
- Further access to the underlying server.
- Potential lateral movement into other systems.
- Operational and reputational consequences.

No production system or real organizational data was targeted during this laboratory exercise.

---

## 4. Attack Summary

The assessment followed this general attack path:

```text
Target Discovery
      ↓
Port Enumeration
      ↓
Service Identification
      ↓
Web Application Enumeration
      ↓
Content Discovery
      ↓
WordPress Discovery
      ↓
Username Discovery
      ↓
Authentication Testing
      ↓
Evidence Collection
      ↓
Risk Assessment
```

The web application provided the largest identifiable attack surface.

Discovered resources included:

```text
/wordpress/
/wp-admin/
/wp-login.php
/wp-signup.php
/contact.php
/blog-single.html
/about.html
/service.html
/team.html
```

---

## 5. Key Findings

| ID | Finding | Severity |
|---|---|---|
| F-01 | Legacy Apache HTTP Server exposed | Medium* |
| F-02 | Legacy OpenSSH service exposed | Medium* |
| F-03 | WordPress authentication/admin interfaces exposed | Medium |
| F-04 | Google Maps API key exposed | Medium* |

\* Final severity should be validated against the course's required scoring methodology and specific vulnerability/configuration evidence.

---

## 6. Priority Actions

### Immediate

- Restrict access to administrative interfaces.
- Enable multi-factor authentication.
- Review and restrict the exposed Google Maps API key.
- Remove unnecessary publicly accessible files and endpoints.
- Monitor authentication attempts.
- Review discovered usernames and account-enumeration behavior.

### Short Term

- Upgrade Apache and the underlying operating system.
- Upgrade OpenSSH.
- Update WordPress core, themes, and plugins.
- Remove unused WordPress components.
- Implement authentication rate limiting.
- Review web-server configuration.

### Strategic

- Establish formal patch-management procedures.
- Implement centralized security logging and monitoring.
- Conduct regular vulnerability assessments.
- Perform periodic penetration testing.
- Establish secure configuration baselines.
- Maintain an incident-response process.

---

## 7. Assessment Limitations

The available evidence does not confirm:

- Successful SSH authentication.
- Successful WordPress authentication.
- A valid compromised password.
- Remote command execution.
- Reverse shell access.
- Root/administrator access.
- Privilege escalation.
- Persistence.
- Lateral movement.
- Complete system compromise.

These items should therefore not be represented as successful attack results.

---

## 8. Conclusion

Operation Iron Raven successfully demonstrated the reconnaissance and attack-surface analysis stages of a black-box penetration test.

The assessment identified exposed network services, an aging web-server stack, WordPress authentication interfaces, discoverable application information, usernames, and an exposed API key.

The operation also demonstrated the importance of distinguishing between **potential security weaknesses and confirmed exploitation**. Although authentication testing was performed, successful credential compromise was not confirmed in the available evidence.

The principal security priorities are software modernization, reduction of unnecessary attack surface, WordPress hardening, stronger authentication controls, API-key restrictions, patch management, and continuous security monitoring.

---

**End of Executive Report**