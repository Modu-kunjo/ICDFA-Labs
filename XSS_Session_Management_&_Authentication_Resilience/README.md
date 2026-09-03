# Lab 4 — XSS, Session Management and Authentication Resilience Assessment

## Overview

This lab evaluates common web application security weaknesses involving:

- Reflected Cross-Site Scripting (XSS)
- Stored Cross-Site Scripting (XSS)
- DOM-Based XSS
- Session lifecycle and session invalidation
- Cookie security attributes
- Authentication resilience
- Rate limiting and account lockout
- Secure configuration and remediation

Testing was performed only against **authorized, deliberately vulnerable local applications** in an isolated laboratory environment.

## Objectives

The assessment objectives were to:

1. Identify reflected, stored, and DOM-based XSS attack surfaces.
2. Demonstrate XSS behavior using harmless test markers.
3. Examine how user-controlled input reaches browser rendering sinks.
4. Verify whether stored XSS persists across learner-controlled sessions.
5. Compare application behavior under different security configurations.
6. Examine session creation, rotation, and invalidation.
7. Review security-related cookie attributes.
8. Conduct a tightly bounded authentication resilience test.
9. Compare security controls between DVWA and OWASP Mutillidae II.
10. Recommend layered defensive controls.

---

## Scope

### Applications

- DVWA
- OWASP Mutillidae II

### XSS Testing

The following XSS categories were assessed:

- Reflected XSS
- Stored XSS
- DOM-Based XSS

### Session Management

Testing included:

- Pre-authentication session state
- Post-authentication session state
- Session rotation
- Logout invalidation
- Cookie security attributes

### Authentication Resilience

A dedicated learner-owned test account was used.

**Maximum failed attempts per target:** 5

Testing was limited to observing:

- Response behavior
- Timing
- Delays
- Rate limiting
- Lockout behavior
- Authentication feedback

---

## Rules of Engagement

All testing remained within the authorized local laboratory environment.

### Allowed

- Harmless XSS markers
- Learner-controlled accounts
- Learner-controlled browser sessions
- Burp Suite/ZAP request inspection
- HTTP request and response analysis
- Cookie attribute inspection
- Controlled authentication attempts

### Prohibited

The assessment did **not** include:

- Cookie or session-token theft
- Session hijacking
- Credential stuffing
- Password spraying
- Phishing overlays
- Keylogging
- External callbacks
- Malware
- Reverse shells
- Persistence
- Privilege escalation
- Testing real accounts
- Access to unrelated systems or sensitive data

---

## Evidence Register

| ID | Evidence | Purpose | Status |
|---|---|---|---|
| E01 | Reflected XSS baseline | Establish normal input/output behavior | Complete |
| E02 | Reflected XSS proof | Demonstrate unsafe reflection | Complete |
| E03 | DOM XSS source/sink analysis | Identify client-side source and sink | Complete |
| E04 | Stored XSS persistence | Demonstrate persistence across sessions | Complete |
| E05 | XSS security-level retest | Compare behavior under stronger configuration | Pending |
| E06 | Session lifecycle | Examine pre-login, post-login and logout behavior | Pending |
| E07 | Cookie attributes | Review Secure, HttpOnly, SameSite, path and expiry | Pending |
| E08 | Authentication resilience | Perform bounded five-attempt test | Pending |
| E09–E16 | Mutillidae assessment | Repeat relevant tests against Mutillidae | Pending |
| E17 | Cross-target comparison | Compare DVWA and Mutillidae controls | Pending |
| E18 | Cleanup | Confirm markers, sessions and test artifacts are removed | Pending |

---

## Tools

The assessment may use:

- Burp Suite
- Browser Developer Tools
- HTTP request/response inspection
- Linux command-line utilities
- DVWA
- OWASP Mutillidae II

---

## XSS Testing Approach

### Reflected XSS

The assessment identifies:

**Input → HTTP request → Server processing → HTTP response → Browser rendering**

A harmless JavaScript marker is used to determine whether user-controlled input is reflected into an executable browser context.

### Stored XSS

The assessment identifies:

**Input → Server-side storage → Later retrieval → Browser rendering**

The stored marker is retrieved from a second learner-controlled browser session to demonstrate persistence.

### DOM-Based XSS

