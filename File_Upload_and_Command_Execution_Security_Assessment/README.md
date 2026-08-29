# ICDFA Offensive Security I — Lab 2
## File Upload and Command Execution Security Assessment

**Assessment Type:** Practical Security Assessment  
**Course:** Offensive Security I  
**Lab:** 2 of 5  
**Environment:** Isolated local training environment  
**Applications:** Damn Vulnerable Web Application (DVWA) and OWASP Mutillidae II  
**Testing Tool:** Burp Suite  
**Assessment Window:** 24 August 2026 – 6 September 2026  
**Recommended Focus:** 26–29 August 2026  
**Assessment Deadline:** 29 August 2026, 11:59 PM WAT  

---

## 1. Lab Overview

This laboratory evaluates file-upload validation and command-execution security controls in intentionally vulnerable web applications.

Testing is performed exclusively against locally installed DVWA and OWASP Mutillidae II instances running inside an isolated training environment.

The assessment focuses on identifying security weaknesses while using only harmless marker files and minimal-impact, instructor-approved validation techniques.

No malware, executable upload, reverse shell, persistence mechanism, privilege escalation, destructive command, external callback, or unrelated-file access is permitted.

---

## 2. Objectives

The assessment aims to demonstrate the ability to:

- Assess client-side and server-side file-upload validation.
- Examine filename, MIME type, content, and storage handling.
- Identify command-execution trust boundaries.
- Compare insecure and stronger security modes.
- Determine the difference between observed and potential impact.
- Document repeatable technical evidence.
- Recommend layered remediation controls.
- Restore both applications to a clean state after testing.

---

## 3. Rules of Engagement

All testing remains within the authorized training environment.

### Authorized Targets

- Local DVWA instance
- Local OWASP Mutillidae II instance

### Authorized Testing

- Harmless image and text marker files.
- Controlled filename/content mismatch tests.
- Normal application requests.
- Burp Suite interception and analysis.
- Instructor-approved minimal command markers.
- Security-level comparison and retesting.
- Application reset and cleanup.

### Prohibited Testing

The following are explicitly excluded:

- Malware
- Executable uploads
- Reverse shells
- External callbacks
- Persistence
- Privilege escalation
- Destructive commands
- Access to unrelated files
- Credential harvesting
- Testing against external systems
- Public exposure of the vulnerable applications

---

## 4. Assessment Phases

### Phase 1 — Evidence Preparation

Create harmless marker files and record:

- Filename
- Extension
- MIME/content type
- File size
- SHA-256 hash
- Purpose

### Phase 2 — Upload Baseline

Perform normal uploads against both applications.

Record:

- HTTP request
- HTTP response
- Filename
- Stored filename
- Storage path
- Retrieval behaviour

### Phase 3 — Validation Comparison

Perform a harmless filename/content mismatch test.

Determine whether validation occurs:

- In the browser
- On the server
- At both layers

### Phase 4 — Storage Assessment

Determine whether uploaded content is:

- Renamed
- Access-controlled
- Stored outside an executable path
- Directly retrievable
- Served with an appropriate content type

### Phase 5 — Command Baseline

Capture normal behaviour of the command-backed feature in:

- DVWA
- Mutillidae II

### Phase 6 — Minimal Execution Proof

Use only an instructor-approved harmless marker to determine whether user input can alter backend command meaning.

### Phase 7 — Impact Assessment

Document:

- Affected parameter
- Observed behaviour
- Execution context
- Observed impact
- Potential impact

No unrelated system resources are accessed.

### Phase 8 — Secure Comparison

Repeat the relevant tests using:

- A stronger DVWA security level
- Mutillidae secure mode

Document the differences.

### Phase 9 — Remediation

Develop recommendations addressing:

- Upload validation
- File naming
- File storage
- Content delivery
- Command execution architecture
- Input handling
- Least privilege
- Defence in depth

---

## 5. Evidence Register

