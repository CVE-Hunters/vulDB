## Broken Function Level Authorization (BFLA) allows unauthorized users to alter student grades

### Summary
An API endpoint in i-Educar 2.9.0 is vulnerable to Broken Function Level Authorization (BFLA). An unauthenticated or unauthorized user is able to modify student grades by directly accessing the `/module/Api/Diario `endpoint, bypassing permission controls. This leads to severe integrity issues, where anyone with access to the API format can tamper with academic records.

### Details

The endpoint `/module/Api/Diario ` does not enforce proper authorization checks to validate whether the calling user has the right to alter student grades. Even a user without any profile or assigned permissions can successfully submit a request and change the grades of students in the system.

There is no validation of session roles or associated permissions before executing sensitive academic actions.

### PoC
1 - Create a new user with no privileges.
![image](https://github.com/user-attachments/assets/44b8aa71-ad6c-4e28-af99-0a517cfa5d85)

2 - Prepare a request to the `/module/Api/Diario `endpoint with the data to submit a student grade, using the low privillege user cookie then send the request.

![image](https://github.com/user-attachments/assets/3b84ea52-e492-4a01-919e-9d86792e4353)




### Impact
This is a Broken Function Level Authorization (BFLA) vulnerability, as categorized by OWASP API Security Top 10 (2023) - API4. The consequences include:

- Tampering with academic data without authorization.
- Loss of data integrity in school records.
- Potential legal and reputational damage for educational institutions.

# Discoverer

[Natan Maia Morette](https://nmmorette.github.io) 

by [CVE-Hunters](https://github.com/Sec-Dojo-Cyber-House/cve-hunters)

