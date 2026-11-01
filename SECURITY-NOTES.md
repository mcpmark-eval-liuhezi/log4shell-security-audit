# Log4Shell Security Notes (CVE-2021-44228)

## Summary

**Log4Shell** is a critical remote code execution (RCE) vulnerability in Apache Log4j 2, triggered via JNDI lookups in log messages. An unauthenticated remote attacker who can control log output can execute arbitrary code loaded from an LDAP or other JNDI endpoint.

## Key Facts

- **CVE ID:** CVE-2021-44228
- **Affected versions:** Apache Log4j 2 `2.0-beta9` through `2.14.1` (i.e., `[2.0-beta9, 2.3.1) ∪ [2.4, 2.12.2) ∪ [2.13.0, 2.15.0)`)
- **Fixed version:** `2.15.0` (Java 8+); recommended fixed versions per CISA/ Apache: `2.17.1` (Java 8), `2.12.4` (Java 7), `2.3.2` (Java 6)
- **Severity:** CVSS 3.x **10.0 CRITICAL** (CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:C/C:H/I:H/A:H)
- **Component affected:** `log4j-core` only; `log4j-api`-only applications are not impacted

## Remediation

1. **Upgrade** log4j-core to 2.17.1 (Java 8+), 2.12.4 (Java 7), or 2.3.2 (Java 6).
2. **Detect** vulnerable deployments by scanning dependencies and filesystem for the `JndiLookup` class and affected version ranges.
3. **Hardening:** set `-Dlog4j2.formatMsgNoLookups=true` (or env `LOG4J_FORMAT_MSG_NO_LOOKUPS=true`); remove `JndiLookup.class` from the jar as a interim measure.
4. **Automated dependency scanning:** enable Dependabot, OWASP Dependency-Check, Snyk, Trivy, or GitHub Advanced Security with a fail-closed policy on log4j-core `< 2.17.1`.

## Sources

- NVD: https://nvd.nist.gov/vuln/detail/cve-2021-44228
- Apache Logging Services Security Page: https://logging.apache.org/security.html
- CISA Apache Log4j Vulnerability Guidance: https://www.cisa.gov/news-events/news/apache-log4j-vulnerability-guidance
- GitHub Advisory Database (GHSA-jfh8-c2jp-5v3q): https://github.com/advisories/ghsa-jfh8-c2jp-5v3q
