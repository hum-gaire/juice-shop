# AppSec Analysis: OWASP Juice Shop

## Overview
This repository demonstrates a complete Application Security testing pipeline
applied to the intentionally vulnerable OWASP Juice Shop application.

## Testing Coverage

| Category | Tool | What It Finds |
|----------|------|---------------|
| **SAST** | Semgrep | OWASP Top 10 patterns, XSS, SQLi, hardcoded secrets |
| **SAST** | CodeQL | Deep taint-flow analysis, data tracking |
| **SCA** | npm audit + Trivy | Known CVEs in dependencies |
| **Secrets** | TruffleHog | API keys, passwords, tokens in code |
| **DAST** | OWASP ZAP | Runtime vulnerabilities, misconfigurations |
| **Container** | Trivy | OS vulnerabilities, image misconfigurations |

## Key Findings

### SAST - Semgrep
- Multiple SQL injection sinks detected
- Hardcoded secrets in test files
- Insecure JWT validation patterns

### SAST - CodeQL
- Cross-site scripting (XSS) data flows
- Server-side request forgery (SSRF) patterns
- Insecure deserialization

### SCA - npm audit
- 100+ known vulnerabilities in dependencies
- Multiple critical severity CVEs

### DAST - ZAP
- Missing security headers
- XSS vulnerabilities in search functionality
- Information disclosure in error messages

## Remediation Approach
1. **Immediate:** Update dependencies with known CVEs
2. **Short-term:** Fix SQL injection with parameterized queries
3. **Long-term:** Implement Content Security Policy (CSP) headers
4. **Ongoing:** Integrate SAST/SCA into CI/CD pipeline

## CI/CD Integration
All scans run automatically on:
- Every push to main
- Every pull request
- Weekly scheduled scans (to catch new CVEs)

## References
- [OWASP Juice Shop](https://owasp.org/www-project-juice-shop/)
- [OWASP Top 10](https://owasp.org/Top10/)
