# Lab 5 — OWASP ZAP Integrated Assessment, Remediation and Retest Capstone

## Overview

This lab provides a final end-to-end security assessment of two deliberately vulnerable web applications:

- DVWA (Damn Vulnerable Web Application)
- OWASP Mutillidae II

The assessment combines OWASP ZAP automated assessment with manual security validation, minimal-impact proof, impact analysis, remediation, retesting, prioritisation, cleanup, and professional reporting.

Testing was performed only against **authorized, deliberately vulnerable local applications** in an isolated laboratory environment.

---

## Objectives

The assessment objectives were to:

1. Restore and verify the clean laboratory state.
2. Define the authorized scope, exclusions, and stop conditions.
3. Configure OWASP ZAP Protected Mode.
4. Browse DVWA and Mutillidae II through ZAP.
5. Record site trees and passive alerts.
6. Configure a reduced active-scan policy.
7. Perform one deliberately limited active scan against authorized paths.
8. Review and classify selected ZAP alerts.
9. Manually validate representative findings.
10. Collect minimal-impact request and response evidence.
11. Distinguish observed impact from potential impact.
12. Apply remediation or stronger security controls.
13. Retest affected functionality.
14. Compare original and retested behavior.
15. Prioritize validated findings.
16. Remove learner-created artifacts.
17. Reset both applications.
18. Produce the final report and evidence package.

---

## Scope

### Applications

- DVWA
- OWASP Mutillidae II

### Automated Assessment

Testing included:

- ZAP Protected Mode
- Passive scanning
- Site-tree discovery
- Reduced-scope spidering
- One deliberately limited active scan
- Alert review and classification

### Manual Validation

Manual testing included:

- Representative finding validation
- Minimal-impact proof
- Request and response inspection
- Observed-impact analysis
- Potential-impact analysis
- Remediation verification
- Retesting

### Remediation and Retesting

Testing included:

- Applying stronger security controls where appropriate
- Repeating the affected request or action
- Comparing original and retested behavior
- Recording residual risk

---

## Rules of Engagement

All testing remained within the authorized local laboratory environment.

### Allowed

- OWASP ZAP Protected Mode
- Passive scanning
- Controlled site-tree discovery
- Reduced-scope spidering
- One limited active scan
- Manual request and response inspection
- Harmless test inputs
- Minimal-impact proof
- Learner-controlled browser sessions
- Remediation and retesting
- Evidence collection using screenshots and exported ZAP output

### Prohibited

The assessment did **not** include:

- Database dumping
- Credential dumping
- Credential stuffing
- Password spraying
- Persistence
- Privilege escalation
- Lateral movement
- Destructive actions
- External callbacks
- Reverse shells
- Malware
- Attacks against real accounts
- Testing publicly exposed systems
- Access to unrelated systems or sensitive data

### Stop Conditions

Testing was stopped or restricted if an action could:

- Affect systems outside the authorized scope
- Cause unnecessary service disruption
- Access unrelated data
- Create persistence
- Require privilege escalation
- Generate external network activity
- Produce destructive or irreversible effects

---

## Evidence Register

| ID  | Evidence                                        | Purpose                                                                | Status  |
| --- | ----------------------------------------------- | ---------------------------------------------------------------------- | ------- |
| E01 | Final scope, rules of engagement and baseline   | Establish authorized targets, exclusions and initial application state | Complted |
| E02 | ZAP Protected Mode and context                  | Demonstrate controlled scanning configuration                          | Pending |
| E03 | DVWA site tree and passive alerts               | Record discovered DVWA paths and passive findings                      | Pending |
| E04 | Mutillidae II site tree and passive alerts      | Record discovered Mutillidae II paths and passive findings             | Pending |
| E05 | Reduced active-scan policy                      | Demonstrate constrained active-scan configuration                      | Pending |
| E06 | Limited active-scan summary                     | Record results from the authorized active scan                         | Pending |
| E07 | Manual validation — finding 1                   | Confirm the first representative finding                               | Pending |
| E08 | Manual validation — finding 2                   | Confirm the second representative finding                              | Pending |
| E09 | Manual validation — finding 3                   | Confirm the third representative finding                               | Pending |
| E10 | False-positive and informational alert analysis | Distinguish confirmed findings from non-findings                       | Pending |
| E11 | Observed-versus-potential impact matrix         | Document demonstrated and possible security impact                     | Pending |
| E12 | Remediation retest 1                            | Verify the first remediation result                                    | Pending |
| E13 | Remediation retest 2                            | Verify the second remediation result                                   | Pending |
| E14 | Cross-application comparison                    | Compare DVWA and Mutillidae II behavior and controls                   | Pending |
| E15 | Prioritized findings                            | Rank validated findings by risk and remediation priority               | Pending |
| E16 | Cleanup and reset                               | Confirm removal of test artifacts and restoration of the lab           | Pending |
| E17 | Final evidence and register verification        | Confirm submission completeness and consistency                        | Pending |

Additional evidence IDs may be added where required by the actual testing results.

---

## Tools

The assessment may use:

