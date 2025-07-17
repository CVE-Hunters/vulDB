### Summary

A Reflected Cross-Site Scripting (XSS) vulnerability was identified in the `educar_aluno_lst.php` endpoint of the i-educar application. This vulnerability allows attackers to inject malicious scripts in the `ref_cod_matricula` parameter.

### Details
Vulnerable Endpoint:`educar_aluno_lst.php`
Parameter: `ref_cod_matricula`

The application fails to validate and sanitize user inputs in the `ref_cod_matricula` parameter. This lack of validation permits the injection of malicious payloads, which are reflected back to the user's browser in the server's response and executed within the context of the victim's browser.

### PoC

Insert the payload `"><img%20src=x%20onerror=alert(%27CVE-Hunters%27)>` in the field ` ref_cod_matricula`

![image](https://drive.google.com/file/d/1nBynPM5vzRlD1HDJVy5CAuOODFrTsaxq/view?usp=sharing)

Full Payload: `https://comunidade.ieducar.com.br/intranet/educar_aluno_lst.php?ref_cod_matricula="><img%20src=x%20onerror=alert(%27CVE-Hunters%27)>`

### Impact

- User actions: Attackers can perform any action the user can, such as viewing, modifying, or initiating interactions with other users
- Data theft: Attackers can exfiltrate data or install malware on the user's machine
- Account compromise: Attackers can manipulate or steal cookies, or compromise confidential information
- Malicious code: Attackers can execute malicious code on the user's system
- Business reputation damage: Attackers can deface a corporate website or spread misinformation
- Misdirection: Attackers can change the instructions given to users, which can be dangerous if the target is a government website or provides vital resources

# Discoverer

[Natan Maia Morette](https://nmmorette.github.io) 

by [CVE-Hunters](https://github.com/Sec-Dojo-Cyber-House/cve-hunters)

