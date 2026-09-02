# Lab 3 — File Inclusion and SQL Injection Security Assessment

## Objective

Assess unsafe file/resource selection and database queries in DVWA and OWASP Mutillidae II using benign markers and minimal-impact evidence.

## Scope

- DVWA File Inclusion
- Mutillidae II LFI/RFI challenges where available
- DVWA SQL Injection/authentication exercises
- Mutillidae II SQL Injection challenges

## Rules

- Use only local/host-only training applications.
- Use benign local/remote markers only.
- No OS secrets, private keys, remote code, database dumping, credential collection, or unrelated enumeration.
- Stop after obtaining the minimum evidence required.

## Evidence

| Evidence | Description | Status |
|---|---|---|
| E01 | File-selection baseline | Completed |
| E02 | LFI marker and hash | Completed |
| E03 | Path/error disclosure | Pending |
| E04 | Controlled RFI marker, if assigned | Pending |
| E05 | SQL baseline | Pending |
| E06 | Behavioural SQLi proof | Pending |
| E07 | Minimal authentication/marker evidence | Pending |
| E08 | Security-level comparison/retest | Pending |
| E09 | Remediation | Pending |
| E10 | Cleanup and restoration | Pending |

## Key Analysis

- Identify the parameter controlling server-side resource selection.
- Demonstrate that a benign marker can influence file inclusion.
- Distinguish server-side inclusion from browser redirection.
- Determine whether SQL input changes query logic or only produces an error.
- Compare insecure and stronger security modes.
- Document the relevant trust boundaries.

## Remediation

Recommended controls include:

- Fixed resource mappings instead of user-controlled paths.
- Canonicalisation and strict path validation.
- Disable unnecessary remote inclusion.
- Prepared statements/parameterised queries.
- Generic database error messages.
- Least-privileged database accounts.

## Submission

- Professional PDF report
- ZIP evidence package
- Evidence register
- Activity log
- Screenshots, requests/responses, hashes and notes

## Cleanup

- Stop any local marker service.
- Restore secure configuration.
- Reset application databases/content.
- Remove temporary marker files.
- Confirm no database dump or persistent artefact was created.

**Environment:** Local/host-only DVWA and OWASP Mutillidae II  
**Lab:** 3 
**Course:** Offensive Security I  
**Course Window:** 24 August– 1 September 2026
