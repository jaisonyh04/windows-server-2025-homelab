## Purpose

Enforce a consistent password policy for all domain accounts.

> [!NOTE]
> Account policies (password and lockout) only apply to domain accounts when set in a GPO linked at the **domain root**. 
> If you set them on an OU, they only affect local accounts of computers in that OU.

---

## 1 - Open the Default Domain Policy

1. Open *Server Manager* → *Tools* → *Group Policy Management*.
2. Navigate to: `Forest: corp.test` → *Domains* → `corp.test` → *Default Domain Policy*.
3. Right-click *Default Domain Policy*.
4. Right-click → **Edit**.
5. Navigate to: Computer Configuration → Policies → Windows Settings → Security Settings → Account Policies → **Password Policy**.

---

## 2 - Configure the GPO

| Setting                                     | Value         | Why                                                               |
| ------------------------------------------- | ------------- | ----------------------------------------------------------------- |
| Minimum password length                     | 14 characters | Matches Microsoft’s Windows Server 2025 security baseline         |
| Password must meet complexity requirements  | Enabled       | Baseline default                                                  |
| Enforce password history                    | 24            | Prevents password reuse                                           |
| Minimum password age                        | 1 day         | Stops users from cycling through history to reuse an old password |
| Maximum password age                        | 90            |                                                                   |
| Store passwords using reversible encryption | Disabled      | Weakens password storage                                          |
<img width="1100" height="559" alt="image" src="https://github.com/user-attachments/assets/229982ec-2876-4503-a284-cb8d011fa521" />

### Verification

1. Log in to `WIN11-01` using a domain account.
2. Press **Ctrl + Alt + Delete** → **Change a password**.
3. Attempt to set a password that does not meet the password policy (for example, `password`).
4. Verify that Windows rejects the password.
5. Set a password that meets the domain password policy requirements.
6. Verify that the password change succeeds.
7. On `DC01`, open PowerShell and run:

```powershell
Get-ADDefaultDomainPasswordPolicy
```

Expected output:

```
ComplexityEnabled           : True
DistinguishedName           : DC=corp,DC=test
LockoutDuration             : 00:10:00
LockoutObservationWindow    : 00:10:00
LockoutThreshold            : 0
MaxPasswordAge              : 90.00:00:00
MinPasswordAge              : 1.00:00:00
MinPasswordLength           : 14
objectClass                 : {domainDNS}
objectGuid                  : 5e56184d-991a-45aa-ae28-a0b7b4a9eab9
PasswordHistoryCount        : 24
ReversibleEncryptionEnabled : False
```

---
## 3 - Configure the Account Lockout Policy

1. Navigate to: *Account Policies* → *Account Lockout Policy*.
2. Configure:

```
Account lockout threshold: 5 invalid logon attempts
Account lockout duration: 15 minutes
Reset account lockout counter after: 15 minutes
```

### Verification

1. Log in to `WIN11-01` using a domain account.
2. At the Windows sign-in screen, enter an incorrect password five times for a domain user.
3. Verify that the account is locked.
4. On `DC01`, open *Active Directory Users and Computers*.
5. Navigate to the user account.
6. Open **Properties** → `Account`.
7. Verify that the account is locked.
8. Click **Unlock account** and click **OK**.
9. Open PowerShell on `DC01` and run:

```powershell
Get-ADDefaultDomainPasswordPolicy
```

Expected output:

```
ComplexityEnabled           : True
DistinguishedName           : DC=corp,DC=test
LockoutDuration             : 00:15:00
LockoutObservationWindow    : 00:15:00
LockoutThreshold            : 5
MaxPasswordAge              : 90.00:00:00
MinPasswordAge              : 1.00:00:00
MinPasswordLength           : 14
objectClass                 : {domainDNS}
objectGuid                  : 5e56184d-991a-45aa-ae28-a0b7b4a9eab9
PasswordHistoryCount        : 24
ReversibleEncryptionEnabled : False
```