| Evidence ID | Application | Test | Status |
|---|---|---|---|
| E01 | DVWA | Upload marker preparation | Completed |
| E02 | DVWA | Normal upload baseline | In progress |
| E03 | DVWA | Filename/content mismatch | Completed |
| E04 | DVWA | Successful upload and storage assessment | Pending |
| E05 | Mutillidae II | Normal upload baseline | Pending |
| E06 | Mutillidae II | Upload validation/storage assessment | Pending |
| E07 | DVWA | Command-execution baseline | Pending |
| E08 | Mutillidae II | Command-execution baseline | Pending |
| E09 | DVWA | Minimal-impact execution validation | Pending |
| E10 | Mutillidae II | Minimal-impact execution validation | Pending |
| E11 | DVWA | Stronger security-level retest | Pending |
| E12 | Mutillidae II | Secure-mode retest | Pending |
| E13 | Cleanup and restoration | Final verification | Pending |

> Evidence numbering may be adjusted during the investigation if additional evidence is required. The evidence register should remain synchronized with the final evidence files.

---

## 6. Current Evidence

### E01 — Upload Marker

A harmless upload marker was created for the assessment.

**File:**

`upload-maker.txt`

**SHA-256:**

`13bc692f9e69dabdeffc7c93040f1d1087cca59c19ff5a099b8724e5ea7b278a`

Purpose:

> Provide a known harmless marker for testing upload handling and validation.

---

### E03 — Filename/Content Mismatch

A filename/content mismatch test was performed against DVWA at the `impossible` security level.

The request used:

```text
Filename: mismatch.jpg
Declared Content-Type: image/jpeg
Actual Content: File-Upload-MISMATCH-MARKER
```

The server returned:

```text
HTTP/1.1 200 OK
```

with the application message:

```text
Your image was not uploaded. We can only accept JPEG or PNG images.
```

### Observation

The server rejected the upload even though the request declared an image filename and MIME type.

### Preliminary conclusion

The result indicates that the tested upload control performs server-side validation and does not rely solely on the client-supplied filename or MIME type.

The conclusion is limited to the tested condition and security level.

---

## 7. Environment

### DVWA

Local URL:

```text
http://127.0.0.1:8080/DVWA/
```

File Upload endpoint:

```text
/DVWA/vulnerabilities/upload/
```

Command Injection endpoint:

```text
/DVWA/vulnerabilities/exec/
```

### OWASP Mutillidae II

Local installation running through Docker.

The application is bound to the local training environment and is not intended to be publicly accessible.

### Network

The Kali VM uses a host-only network.

Example observed interface:

```text
eth0    192.168.56.101/24
```

No default route was present during the documented isolated testing configuration.

Docker networks were also observed locally:

```text
172.18.0.0/16
172.19.0.0/16
```

---

## 8. Tools

Primary testing tool:

- Burp Suite

Supporting tools:

```text
curl
sha256sum
file
ls
ip
ss
Docker
Docker Compose
```

These tools are used for controlled observation, evidence collection, verification, and environment management.

---

## 9. Evidence File Naming Convention

Evidence should use a consistent naming scheme.

Example:

```text
e01-upload-marker/
e02-dvwa-upload-baseline/
e03-dvwa-mismatch/
e04-dvwa-storage/
e05-mutillidae-upload/
e06-mutillidae-storage/
e07-dvwa-command-baseline/
e08-mutillidae-command-baseline/
e09-dvwa-execution-proof/
e10-mutillidae-execution-proof/
e11-dvwa-secure-retest/
e12-mutillidae-secure-retest/
e13-cleanup/
```

Recommended files inside each evidence directory:

```text
request.txt
response.txt
screenshot.png
notes.md
hashes.txt
```

Only files relevant to that evidence item should be included.

---

## 10. Evidence Quality Requirements

Every evidence item should answer:

1. What was tested?
2. Which application was tested?
3. Which security level or mode was active?
4. What request was sent?
5. What response was received?
6. What changed?
7. What does the evidence prove?
8. What does it not prove?

Evidence should be reproducible and should distinguish direct observations from security implications.

---

## 11. Analysis Questions

The final report will answer the following questions.

### 1. Why is browser-only upload validation insufficient?

Because requests can be generated or modified outside the normal browser interface. Security decisions must therefore be enforced server-side.

### 2. What proves that command input was treated as executable structure rather than data?

The investigation will identify observable changes in backend command behaviour resulting from controlled input while avoiding destructive execution.

### 3. Why is minimal proof sufficient for both weaknesses?

A controlled proof establishes the security boundary violation without unnecessarily increasing impact or accessing unrelated resources.

