# Security Policy

## Supported Versions

The Bedrock Horizons project primarily supports the latest stable release.

Security fixes are generally applied to the current development branch and the most recent release.

| Version | Supported |
| ------- | :-------: |
| Latest Release | Yes |
| Development Branch (`main`) | Yes |
| Older Releases | No |
| Archived Versions | No |

---

# Reporting a Security Vulnerability

If you believe you have discovered a security vulnerability in Bedrock Horizons, please report it responsibly.

Examples include, but are not limited to:

- Malicious code execution
- Remote code execution (RCE)
- Supply chain vulnerabilities
- Dependency vulnerabilities
- Build system vulnerabilities
- Malicious scripts
- Unsafe GitHub Actions workflows
- Sensitive information accidentally committed to the repository

Please **do not** disclose security vulnerabilities publicly before they have been investigated.

Instead:

1. Open a private GitHub Security Advisory if the repository has security advisories enabled.
2. If private reporting is unavailable, contact the project maintainer directly.
3. Include as much information as possible to help reproduce and investigate the issue.

Helpful information includes:

- A description of the vulnerability.
- Steps to reproduce.
- A proof of concept, if appropriate.
- The affected version or commit.
- Any suggested mitigations.

---

# Response Process

After receiving a vulnerability report, the project maintainer will:

1. Acknowledge receipt of the report.
2. Investigate the issue.
3. Determine its severity and impact.
4. Develop and test a fix.
5. Release the fix as soon as practical.
6. Publicly disclose the issue after a fix is available, when appropriate.

Response times may vary depending on the complexity of the issue and maintainer availability.

---

# Scope

This security policy applies to:

- Source code
- Build scripts
- GitHub Actions workflows
- Project dependencies
- Release artifacts
- Documentation that affects security

This policy does **not** apply to:

- Minecraft: Bedrock Edition itself
- Third-party software
- Operating systems
- Hardware-specific vulnerabilitie
- Community-made forks of Bedrock Horizons

---

# Responsible Disclosure

Please:

- Allow reasonable time for investigation and remediation.
- Avoid publicly disclosing vulnerabilities before a fix is available.
- Do not exploit vulnerabilities beyond what is necessary to demonstrate the issue.
- Avoid accessing or modifying data that does not belong to you.

Good-faith security research is welcomed and appreciated.

---

# Dependencies

Bedrock Horizons attempts to use trusted dependencies and development tools whenever possible.

If you discover a vulnerability in a third-party dependency used by this project, please also report it to us about that dependency according to their security policy.

---

# Contact

For security-related concerns, use GitHub's private security reporting features whenever available. If private reporting is not enabled, contact the project maintainer through the project's official GitHub repository.

Please do not use GitHub Issues for reporting security vulnerabilities, as Issues are public.
