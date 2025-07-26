\## Reflected XSS (GET) – bWAPP



Vulnerable Application



\- \*\*Application:\*\* bWAPP (Buggy Web Application)

\- \*\*Module:\*\* Reflected XSS (GET)

\- \*\*URL:\*\* `http://<bee-box-ip>/bWAPP/xss\_get.php`



Objective



To identify and exploit a reflected XSS vulnerability in a GET-based input scenario where the application fails to sanitize user-supplied data before rendering it in the response.



Test Environment



\- \*\*Attacker Machine:\*\* Kali Linux

\- \*\*Target Machine:\*\* Bee-box (bWAPP)

\- \*\*Browser:\*\* Firefox

\- \*\*Tools Used:\*\* Manual Testing



Steps to Reproduce



1\. \*\*Login to bWAPP\*\*

&nbsp;  - URL: `http://<bee-box-ip>/bWAPP/`

&nbsp;  - Username: `bee`

&nbsp;  - Password: `bug`



2\. \*\*Select the XSS Module\*\*

&nbsp;  - Vulnerability: `XSS - Reflected (GET)`

&nbsp;  - Click: `Hack`



3\. \*\*Submit Payload via Input Fields\*\*

&nbsp;  - First Name: `<script>alert(1)</script>`

&nbsp;  - Last Name: `tj`

&nbsp;  - Click: `Submit`



4\. \*\*Observe Output\*\*

&nbsp;  - A JavaScript alert box appears with message `1`



Payloads Used



Basic Script Tag:

```html

<script>alert(1)</script>



URL-Based Injection:



http://<bee-box-ip>/bWAPP/xss\_get.php?firstname=<script>alert(1)<%2Fscript>\&lastname=tj\&form=submit



Alternate Payloads (for filter bypass testing):



<img src=x onerror=alert(1)>

<svg/onload=alert(1)>

<body onload=alert(1)>



Result



Alert box with 1 was successfully triggered.

Confirms vulnerability to Reflected Cross-Site Scripting (GET method).



Mitigation



* Sanitize user input using functions like htmlspecialchars() in PHP.
* Apply proper output encoding for HTML.
* Implement Content Security Policy (CSP).
* Avoid reflecting unsanitized input in responses.

Reflected XSS (POST) – bWAPP

Vulnerable Application
- **Application:** bWAPP (Buggy Web Application)
- **Module:** Reflected XSS (POST)
- **URL:** `http://<bee-box-ip>/bWAPP/xss_post.php`

---

Objective
To exploit a reflected XSS vulnerability where input submitted via the HTTP POST method is reflected back in the server response without sanitization.

---

Test Environment
- **Attacker Machine:** Kali Linux
- **Target Machine:** Bee-box (bWAPP)
- **Browser:** Firefox
- **Tools Used:** Manual Testing (Burp Suite optional)

---

Steps to Reproduce

1. **Login to bWAPP**
   - URL: `http://<bee-box-ip>/bWAPP/`
   - Username: `bee`
   - Password: `bug`

2. **Select Module**
   - Select: `XSS - Reflected (POST)`
   - Click: `Hack`

3. **Submit Malicious Input**
   - First Name: `<script>alert(1)</script>`
   - Last Name: `tj`
   - Click: `Submit`

4. **Observe Output**
   - A popup alert with `1` appears, confirming XSS execution

---

Payloads Used

```html
<script>alert(1)</script>

Result

JavaScript executed
Confirms Reflected XSS via POST

Mitigation

Sanitize user input using functions like htmlspecialchars()
Encode output before displaying it in HTML
Use Content Security Policy (CSP)
Avoid reflecting unsanitized input