### 4. Which control produced the greatest improvement in stronger mode?

The final comparison will identify the control that most significantly changes the observed behaviour between insecure and stronger configurations.

---

## 12. Observed vs Potential Impact

The final assessment will distinguish between what was directly demonstrated and what could theoretically result from the weakness.

| Finding | Observed Impact | Potential Impact |
|---|---|---|
| Upload validation weakness | To be determined from testing | Depends on accepted content, storage and execution configuration |
| Unsafe storage | To be determined | Possible unauthorized content delivery or execution depending on server configuration |
| Command injection | To be determined | Possible execution with the privileges of the application process |
| Stronger security mode | To be determined | Reduced attack surface/control effectiveness |

Potential impact will not be presented as observed compromise.

---

## 13. Remediation Areas

### File Upload

Recommended layered controls include:

- Server-side validation.
- Allowlisting permitted file types.
- Verification of actual file content.
- Safe filename generation.
- Removal of user-controlled path components.
- Size limits.
- Storage outside executable web directories where practical.
- Non-executable upload directories.
- Controlled content delivery.
- Appropriate access controls.
- Malware scanning where appropriate.
- Defence in depth.

### Command Execution

Recommended architecture includes:

- Avoiding shell invocation where possible.
- Using structured APIs instead of shell commands.
- Strict allowlists for permitted operations.
- Treating user input as data rather than command structure.
- Avoiding shell metacharacter interpretation.
- Running services with least privilege.
- Applying operating-system-level isolation where appropriate.
- Logging security-relevant command activity.

---

## 14. Cleanup and Restoration

At the conclusion of testing:

- Remove learner-created marker files.
- Remove only learner-created uploads.
- Reset DVWA.
- Reset Mutillidae II.
- Confirm no temporary accounts were created.
- Confirm no scheduled tasks were created.
- Confirm no listeners were created.
- Confirm no persistence mechanisms were introduced.
- Confirm all testing remained local.
- Record cleanup evidence.

Final cleanup evidence will be recorded as **E13**.

---

## 15. Submission Package

The completed assessment will contain:

### Professional Report

```text
Lab-2-File-Upload-Command-Execution-Assessment.pdf
```

The report will contain:

- Investigation narrative
- Scope
- Methodology
- Evidence
- Findings
- Analysis
- Observed vs potential impact
- Secure-mode comparison
- Remediation
- Cleanup confirmation
- Conclusions

### Evidence Package

```text
Lab-2-Evidence.zip
```

Containing:

- Requests
- Responses
- Screenshots
- Tool output
- Marker hashes
- Notes
- Evidence register
- Activity log
- Final report

---

## 16. Activity Log

| Date/Time | Activity | Tool | Result | Evidence |
|---|---|---|---|---|
| 29 Aug 2026 | Created upload marker | `sha256sum` | Hash recorded | E01 |
| 29 Aug 2026 | Normal DVWA upload attempted | Burp Suite | Upload rejected at current test condition | E02 |
| 29 Aug 2026 | Filename/content mismatch tested | Burp Suite | Server rejected mismatch | E03 |
| 29 Aug 2026 | DVWA database/application preparation | Browser/DVWA | Database reset successful | Setup |
| 29 Aug 2026 | Local lab networking verified | `ip`, `ss` | Host-only/local services confirmed | Environment |

This table will be updated throughout the assessment.

---

## 17. Conclusion

This laboratory is designed to demonstrate professional web application security testing rather than simply obtaining a vulnerable result.

The assessment will focus on:

- Reproducible evidence.
- Controlled testing.
- Clear security reasoning.
- Separation of observed and potential impact.
- Comparison of security controls.
- Root-cause analysis.
- Practical remediation.
- Complete cleanup.

All conclusions will be based on evidence collected from the authorized local training applications.

---

## References

- DVWA — Official project repository: https://github.com/digininja/DVWA
- OWASP Mutillidae II — Official project repository: https://github.com/webpwnized/mutillidae
- OWASP Web Security Testing Guide: https://owasp.org/www-project-web-security-testing-guide/latest/4-Web_Application_Security_Testing/

---

**Assessment Status:** In Progress  
**Current Phase:** Upload Validation and Storage Assessment  
**Next Evidence:** E04 — Successful Upload and Storage Behaviour