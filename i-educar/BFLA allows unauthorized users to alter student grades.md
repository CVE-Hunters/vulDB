## Broken Function Level Authorization (BFLA) allows unauthorized users to alter student grades

### Summary

A Broken Object Level Authorization (BOLA) vulnerability was identified in the i-educar 2.8 and 2.9 API, allowing any authenticated low-privileged user to access sensitive information from other users by manipulating the `id` parameter in the `pessoa` resource endpoint. 


### Details

The endpoint `/module/Api/pessoa` lacks proper authorization checks to ensure that the authenticated user is only able to access their own data.

By altering the id parameter in the following request, any authenticated user can retrieve information about other users:

`GET /module/Api/pessoa?&oper=get&resource=pessoa&id=1 HTTP/1.1
`

### PoC

1. Authenticate as a non-privileged user (e.g., student, professor).
![image](https://github.com/user-attachments/assets/bc3ac579-2633-4d43-b2e4-4235c56fb4e7)

2. Send the following request targeting id=1 user
```
GET /module/Api/pessoa?&oper=get&resource=pessoa&id=1 HTTP/1.1
Cookie: i_educar_session=VALID_SESSION_COOKIE
```
![image](https://github.com/user-attachments/assets/5aa2edd8-83f9-48f2-ac3b-46cde2a26029)

3. Observe that user data for id=1 is returned, even if the logged-in user is not authorized to access that profile.
![image](https://github.com/user-attachments/assets/4349ff5b-6600-4b26-9643-b0a0ad461fb5)

4. Modify the id parameter to access data from additional users.


### Impact
This vulnerability is a Broken Object Level Authorization (BOLA) issue [(OWASP API Top 10 - 2023, A01)](https://owasp.org/API-Security/editions/2023/en/0xa1-broken-object-level-authorization/), allowing sensitive data exposure. Any authenticated user can access personal information of other users. This can lead to:

- Unauthorized access to sensitive PII
- Violation of data protection laws (e.g., LGPD, GDPR)
- Potential abuse of user data or impersonation
- User enumeration


# Discoverer

[Natan Maia Morette](https://nmmorette.github.io) 

by [CVE-Hunters](https://github.com/Sec-Dojo-Cyber-House/cve-hunters)