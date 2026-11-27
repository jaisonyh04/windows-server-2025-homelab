## Purpose
Implement a stricter password policy for privileged administrative accounts without modifying the existing *Default Domain Policy*.

---
## 1 - Define the Password Policy Strategy

|Setting|Existing Domain Policy|Privileged Accounts (PSO)|
|---|---|---|
|Minimum password length|14 characters|**20 characters**|
|Password complexity|Enabled|Enabled|
|Password history|24|24|
|Minimum password age|1 day|1 day|
|Maximum password age|90 days|90 days|
|Reversible encryption|Disabled|Disabled|
|Account lockout threshold|5 attempts|5 attempts|
|Account lockout duration|15 minutes|15 minutes|
|Reset lockout counter|15 minutes|15 minutes|

---
## 2 - Create a Global Security Group

1. On `WIN11-01`, sign in as `jaison-admin@corp.test`.
2. Open **Active Directory Users and Computers**.
3. Navigate to: `corp.test` → `Corp` → `Groups`.
4. Right-click → **New** → **Group**.
5. Configure:

|Setting|Value|
|---|---|
|Group name|`GG_Privileged_Accounts`|
|Group scope|Global|
|Group type|Security|

6. Open the group → **Members** → **Add**.
7. Add `jaison-admin`.

> [!NOTE]
> This group defines which accounts receive the stricter password policy. Membership does not grant administrative privileges.


---
## 3 - Create the Fine-Grained Password Policy

1. Open *Active Directory Administrative Center* (`dsac.exe`).
2. Navigate to: `corp (local)` → `System` → `Password Settings Container`.
3. In the Tasks panel, select **New** → **Password Settings**.
4. Configure:

|Setting|Value|
|---|---|
|Name|`PSO_Privileged_Accounts`|
|Precedence|10|
|Minimum password length|20|
|Enforce password history|24|
|Minimum password age|1 day|
|Maximum password age|90 days|
|Password complexity|Enabled|
|Reversible encryption|Disabled|
|Account lockout threshold|5 attempts|
|Reset failed logon attempts count|15 minutes|
|Account lockout duration|15 minutes|
|Protect from accidental deletion|Enabled|
5. Under *Directly Applies To*, click **Add**.
6. Enter `GG_Privileged_Accounts` → **Check Names** → **OK** → **OK**.

> [!NOTE]
> Fine-Grained Password Policies (FGPPs) are stored as Password Settings Objects (PSOs) and can be assigned to users or Global Security Groups, but not directly to OUs.

---
## 4 - Verify the Password Policy

1. On `WIN11-01`, open PowerShell and run:

```
Get-ADUserResultantPasswordPolicy -Identity jaison-admin
```

Expected output:

```
Name                         : PSO_Privileged_Accounts
Precedence                   : 10
MinPasswordLength            : 20
MaxPasswordAge               : 90.00:00:00
MinPasswordAge               : 1.00:00:00
PasswordHistoryCount         : 24
ComplexityEnabled            : True
LockoutThreshold             : 5
LockoutDuration              : 00:15:00
LockoutObservationWindow     : 00:15:00
ReversibleEncryptionEnabled  : False
```

2. Verify that the default domain password policy remains unchanged:

```
Get-ADDefaultDomainPasswordPolicy
```

3. Verify that standard users are not affected by the PSO:

```
Get-ADUserResultantPasswordPolicy -Identity jsmith
```

No output is expected because `jsmith` follows the default domain password policy.

---
## 5 - Test Password Policy Enforcement

- [ ] Create a temporary standard user account named `fgpp-test`.
- [ ] Add the account to `GG_Privileged_Accounts`.
- [ ] Attempt to reset its password to a complex password containing between 14 and 19 characters.
- [ ] Verify that Active Directory rejects the password.
- [ ] Set a compliant password containing at least 20 characters.
- [ ] Verify that the operation succeeds.
- [ ] Remove the temporary account after completing the test.



> [!IMPORTANT]
> A **Password Settings Object** (**PSO**) replaces the entire password and account lockout policy for its targeted accounts rather than merging individual settings with the Default Domain Policy. Also, accounts with **Password never expires** enabled will not respect the configured 90-day expiration.