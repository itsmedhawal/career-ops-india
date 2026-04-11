# Security Policy

## Reporting a Vulnerability

Do NOT open a public issue for security vulnerabilities.

Instead, please reach out to  **[Dhawal](https://www.linkedin.com/in/dhawalshrivastava/)** with:

1. Description of the vulnerability
2. Steps to reproduce
3. Potential impact
4. Suggested fix (if any)

I will try to respond within 72 hours. I will work with you to understand and address the issue before any public disclosure.

## Scope

Security issues in the following are in scope:

* Scripts (`*.mjs`) -- command injection, path traversal, SSRF
* Dashboard (`dashboard/`) -- any Go binary vulnerabilities
* Templates (`templates/`) -- XSS in generated HTML/PDF
* Configuration -- secrets exposure, unsafe defaults

## Out of Scope

* Issues in third-party dependencies (report upstream)
* Issues requiring physical access to the user's machine
* Social engineering attacks
* career-ops-india is a local tool -- there is no hosted service to attack

## Disclosure Policy

I follow coordinated disclosure. Once a fix is released, we will credit the reporter (unless they prefer anonymity) in the release notes.

## Note on Fork

career-ops-india is a fork of [santifer/career-ops](https://github.com/santifer/career-ops). If a vulnerability exists in the original engine (scripts, dashboard, PDF generation), please report it upstream to Santiago at hi@santifer.io as well. I will coordinate with the original author where fixes need to be applied to shared code.
