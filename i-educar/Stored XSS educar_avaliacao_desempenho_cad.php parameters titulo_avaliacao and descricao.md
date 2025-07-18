# Cross-Site Scripting (XSS) Stored endpoint `/intranet/educar_avaliacao_desempenho_cad.php` parameters `titulo_avaliacao` and `descricao`

---

## Summary

A Stored Cross-Site Scripting (XSS) vulnerability was identified in the `/intranet/educar_avaliacao_desempenho_cad.php` endpoint of the _i-educar_ application. This vulnerability allows attackers to inject malicious scripts into the `titulo_avaliacao` and `descricao` parameters. The injected scripts are stored on the server and executed automatically whenever the affected page is accessed by users, posing a significant security risk.

---

## Details

**Vulnerable Endpoint:** `POST /intranet/educar_avaliacao_desempenho_cad.php`  
**Parameters:** `titulo_avaliacao`, `descricao`

The application fails to properly validate and sanitize user input in the `titulo_avaliacao` and `descricao` parameters. This allows attackers to inject malicious scripts, which are stored in the backend and executed in the browser of any user viewing the stored content.

---

## PoC

**Encoded Payload:**

`%3Cscript%3Ealert%28%27PoC-XXS51%27%29%3C%2Fscript%3E`

**Decoded Payload:**

`<script>alert('PoC-XXS51')</script>`

<img width="737" height="887" alt="image" src="https://github.com/user-attachments/assets/7a3d215f-8a16-4314-8acc-68c7ff2dfb36" />


The payload was submitted via the `titulo_avaliacao` and `descricao` fields and stored successfully. When the page displaying these values is accessed, the script is executed in the context of the user's browser session, confirming the presence of a stored XSS vulnerability.

---

## Impact

Stored XSS attacks can have severe consequences, including:

- **Stealing session cookies:** Attackers can hijack user sessions and perform actions on their behalf
    
- **Delivering malware:** Users can be tricked into downloading and executing malicious software
    
- **Hijacking browsers:** Full control over the user’s browser through JavaScript execution
    
- **Credential theft:** Capturing usernames, passwords, and other sensitive information
    
- **Exposing sensitive data:** Accessing data stored in the application or browser
    
- **Website defacement:** Altering the content of web pages viewed by users
    
- **User redirection:** Redirecting victims to phishing or malicious websites
    
- **Damaging business reputation:** Loss of trust if users are affected by attacks originating from the application

## Discoverer

[Marcelo Queiroz](www.linkedin.com/in/marceloqueirozjr) 

by [CVE-Hunters](https://github.com/Sec-Dojo-Cyber-House/cve-hunters)
