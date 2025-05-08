## What is SAST ?
==========================


Static Application Security Testing (SAST) in GitLab is a built-in feature that automatically scans your source code for security vulnerabilities. 

It’s part of GitLab’s Secure stage and helps developers catch security issues early in the development lifecycle, directly within the CI/CD pipeline.

It is a type of security testing that analyzes your source code, bytecode, or binary code for vulnerabilities without executing the application.

#### Key Features of GitLab SAST

`Language support` Works with many popular languages like Python, JavaScript, Java, Ruby, Go, C/C++, PHP, etc.

`Automatic setup` GitLab can auto-detect the programming language and set up SAST scanners.

`CI/CD integration` Scans are triggered via .gitlab-ci.yml during merge requests or pipeline runs.

`Reports and merge request feedback` Vulnerabilities are reported in the pipeline and directly in merge requests.

`Customizable` You can enable/disable specific analyzers or configure rules via custom YAML configuration.


## GitLab SAST integration
===============================

Integrating GitLab Static Application Security Testing (SAST) into your CI/CD pipeline helps automatically scan your code for security vulnerabilities. 

GitLab provides built-in support for SAST using CI templates and supports many languages and frameworks out-of-the-box.

#### Steps to Integrate GitLab SAST

1. Auto-DevOps (Automatic Setup) > If Auto DevOps is enabled and your project uses a supported language, GitLab automatically runs SAST.

2. Manual Setup with `.gitlab-ci.yml`

```
include:
  - template: Security/SAST.gitlab-ci.yml
```

After the pipeline runs, navigate to Security & Compliance > Vulnerability Report in your GitLab project.

Each vulnerability includes :-

  - File and line number
  - Suggested fix (if available)
  - CVE/CWE references



## Running SAST in GitLab pipelines
========================================

Running SAST, in GitLab pipelines helps you automatically detect security vulnerabilities in your code during the CI/CD process. 

GitLab provides built-in SAST scanning capabilities that are easy to set up using predefined CI/CD templates.


## Interpreting SAST reports in gitlab
==========================================

Interpreting SAST (Static Application Security Testing) reports in GitLab involves understanding the security vulnerabilities identified in your source code.

#### Where to Find the Report

Go to CI/CD > Pipelines in your GitLab project.

Click on the relevant pipeline.

Select the Security tab.

Click on SAST to view the list of vulnerabilities.


#### Each SAST issue includes :-

`Vulnerability Title`

A short description of the issue, e.g., "SQL Injection" or "Cross-Site Scripting (XSS)".

`Severity`

One of: Critical, High, Medium, Low, Info.

`Confidence`

Indicates how certain the tool is that this is a real issue (High, Medium, Low).

`File & Line Number`

Tells you exactly where the vulnerable code is.

`Description`

A more detailed explanation of the vulnerability and how it could be exploited.

`Remediation Advice`

Suggestions on how to fix or mitigate the issue.

`Tool`

The scanner that detected it (e.g., Bandit, ESLint, Brakeman, etc.).


#### What You Should Do

`Prioritize` Focus on Critical and High severity with High confidence.

`Verify` Review the code manually to confirm the issue (some false positives may exist).

`Fix` Apply secure coding practices or the suggested remediation.

`Document` Use GitLab’s Dismissal Comments if a finding is false positive or acceptable risk.

`Track` Use the Security Dashboard for ongoing vulnerability tracking.

You can download or view the raw gl-sast-report.json artifact if you want to parse it or use it in other tools.


## Best practices to address vulnerabilities
====================================================

`Prioritize by Severity and Confidence` 

Start with Critical & High severity and High confidence issues.

Use tools like GitLab’s Security Dashboard to visualize and sort issues.

Don’t ignore Medium/Low severity—many breaches start small.

`Apply Secure Coding Principles`

Sanitize and validate all inputs (e.g., to prevent XSS, SQLi).

Use parameterized queries for database access.

Avoid using eval(), hardcoded secrets, or insecure cryptographic algorithms.

`Use Safe Libraries and Frameworks`

Stay up to date with dependencies using tools like Dependabot or GitLab’s Dependency Scanning.

Replace outdated or vulnerable libraries with patched versions.

`Implement Defense in Depth`

Use multiple layers of security: e.g., WAF, secure headers, RBAC.

Don’t rely solely on SAST—combine with DAST, dependency scanning, and secret detection.

`Review and Test Thoroughly`

Conduct code reviews that include security as a checklist item.

Write unit/integration tests for security-related logic.

Use GitLab Merge Request security widgets to catch issues before merging.

`Track and Document Decisions`

If you dismiss a vulnerability in GitLab, provide a justification (e.g., false positive, risk accepted).

Create internal security guidelines and keep them updated.

`Train Developers in Secure Coding`

Run periodic training on OWASP Top 10, language-specific vulnerabilities, etc.

Encourage a security-first culture.

`Automate Where Possible`

Integrate SAST, Dependency Scanning, Secret Detection, and License Compliance into your GitLab CI/CD pipeline.

Enable blocking on merge for unaddressed high-risk vulnerabilities (when feasible).



## TEST

---