The assessment identifies:

**Client-side source → JavaScript processing → Dangerous sink → DOM**

Particular attention is given to sources such as URL-controlled values and dangerous rendering functions such as `document.write()`.

---

## Session Management Testing

The session lifecycle assessment records:

1. Session state before authentication.
2. Session state after successful authentication.
3. Whether the session identifier changes during authentication.
4. Session state after logout.
5. Whether the previous authenticated session remains usable after logout.

Only learner-controlled sessions are used.

---

## Cookie Security Review

Cookie attributes reviewed include:

| Attribute | Purpose |
|---|---|
| Secure | Restricts cookie transmission to HTTPS |
| HttpOnly | Prevents JavaScript access to the cookie |
| SameSite | Helps control cross-site cookie transmission |
| Domain | Defines applicable host scope |
| Path | Defines applicable URL path |
| Expiry/Max-Age | Defines cookie lifetime |

Actual session tokens are not included in the public repository.

---

## Authentication Resilience Testing

The authentication test is intentionally limited.

For each target:

- One dedicated learner-owned account is used.
- No more than five failed attempts are performed.
- Timing and server responses are recorded.
- Rate limiting or lockout behavior is documented if observed.
- No real-user credentials are tested.

The objective is to determine whether the application provides meaningful resistance against repeated authentication failures.

---

## Findings Summary

### DVWA

| Area | Result |
|---|---|
| Reflected XSS | Confirmed |
| DOM XSS source/sink | Identified |
| Stored XSS | Confirmed |
| Security-level retest | Pending |
| Session lifecycle | Pending |
| Cookie security | Pending |
| Authentication resilience | Pending |

### Mutillidae II

| Area | Result |
|---|---|
| XSS assessment | Pending |
| Session management | Pending |
| Cookie security | Pending |
| Authentication resilience | Pending |

---

## Remediation Strategy

Recommended defensive controls include:

### XSS Prevention

- Apply context-aware output encoding.
- Validate input where appropriate.
- Avoid unsafe HTML rendering.
- Use safe DOM APIs such as `textContent` where applicable.
- Avoid dangerous client-side sinks such as unsafe `document.write()` usage.
- Implement an appropriate Content Security Policy as defense in depth.

### Session Security

- Rotate session identifiers after authentication.
- Invalidate authenticated sessions during logout.
- Use secure session-management mechanisms.
- Minimize session lifetime where appropriate.

### Cookie Security

Configure appropriate:

- `Secure`
- `HttpOnly`
- `SameSite`
- `Domain`
- `Path`
- Expiration/lifetime

attributes.

### Authentication Security

- Implement rate limiting.
- Apply progressive delays where appropriate.
- Monitor repeated authentication failures.
- Consider carefully designed account lockout controls.
- Implement MFA for sensitive accounts.

---

## Cleanup

Before final submission:

- Remove all stored XSS test markers.
- Reset application test data where appropriate.
- Log out all learner-controlled sessions.
- Clear temporary browser profiles.
- Reset/unlock the dedicated authentication test account if required.
- Remove unnecessary temporary files.
- Ensure no session tokens, credentials, or sensitive authentication data are included in the repository.
- Preserve only the evidence required for assessment.

---

## Evidence Naming Convention

Files followed the evidence identifier:

```text
E01-request.txt
E01-response.txt
E01-screenshot.png

E02-request.txt
E02-response.txt
E02-screenshot.png

E03-source-sink.txt
E03-source-sink.png

E04-submit-request.txt
E04-submit-response.txt
E04-second-session-request.txt
E04-second-session-response.txt
E04-second-session.png
```

Sensitive authentication/session are redacted before committing evidence to a public repository.

---

## Assessment Status

**Lab:** Offensive Security I — Lab 4  
**Assessment:** XSS, Session Management and Authentication Resilience  
**Environment:** Authorized isolated laboratory  
**Primary Targets:** DVWA and OWASP Mutillidae II  
**Status:** In Progress

---

## Conclusion

This assessment is designed to demonstrate practical understanding of browser-side injection, session security, cookie protections, and authentication resilience while maintaining strict laboratory boundaries.

All testing uses controlled applications, learner-owned accounts, learner-controlled sessions, and harmless security markers.