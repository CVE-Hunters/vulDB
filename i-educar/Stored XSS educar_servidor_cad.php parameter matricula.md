# Cross-Site Scripting (XSS) Stored endpoint `/intranet/educar_servidor_cad.php` parameter `matricula`

---

## Summary

A Stored Cross-Site Scripting (XSS) vulnerability was identified in the `/intranet/educar_servidor_cad.php` endpoint of the _i-educar_ application. This vulnerability allows attackers to inject malicious scripts into the `matricula` parameter. The injected script is stored on the server and executed automatically whenever the affected page is accessed by users, posing a significant security risk.

---

## Details

**Vulnerable Endpoint:** `POST /intranet/educar_servidor_cad.php`  
**Parameter:** `matricula`

The application does not properly validate or sanitize user input in the `matricula` parameter. As a result, an attacker can submit a specially crafted payload that is saved in the system and later executed in the browser of any user who views the content.

---

## PoC

**Encoded Payload:**

`%22%3E%3Csvg+onload%3Dalert%2812%29%3E`

**Decoded Payload:**

`"><svg onload=alert(12)>`

![[Pasted image 20250704153044.png]]

On /intranet/educar_servidor_det.php?cod_servidor=28915&ref_cod_instituicao=1 page click on "Editar" button.
![[Pasted image 20250704153406.png]]

![[Pasted image 20250704153423.png]]

This payload was submitted through the `matricula` field and successfully stored. Upon accessing the affected content, the JavaScript executes immediately in the context of the victim’s browser.

---

## Impact

Stored XSS vulnerabilities can lead to a range of serious consequences, including:

- **Session hijacking:** Stealing cookies or tokens to impersonate users
    
- **Malware delivery:** Inserting scripts that download malicious content
    
- **Credential theft:** Capturing usernames and passwords through fake forms
    
- **Sensitive data exposure:** Accessing protected application data
    
- **Browser takeover:** Running arbitrary commands within the user’s browser session
    
- **Phishing attacks:** Redirecting users to malicious or fake login pages
    
- **Website defacement:** Altering visible content on the platform
    
- **Reputational damage:** Undermining trust in the affected platform

## Discoverer

[Marcelo Queiroz](www.linkedin.com/in/marceloqueirozjr) 

by [CVE-Hunters](https://github.com/Sec-Dojo-Cyber-House/cve-hunters)