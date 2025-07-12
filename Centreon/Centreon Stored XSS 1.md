## Cross-Site Scripting (XSS) Stored endpoint `/centreon/main.get.php?p=60102` parameter '`hg_name`'

---

#### Summary

A Stored Cross-Site Scripting (XSS) vulnerability was identified in the `/centreon/main.get.php?p=60102` endpoint of the Centreon application. This vulnerability allows attackers to inject malicious scripts into the `hg_name` parameter. The injected scripts are stored on the server and executed automatically whenever the affected page is accessed by users, posing a significant security risk.

---

## Details

- **Vulnerable Endpoint:** `POST /centreon/main.get.php?p=60102`
    
- **Parameter:** `hg_name`
    

The application fails to properly validate and sanitize user input in the `hg_name` parameter. This lack of validation allows attackers to inject malicious scripts, which are then stored on the server. Whenever the affected page is accessed, the malicious payload is executed in the victim's browser, potentially compromising the user's data and system.

---

## PoC

**Payload:**

`><svg/onload=alert(1)>`

### Steps to Reproduce:

- Log in to the _Centreon_ application using an account with permissions to add hosts groups.
    
- Navigate to **Configuration > Hosts > Hosts Groups** and click on one of the groups.

<img width="921" height="553" alt="image" src="https://github.com/user-attachments/assets/11dd383e-90a9-4fa1-b831-849ccd4ab138" />


- In the **Name** field (which maps to the `hg_name` parameter), insert the following payload:    
    
    `><svg/onload=alert(1)>`
    
- Click **Save**.
  

<img width="1906" height="520" alt="image" src="https://github.com/user-attachments/assets/8543bcd6-e8c1-451d-bf81-f4f5cd4794a2" />


- After submission, the XSS payload is stored and executed in the browser, confirming the presence of the vulnerability.
  

<img width="796" height="416" alt="image" src="https://github.com/user-attachments/assets/f81b4133-10a4-4b3c-8227-b49082a3677c" />


This is the request:


<img width="665" height="466" alt="image" src="https://github.com/user-attachments/assets/5811be6b-e4f7-49fb-9e7b-4710afa85ccd" />


---

#### Impact

- **Stealing session cookies:** Attackers can use stolen session cookies to hijack a user's session and perform actions on their behalf.
    
- **Downloading malware:** Attackers can trick users into downloading and installing malware on their computers.
    
- **Hijacking browsers:** Attackers can hijack a user's browser or deliver browser-based exploits.
    
- **Stealing credentials:** Attackers can steal a user's credentials.
    
- **Obtaining sensitive information:** Attackers can obtain sensitive information stored in a user's account or in their browser.
    
- **Defacing websites:** Attackers can deface a website by altering its content.
    
- **Misdirecting users:** Attackers can change the instructions given to users who visit the target website, misdirecting their behavior.
    
- **Damaging a business's reputation:** Attackers can damage a business's image or spread misinformation by defacing a corporate website.


## Discoverer

[Marcelo Queiroz](www.linkedin.com/in/marceloqueirozjr) 

by [CVE-Hunters](https://github.com/Sec-Dojo-Cyber-House/cve-hunters)
