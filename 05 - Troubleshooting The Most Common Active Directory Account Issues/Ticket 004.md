## Scenario
User cannot log in to the domain, and receives *The user's account has expired* message.
<img width="1273" height="761" alt="image" src="https://github.com/user-attachments/assets/742d24a4-f53e-4546-901b-27d8ed2af5f0" />

---
## 1 - Verify the Account Status and Resolve the Issue

1. On `DC01` Open *Server Manager* → *Tools* → *Active Directory Users and Computers* → `corp.test`.
2. Right-click `corp.test` → **Find...**.
3. Enter the affected user name → **Find Now**.
4. Right-click the user → **Properties** → **Account**.
5. In the *Account expires* section change the expiration day or set it to **Never**.

---
## 2 - Test the Resolution

1. On `WIN11-01`, attempt to sign in using the affected user's domain account.
2. Confirm that the user can successfully authenticate to the domain.
3. Verify that the *The user's account has expired* message no longer appears.
4. Confirm that the user's desktop loads successfully.
5. Verify that the user can access domain resources, such as shared folders or network drives.
