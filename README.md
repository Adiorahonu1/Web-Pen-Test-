# Web Penetration Testing with OWASP ZAP & bWAPP

## 🔍 Overview

This project demonstrates a **web penetration test** conducted on **bWAPP**, a deliberately vulnerable web application, using **OWASP ZAP**. The objective was to identify **SQL Injection (SQLi)** and **Cross-Site Scripting (XSS)** vulnerabilities, analyze their impact, and propose remediation strategies.

✅ **Key Testing Aspects:**

- **Manual Exploration** – Navigating bWAPP to identify potential vulnerabilities.
- **Passive Scanning** – Analyzing requests and responses for security weaknesses.
- **Active Scanning** – Attempting to exploit vulnerabilities detected by ZAP.

## 🛠️ Test Environment

- **Target Application:** bWAPP (Buggy Web Application) – a PHP-based security testing app.
- **Environment:** Docker, running bWAPP as a container.
- **Testing Tool:** OWASP ZAP (Zed Attack Proxy), an open-source security scanner.
- **Testing Methodology:** Manual exploration, passive scanning, and active scanning.

---

## 🚀 Setup Instructions

### 🔹 1. Install and Run bWAPP in Docker

To deploy the vulnerable web application, execute:

```sh
# Pull the bWAPP Docker image
docker pull raesene/bwapp

# Run the container, exposing it on port 80
docker run -d -p 80:80 raesene/bwapp
```

Once running, access bWAPP at: `http://localhost/bwapp`

<img src="asset/Screenshot 2025-04-03 at 09.15.08.png" alt="Docker Test Screenshot" width="600">



### 🔹 2. Configure OWASP ZAP

- Open **OWASP ZAP**.
- Select **Manual Explore** mode.
- Enter the target URL: `http://localhost/bwapp`.
- Browse the application while ZAP logs requests & responses.
- Perform a **Passive Scan** to analyze security weaknesses.
- Execute an **Active Scan** to identify and exploit vulnerabilities.

---

## 🎯 Conducting the Tests


<img src="asset/Screenshot 2025-04-03 at 10.20.31.png" alt="SQL Injection Test Screenshot" width="600">


### 🔥 SQL Injection (SQLi)

SQL Injection is an attack where malicious SQL queries are injected into input fields to manipulate the database.

✅ **Test Steps:**  
1️⃣ Locate a login form or search field that interacts with a database.  
2️⃣ Inject the following SQLi payload:

```sql
'
```
<img src="asset/Screenshot 2025-04-03 at 09.33.00.png" alt="SQL Injection Test Screenshot" width="600">

✅ **Expected Outcome:**  

- If vulnerable, the app may return an **SQL syntax error**.  
- It may also grant **unauthorized access** or reveal database data.  


<img src="asset/Screenshot 2025-04-03 at 10.31.37.png" alt="SQL Injection Test Screenshot" width="600">


---

### 🚨 Cross-Site Scripting (XSS)

XSS occurs when user input isn't properly sanitized, allowing script execution in a victim's browser.

✅ **Test Steps:**  
1️⃣ Find a form field that reflects user input (e.g., comment section, search box).  
2️⃣ Inject the following XSS payload:

```html
</div><script>alert(1);</script><div>
```
<img src="asset/Screenshot 2025-04-03 at 09.39.41.png" alt="XSS Test Screenshot" width="600">

<img src="asset/Screenshot 2025-04-03 at 09.40.08.png" alt="XSS Test Screenshot" width="600">



✅ **Expected Outcome:**  

- If vulnerable, a **JavaScript alert box** will pop up, demonstrating the script execution.  


<img src="asset/Screenshot 2025-04-03 at 09.43.47.png" alt="XSS Test Screenshot" width="600">


---

## 📊 Findings and Analysis

### 🔹 **SQL Injection Findings**

- Vulnerability found in (http://localhost/sqli_1.php?title=%27&action=search)
- Allowed database exposure

### 🔹 **XSS Findings**

- Vulnerability identified in First Name and Last Name fields.
- Potential impact includes **session hijacking or data theft**.

---

## 🛡️ Remediation Recommendations

### ✅ Preventing SQL Injection

- Implement **prepared statements & parameterized queries**.
- Enforce **strict input validation** to reject unexpected characters.
- Limit **database user permissions** to minimize exposure.

### ✅ Preventing XSS

- **Sanitize and encode** user input before rendering it.
- Use **Content Security Policy (CSP)** to restrict script execution.
- Implement security libraries like **DOMPurify** to filter malicious scripts.

---

## 🔚 Conclusion

This penetration test underscores the importance of **secure coding practices**. Developers should implement **proper input validation**, **secure database queries**, and **strict security policies** to mitigate risks associated with **SQL Injection** and **Cross-Site Scripting** attacks.

🔐 *Security is not a one-time effort; it's a continuous process!*

---

📢 *This project was conducted for educational and ethical hacking purposes only.*

