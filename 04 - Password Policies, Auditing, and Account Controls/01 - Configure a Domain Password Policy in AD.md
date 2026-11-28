## Purpose

Configure and Enforce a consistent password policy for all domain accounts.

> [!NOTE]
> Account policies (password and lockout) only apply to domain accounts when set in a GPO linked at the **domain root**. 
> If you set them on an OU, they only affect local accounts of computers in that OU.

---
## 1 - Configure the Default Domain Policy

1. Open *Server Manager* → *Tools* → *Group Policy Management*.
2. Navigate to: `Forest: corp.test` → `Domains` → `corp.test`.
3. Right-click *Default Domain Policy*.
4. Right-click → **Edit**.
5. Navigate to: *Computer Configuration* → *Policies* → *Windows Settings* → *Security Settings* → *Account Policies* → *Password Policy*.
6. Double-click *Password Policy*.
7. Configure:

| Setting                                     | Value    | Why                                                               |
| ------------------------------------------- | -------- | ----------------------------------------------------------------- |
| Minimum password length                     | 14       | Encourages longer and stronger passwords.                         |
| Password must meet complexity requirements  | Enabled  | Enforces password complexity requirements.                        |
| Enforce password history                    | 24       | Prevents immediate reuse of previous passwords.                   |
| Minimum password age                        | 1        | Stops users from cycling through history to reuse an old password |
| Maximum password age                        | 90       | Enforces periodic password changes for applicable accounts.       |
| Store passwords using reversible encryption | Disabled | Prevents insecure, reversible password storage.                   |
### Verification

1. On `WIN11-01`, sign in as `CORP\mjohnson`.
2. Press **Ctrl + Alt + Delete** → **Change a password**.
3. Attempt to set a password that does not meet the domain password policy requirements.
4. Verify that Windows rejects the password.
5. Set a password that meets the domain password policy requirements.
6. Verify that the password change succeeds.

---
## 2 - Configure the Account Lockout Policy

1. Navigate to: *Computer Configuration* → *Policies* → *Windows Settings* → *Security Settings* → *Account Policies* → *Account Lockout Policy*.
2. Double-click *Account Lockout Policy*.
3. Configure:

| Setting                             | Value                    |
| ----------------------------------- | ------------------------ |
| Account lockout threshold           | 5 invalid logon attempts |
| Account lockout duration            | 15 minutes               |
| Reset account lockout counter after | 15 minutes               |

### Verification

1. Log in to `WIN11-01` using a domain account.
2. At the Windows sign-in screen, enter an incorrect password five times for a domain user.
3. Verify that the account is locked.
4. On `DC01`, open *Active Directory Users and Computers*.
5. Navigate to the user account.
6. Open **Properties** → `Account`.
7. Verify that the account is locked.
8. Click **Unlock account** and click **OK**.


