Cross-Site Scripting (XSS) Stored endpoint `data_source_edit.shtm` parameter `name`

---

## Summary

A Stored Cross-Site Scripting (XSS) vulnerability was identified in the `data_source_edit.shtm` endpoint of the _SCADA-LTS_ application. This vulnerability allows attackers to inject malicious scripts into the `name` parameter. The injected payload is stored on the server and executed automatically in the browser of any user who accesses the affected data source entry, creating a persistent attack vector.

---

## Details

**Vulnerable Endpoint:** `POST /data_source_edit.shtm`  
**Parameter:** `name`

The application does not properly validate or sanitize input in the `name` field. As a result, an attacker can inject JavaScript code, which is stored in the system and later rendered in the application’s interface, leading to automatic execution in the user's browser.

---

## PoC

**Payload:**

`"><img src=x onerror=alert('XSS-PoC3')>`

### Steps to Reproduce:

1. Log in to the _SCADA-LTS_ application with an account that has permission to create or edit data sources.
    
2. Navigate to the **Data Sources** section and select **Add Data Source** or edit an existing entry.
    
3. In the **Name** field, insert the payload above:
          
    `"><img src=x onerror=alert('XSS-PoC3')>`
    
4. Fill in any other required fields and click **Save**.

<img width="710" height="431" alt="Pasted image 20250722175722" src="https://github.com/user-attachments/assets/5a46a084-3b8d-47b1-9606-2a08767281cc" />


5. The stored payload is executed immediately in the browser, confirming the Stored XSS vulnerability.
    
<img width="835" height="436" alt="Pasted image 20250722175822" src="https://github.com/user-attachments/assets/c88fdd69-d610-4252-a808-722adb69fd30" />

    

---

## Impact

Stored XSS attacks can lead to severe consequences, including:

- **Session hijacking:** Stealing cookies or authentication tokens to impersonate users
    
- **Credential theft:** Capturing usernames and passwords through malicious scripts
    
- **Malware delivery:** Distributing harmful code to application users
    
- **Privilege escalation:** Compromising higher-privilege accounts via persistent scripts
    
- **Data manipulation or defacement:** Altering displayed content in the application
    
- **Reputation damage:** Eroding trust among system users and stakeholders
