# Web Application Security Assessment Report

## 1️⃣ Introduction

| Field | Value |
|-------|--------|
| **Tester(s):** | Gökhan Arifoglu |
| **Purpose:** | Identify and assess high-risk vulnerabilities in the target web application, primarily focusing on the /register endpoint. |
| **Scope – Tested components:** | http://localhost:8000/, /register endpoint, static files (footer.js, index.js, tailwind.css) |
| **Scope – Exclusions:** | Underlying Operating System, Network Infrastructure, External Services |
| **Test approach:** | Black-box |
| **Test environment & dates – Start:** | 2025-11-26 |
| **Test environment & dates – End:** | 2025-11-26 |
| **Test environment details:** | Target is running on http://localhost:8000/. |
| **Assumptions & constraints:** | Limited to the endpoints discovered by the ZAP baseline scan; no authenticated testing was performed. |


---

## 2️⃣ Executive Summary

| Field | Value |
|--------|--------|
| **Short summary** | The initial security scan identified two Critical vulnerabilities, SQL Injection and Path Traversal on the registration endpoint, indicating severe risk to the application's data and system integrity. Multiple medium severity security misconfigurations, such as missing protective headers and CSRF tokens, were also found. |
| **Top 5 immediate actions:** |  
| **1.** | Immediately implement parameterized queries or stored procedures on all database interactions to mitigate SQL Injection on inputs like username.  
| **2.** | Enforce stringent input validation and utilize path canonicalization functions to prevent Path Traversal.  
| **3.** | Add unique, cryptographically secure Anti-CSRF Tokens to the /register POST form to prevent Cross-Site Request Forgery.  
| **4.** | Configure the web server to set a robust Content Security Policy (CSP) header to mitigate XSS and data injection attacks.  
| **5.** | Implement the `X-Frame-Options: DENY` or `Content-Security-Policy: frame-ancestors 'none'` directive to prevent Clickjacking. |


---

## 3️⃣ Severity scale & definitions

| Severity Level | Description | Recommended Action |
|----------------|-------------|--------------------|
| 🔴 **High** | A serious vulnerability that can lead to full system compromise or data breach (e.g., SQL Injection, Remote Code Execution). | Immediate fix required |
| 🟠 **Medium** | A significant issue that may require specific conditions or user interaction (e.g., XSS, CSRF). | Fix ASAP |
| 🟡 **Low** | A minor issue or configuration weakness (e.g., server version disclosure). | Fix soon |
| 🔵 **Info** | No direct risk, but useful for system hardening (e.g., missing security headers). | Monitor and fix in maintenance |


---

## 4️⃣ Findings

| ID | Severity | Finding | Description | Evidence / Proof |
|-----|----------|----------|--------------|---------------------|
| **F-01** | 🔴 High | SQL Injection in registration | The /register endpoint's username parameter is vulnerable to SQL injection, as evidenced by a 500 Internal Server Error when a basic injection string (') was used. | URL: http://localhost:8000/register, Parameter: username, Evidence: `HTTP/1.1 500 Internal Server Error` |
| **F-02** | 🔴 High | Path Traversal on /register | An input field (username) on the /register endpoint is susceptible to Path Traversal, which could allow an attacker to access files outside the web document root. | URL: http://localhost:8000/register, Parameter: username, Attack: register (ZAP's test string) |
| **F-03** | 🟠 Medium | Absence of Anti-CSRF Tokens | The form on /register using POST method is missing an Anti-CSRF token, making the registration action vulnerable to CSRF attacks. | URL: http://localhost:8000/register, Evidence: `<form action="/register" method="POST">` with no CSRF token found. |
| **F-04** | 🟠 Medium | Missing Anti-clickjacking Header | The application responses do not include `X-Frame-Options` or `Content-Security-Policy: frame-ancestors`, which is required to prevent Clickjacking attacks. | URL: http://localhost:8000/, http://localhost:8000/register, Parameter: X-Frame-Options missing. |
| **F-05** | 🟠 Medium | Missing Content Security Policy (CSP) | The Content Security Policy (CSP) header is not set. This increases the risk and impact of XSS and data injection attacks. | URL: http://localhost:8000/, http://localhost:8000/register, CSP Header Not Set. |
| **F-06** | 🟠 Medium | Format String Error | The username parameter is vulnerable to format string attacks, which could potentially lead to information disclosure or denial of service. | URL: http://localhost:8000/register, Parameter: username, Attack: Format string payload, Evidence: Connection closed on /%s. |
| **F-07** | 🟡 Low | X-Content-Type-Options Header Missing | The X-Content-Type-Options header is not set to 'nosniff', which could allow browsers to perform MIME-sniffing on responses. | URL: http://localhost:8000/, http://localhost:8000/register, static files, Parameter: X-Content-Type-Options missing. |
| **F-08** | 🔵 Info | User Agent Fuzzer | The application was tested with different User-Agent strings to check for behavioral differences. | URL: http://localhost:8000/register, Instances: 12 different User-Agent strings tested. |


---


## 5️⃣ OWASP ZAP Test Report (Attachment)

**Purpose:**  
Attach or link your OWASP ZAP scan results (Markdown format preferred).

👉 [Click here to open the full OWASP ZAP Report](ZAP-Report-.md)