- OWASP ZAP
- Browser Developer Tools
- HTTP request and response inspection
- Linux command-line utilities
- DVWA
- OWASP Mutillidae II
- Screenshots and exported scanner results
- Spreadsheet or document tools for evidence tracking

---

## OWASP ZAP Assessment Approach

### Protected Mode

OWASP ZAP is configured in Protected Mode so that automated testing remains restricted to the explicitly authorized laboratory targets.

The ZAP context includes only:

- Local DVWA
- Local OWASP Mutillidae II

No public or unrelated host is included in the testing context.

### Passive Scanning

Both applications are browsed through ZAP to populate the site trees and allow passive analysis.

Passive assessment records:

- Discovered paths
- Parameters
- Forms
- Cookies
- Security headers
- Information disclosure indicators
- Other passive alerts

Passive alerts are reviewed before any active scanning is performed.

### Site-Tree Discovery

The site tree is reviewed to identify:

- Application paths
- Functional areas
- Parameters
- Authentication-related pages
- Administrative or sensitive-looking paths
- Duplicate or irrelevant resources
- Paths that must be excluded from active scanning

### Reduced-Scope Spidering

Spidering is limited to the authorized local applications and is configured to avoid unnecessary expansion beyond the intended laboratory scope.

### Limited Active Scan

One deliberately limited active scan is performed against explicitly authorized paths.

The active scan is configured to:

- Use a reduced scan policy
- Avoid destructive or unnecessary tests
- Exclude irrelevant paths
- Avoid testing outside the local laboratory applications
- Minimize request volume where possible
- Stop if unexpected behavior occurs

Automated active-scan alerts are treated as leads for investigation rather than confirmed vulnerabilities.

---

## Manual Validation Approach

Manual validation is used to determine whether selected ZAP alerts represent genuine security issues.

Each validated finding records:

- Application
- Affected path or function
- Relevant parameter or input
- Baseline request
- Modified request or test input
- Observed response
- Security significance
- Observed impact
- Potential impact
- Remediation
- Retest result
- Supporting evidence

A finding is not reported as confirmed unless the available evidence demonstrates that the condition exists and is security-relevant within the authorized scope.

---

## Finding Categories

The assessment may identify findings from categories such as:

- Injection
- Cross-Site Scripting
- Security misconfiguration
- Missing or weak security headers
- Information disclosure
- Authentication or session weaknesses
- Access-control weaknesses
- Insecure cookie configuration
- Unvalidated redirects
- Other OWASP-relevant categories identified during testing

Only categories supported by actual laboratory evidence are included in the final report.

---

## Observed and Potential Impact

The assessment distinguishes between:

### Observed Impact

The effect directly demonstrated during authorized testing, such as:

- A reflected or stored response change
- Exposure of non-sensitive application information
- Missing security controls
- Unauthorized behavior within the learner-controlled session
- A measurable difference before and after remediation

### Potential Impact

The broader risk that could arise if the weakness were exploited in a realistic environment.

Potential impact is described conservatively and is not presented as observed unless it was directly demonstrated.

The assessment does not perform destructive testing, privilege escalation, persistence, database dumping, or access to unrelated data to establish potential impact.

---

## Remediation and Retesting

At least two validated findings are selected for remediation and retesting where the laboratory environment permits.

For each retested finding, the assessment records:

1. Original behavior.
2. Security weakness identified.
3. Control or configuration change applied.
4. Retest request or input.
5. Retest response or behavior.
6. Whether the original issue was reduced or removed.
7. Residual risk.
8. Supporting evidence.

Possible defensive controls include:

- Context-aware output encoding
- Input validation
- Parameterized queries
- Secure session handling
- Stronger authentication controls
- Security headers
- Secure cookie attributes
- Access-control enforcement
- Safer application configuration
- Removal of unnecessary information disclosure

---

## Findings Summary

### DVWA

| Area                  | Result  |
| --------------------- | ------- |
| Site-tree discovery   | Completed |
| Passive assessment    | Pending |
| Limited active scan   | Pending |
| Manual validation     | Pending |
| Remediation retesting | Pending |
| Overall assessment    | Pending |

### OWASP Mutillidae II

| Area                  | Result  |
| --------------------- | ------- |
| Site-tree discovery   | Pending |
| Passive assessment    | Pending |
| Limited active scan   | Pending |
| Manual validation     | Pending |
| Remediation retesting | Pending |
| Overall assessment    | Pending |

---

## Cross-Application Comparison

The final comparison will examine:

- Number and type of passive alerts
- Number and type of active-scan alerts
- Manual validation results
- Differences in application behavior
- Security configuration differences
- Remediation behavior
- Residual risk
- Relative assessment difficulty

| Assessment Area             | DVWA    | Mutillidae II |
| --------------------------- | ------- | ------------- |
| Site-tree size and coverage | Pending | Pending       |
| Passive findings            | Pending | Pending       |
| Active findings             | Pending | Pending       |
| Manual validation           | Pending | Pending       |
| Security controls           | Pending | Pending       |
| Remediation behavior        | Pending | Pending       |
| Residual risk               | Pending | Pending       |
| Overall observations        | Pending | Pending       |

