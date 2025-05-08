## What is DAST ?
==========================

DAST stands for Dynamic Application Security Testing.

It is a type of black-box security testing that analyzes web applications in their running state to find security vulnerabilities.

Unlike static testing (which inspects source code), DAST tests the application from the outside.



## Configuring DAST with GitLab
======================================

Configuring DAST with GitLab involves setting up GitLab CI/CD to automatically run security scans against your running application. 

GitLab provides a built-in DAST template that makes this relatively straightforward.

#### Prerequisites

GitLab Premium or Ultimate (DAST is available in higher tiers).

A web application deployed to a test/staging environment accessible from the GitLab Runner.

The application must be running when the DAST job executes.


`Step-by-Step`

Add a .gitlab-ci.yml File or Modify It

```
stages:
  - test

dast:
  stage: test
  image: registry.gitlab.com/gitlab-org/security-products/dast
  script:
    - /analyze
  variables:
    DAST_WEBSITE: "https://your-staging-site.com"  # Replace with your app's URL
    DAST_FULL_SCAN_ENABLED: "true"  # Optional, enables a full scan

```

Push your changes to GitLab, and the pipeline will start. The DAST job will run and scan the live app.


Once the pipeline finishes :-

Navigate to Security > Vulnerability Report in your GitLab project.

You'll see a list of issues found by DAST with severity and remediation advice.


## Analyzing DAST results
================================


Analyzing the results of a DAST scan in GitLab is an essential part of identifying vulnerabilities and understanding potential security risks in your web application. 

#### Understanding DAST Results in GitLab CI/CD

Once the DAST job completes, GitLab processes the results and makes them available in the Security Dashboard. 

The results typically include :-

`Vulnerabilities` Found vulnerabilities like SQL injection, cross-site scripting (XSS), command injection, etc.

`Risk Level` The severity of each vulnerability (e.g., Low, Medium, High, Critical).

`URLs & Endpoints` The specific URLs or endpoints where vulnerabilities were detected.

`Description` A detailed explanation of the vulnerability, how it works, and possible attack vectors.

`Remediation Advice` Suggested ways to fix the issues (e.g., input validation, parameterized queries for SQL injection).

#### Accessing DAST Results in GitLab

`Pipeline View` 

After the DAST job completes in the pipeline, you can view the results directly in the pipeline details. 

If you click on the DAST job, you’ll see a summary of the vulnerabilities.

`Security Dashboard`

Go to your GitLab project.

In the left sidebar, navigate to Security > DAST to see a summary of the vulnerabilities found during the scan.

You can filter the results by severity (Critical, High, Medium, Low).

The vulnerabilities will be categorized into different types, such as:

  - Injection (e.g., SQL injection)
  - Cross-Site Scripting (XSS)
  - Broken Access Control
  - Information Disclosure

`Vulnerability Details`

Clicking on each vulnerability will provide detailed information, including:

  - Type of vulnerability (e.g., SQL injection, XSS).
  - Location (URL or endpoint).
  - Risk level.
  - Steps to reproduce the issue (helpful for developers to replicate and debug).
  - GitLab may provide guidance on how to resolve the vulnerability.


#### Analyzing Vulnerability Severity

Each vulnerability found by DAST will have a severity rating (Critical, High, Medium, Low). 

The goal is to prioritize addressing the most severe vulnerabilities first.

`Critical` Issues that can be exploited remotely and cause significant harm, such as Remote Code Execution (RCE) or data breaches. These need to be fixed immediately.

`High` Serious vulnerabilities that should be fixed soon, but may not be easily exploitable.

`Medium` Moderate risk vulnerabilities, which are less likely to be exploited but should still be addressed.

`Low` Minor vulnerabilities, such as low-impact issues or potential minor information disclosure.

#### Exporting and Integrating Results

GitLab allows you to export DAST results, which you can use for deeper analysis, integration into other tools, or record-keeping purposes.

`Export Results` You can export the results as a JSON or CSV file from the GitLab interface. 

`Security Reports in Merge Requests` 

GitLab can automatically add security reports to merge requests when a scan is run. 

This allows your team to review the results and ensure security vulnerabilities are addressed before merging the code.

#### Remediation Process

Once vulnerabilities are identified, here’s how to approach fixing them :-

`Fix Critical Vulnerabilities` These should be patched immediately, and the associated code or deployment should be updated quickly.

`Fix High Vulnerabilities` Address these as soon as possible. Some might require more complex fixes or testing, but they should still be prioritized.

`Fix Medium & Low Vulnerabilities` These can be fixed over time, but they should not be ignored. If a vulnerability can potentially be exploited in the future, address it sooner.

#### Re-Scanning After Fixes

After addressing vulnerabilities, it's crucial to rerun the DAST scan to ensure that the vulnerabilities have been resolved and no new issues have been introduced. 

This can be done by re-running the pipeline or manually triggering a new DAST scan.

#### Continuous Monitoring

DAST is a continuous process, and it's important to run DAST scans regularly. 

Incorporating DAST into your CI/CD pipeline ensures that new vulnerabilities are detected as soon as new changes are made to the application. 

You can configure the pipeline to run DAST scans after each deployment or on a schedule (e.g., daily or weekly).

#### Integrating with Other Security Tools

GitLab integrates with other security tools, such as SAST (Static Application Security Testing), Container Scanning, and Dependency Scanning. 

Combining these tools with DAST helps build a comprehensive security strategy. 

By analyzing both static (SAST) and dynamic (DAST) security data, you can get a more complete picture of your application's security.

##### Example of Viewing Vulnerabilities in the GitLab UI

`Vulnerability Overview` GitLab will show an overview of vulnerabilities discovered, categorized by type and severity.

`Detailed Results` Clicking on a specific vulnerability will open a detailed page with information like :-

  - The URL/path of the affected endpoint.
  - The type of vulnerability (e.g., SQL injection, XSS).
  - The risk level (e.g., Critical, High).
  - Links to suggested remediation steps.
    

### Summary of the DAST Analysis Process
------------------------------------------------

  - Review the results from the DAST scan in GitLab’s Security Dashboard.
  - Prioritize vulnerabilities based on their severity (Critical, High, Medium, Low).
  - Take action on the vulnerabilities by applying fixes, such as improving input validation or addressing broken access control.
  - Re-run the DAST scan after fixes to ensure vulnerabilities are resolved.
  - Integrate DAST into the CI/CD pipeline for continuous monitoring of application security.





## TEST


--------------





