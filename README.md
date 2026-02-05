# real-world-xss-assessment

**Real-World Cross-Site Scripting (XSS) Vulnerability Assessment**

**(Reflected, DOM-Based & Stored XSS)**

**Overview**

This repository documents an **authorized security assessment** conducted on a live PHP-based web application to identify Cross-Site Scripting (XSS) vulnerabilities. During testing, three types of XSS vulnerabilities were discovered and validated:

* Reflected XSS
* DOM-Based XSS
* Stored XSS
All sensitive information such as domain names, IP addresses, and organization details have been **intentionally redacted** to comply with **responsible disclosure and ethical hacking standards**.
**Target (Redacted)**
https://target-site.com/home.php?id=VALUE
The application uses the `id` parameter to load dynamic content, which was found to be vulnerable to JavaScript injection.
**Vulnerabilities Identified**

| Vulnerability Type | Status    |
| ------------------ | --------- |
| Reflected XSS      | Confirmed |
| DOM-Based XSS      | Confirmed |
| Stored XSS         | Confirmed |

This combination represents a **critical security risk**.
**Testing Methodology**
The vulnerability was identified by testing user-controlled URL parameters with safe proof-of-concept payloads.
**Reflected XSS Test**
**Payload used**:
<script>alert("You are hacked")</script>
**Anonymized example**
https://target-site.com/home.php?id=london<script>alert("You are hacked")</script>
Result:
The browser executed the JavaScript and displayed an alert, confirming **Reflected XSS**.
 DOM-Based XSS Test
**Payload**:
<body onload=alert('hacked')>
Result:
The script executed through client-side JavaScript processing of the URL parameter, confirming **DOM-Based XSS**.
**stored XSS Test**
The same payload was submitted into a parameter that was later rendered again on the page.
Payload:
**<body onload=alert('hacked')>**

Result:
The payload executed again when the page was loaded, confirming **Stored XSS**.
This means any visitor to the affected page would unknowingly execute the attacker’s JavaScript.

**What is Cross-Site Scripting (XSS)**

**Reflected XSS**

Occurs when user input is immediately returned by the server in the response without proper sanitization, allowing attackers to execute scripts via crafted URLs.

**DOM-Based XSS**

Occurs when client-side JavaScript reads data from the URL or page and injects it into the DOM insecurely, allowing JavaScript execution without server-side involvement.

**Stored XSS**
Occurs when malicious input is saved in the application’s database and executed whenever a user loads the affected page. This is the most dangerous form of XSS.

**Impact**
Successful exploitation of these vulnerabilities could allow attackers to:

* Steal session cookies
* Hijack authenticated user accounts
* Perform phishing attacks
* Modify website content
* Redirect users to malicious pages

**Severity: Critical (OWASP Top-10: A03 – Injection)**
**Recommended Mitigations**

* Implement strict **input validation** on all user-supplied data
* Apply **output encoding** before rendering data in HTML
* Avoid unsafe JavaScript functions such as `innerHTML`, `document.write()`, and `eval()`
* Use a strong **Content Security Policy (CSP)**
* Adopt secure coding frameworks that escape output by default

**Legal & Ethical Notice**

This security testing was conducted under **authorized conditions**.
No real domain names, IP addresses, or sensitive data are disclosed in this repository.
This project is shared for **educational and professional cybersecurity research purposes only**.
