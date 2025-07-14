**Cross-Site Scripting (XSS) Reflected endpoint** `/admin/pages/[page]`, **parameter** `data[header][content][items]`, **located in the "Blog Config" tab.**

---

## Summary

A Reflected Cross-Site Scripting (XSS) vulnerability was identified in the `/admin/pages/[page]` endpoint of the _Grav_ application. This vulnerability allows attackers to inject malicious scripts into the `data[header][content][items]` parameter.

---

## Details

**Vulnerable Endpoint:** `GET /admin/pages/[page]`  
**Parameter:** `data[header][content][items]`

The application fails to properly validate and sanitize user input in the `data[header][content][items]` parameter. As a result, attackers can craft a malicious URL with an XSS payload. When this URL is accessed, the injected script is reflected back in the HTTP response and executed within the context of the victim's browser session.

---

## PoC

**Payload:**

`"><ImG sRc=x OnErRoR=alert('XSS-PoC3')>`

### Steps to Reproduce:

1. Log in to the _Grav_ Admin Panel and navigate to **Pages**.
    
2. Create a new page or edit an existing one.
    
3. In the **Advanced > Blog Config > Items** field (which maps to `data[header][content][items]`), insert the payload above.


figura1

4. Save the page.
     
5. The malicious payload is reflected and rendered by the application without proper sanitization. The JavaScript code is immediately executed in the browser.

figura2

---

## Impact

Reflected cross-site scripting (XSS) attacks can have serious consequences, including:

- **User actions:** Attackers can perform actions on behalf of the user
    
- **Data theft:** Sensitive information such as session cookies can be stolen
    
- **Account compromise:** Attackers may impersonate legitimate users
    
- **Malicious code execution:** Arbitrary JavaScript code can run in the user’s browser
    
- **Website defacement or misinformation:** Malicious output may be injected visually
    
- **User redirection:** Victims may be redirected to phishing or malicious websites

## Discoverer

[Marcelo Queiroz](www.linkedin.com/in/marceloqueirozjr) 

by [CVE-Hunters](https://github.com/Sec-Dojo-Cyber-House/cve-hunters)