---

## Prioritization Method

Validated findings are prioritized using:

- Observed impact
- Potential impact
- Likelihood
- Ease of exploitation
- Exposure within the application
- Availability of effective remediation
- Importance of the affected function

| Priority | Finding | Application | Severity | Observed Risk | Likelihood | Priority Rationale |
| -------- | ------- | ----------- | -------- | ------------- | ---------- | ------------------ |
| 1        | Pending | Pending     | Pending  | Pending       | Pending    | Pending            |
| 2        | Pending | Pending     | Pending  | Pending       | Pending    | Pending            |
| 3        | Pending | Pending     | Pending  | Pending       | Pending    | Pending            |

---

## Remediation Strategy

### Input and Output Security

- Apply context-aware output encoding.
- Validate input where appropriate.
- Use parameterized queries for database access.
- Avoid unsafe HTML rendering.
- Use safe DOM APIs where applicable.
- Avoid dangerous client-side sinks.
- Implement an appropriate Content Security Policy as defense in depth.

### Authentication and Session Security

- Rotate session identifiers after authentication.
- Invalidate authenticated sessions during logout.
- Use secure session-management mechanisms.
- Minimize session lifetime where appropriate.
- Apply rate limiting to repeated authentication failures.
- Monitor repeated authentication failures.
- Consider carefully designed account lockout controls.
- Implement MFA for sensitive accounts.

### Cookie Security

Configure appropriate:

- `Secure`
- `HttpOnly`
- `SameSite`
- `Domain`
- `Path`
- Expiration and lifetime

attributes.

### Security Headers

Where appropriate, configure:

- Content Security Policy
- Strict-Transport-Security
- X-Content-Type-Options
- Referrer-Policy
- Frame-ancestors or equivalent clickjacking protection
- Other relevant response headers

### Access Control

- Enforce authorization on the server side.
- Deny access by default where appropriate.
- Validate object ownership.
- Avoid relying on client-side restrictions.
- Review administrative and sensitive paths.

---

## Cleanup

Before final submission:

- Stop all ZAP scans.
- Remove learner-created markers.
- Remove stored test entries where applicable.
- Log out active sessions.
- Clear test sessions.
- Reset both applications.
- Restore the clean snapshot where required.
- Remove temporary files and test artifacts.
- Verify that no temporary listener, process, account, token or test artifact remains.
- Ensure no session tokens, credentials or sensitive authentication data are included in the repository.
- Preserve only the evidence required for assessment.

---

## Evidence Naming Convention

Evidence files follow the evidence identifier:

```text
E01-scope-and-baseline.txt
E01-scope-and-baseline.png

E02-zap-protected-mode.txt
E02-zap-protected-mode.png

E03-dvwa-site-tree.txt
E03-dvwa-passive-alerts.csv
E03-dvwa-site-tree.png

E04-mutillidae-site-tree.txt
E04-mutillidae-passive-alerts.csv
E04-mutillidae-site-tree.png

E05-active-scan-policy.txt
E05-active-scan-policy.png

E06-active-scan-summary.html
E06-active-scan-summary.png

E07-finding-1-request.txt
E07-finding-1-response.txt
E07-finding-1-validation.png

E08-finding-2-request.txt
E08-finding-2-response.txt
E08-finding-2-validation.png

E09-finding-3-request.txt
E09-finding-3-response.txt
E09-finding-3-validation.png

E10-alert-classification.txt
E10-alert-classification.png

E11-impact-matrix.xlsx
E11-impact-matrix.png

E12-retest-1-before.txt
E12-retest-1-after.txt
E12-retest-1.png

E13-retest-2-before.txt
E13-retest-2-after.txt
E13-retest-2.png

E14-cross-application-comparison.xlsx
E14-cross-application-comparison.png

E15-prioritized-findings.xlsx
E15-prioritized-findings.png

E16-cleanup-and-reset.txt
E16-cleanup-and-reset.png

E17-final-verification.txt
E17-final-verification.png
```

Sensitive information is redacted before evidence is committed to a public repository.

---

## Submission Package

The final submission contains:

---

## Final Assessment Questions

The final report will answer:

1. Which validated finding presents the greatest observed risk, and why?
2. Which ZAP alert required the most manual interpretation?
3. What is the difference between automated discovery and a confirmed finding?
4. What did the retest prove, and what residual risk remains?

---

## Assessment Status

**Lab:** Offensive Security I — Lab 5
**Assessment:** OWASP ZAP Integrated Assessment, Remediation and Retest Capstone
**Environment:** Authorized isolated laboratory
**Primary Targets:** DVWA and OWASP Mutillidae II
**Status:** In Progress

---

## Conclusion

This assessment is designed to demonstrate practical understanding of automated web-application security testing, manual validation, evidence-based reporting, remediation, retesting, risk prioritization, and laboratory cleanup.

All testing uses controlled applications, authorized local targets, minimal-impact techniques, learner-controlled sessions, and evidence supported by the learner's own observations.
