## Purpose
Implement a stricter password policy for privileged administrative accounts without modifying the existing *Default Domain Policy*.

---
## 1 - Create a Global Security Group for Privileged Accounts

1. Open *Server Manager* → *Tools* → *Active Directory Users and Computers*.
2. Navigate to: `corp.test` → `Corp` → `Groups`.
3. Right-click → **New** → **Group**.
4. Configure:

| Setting     | Value                    |
| ----------- | ------------------------ |
| Group name  | `GG_Privileged_Accounts` |
| Group scope | Global                   |
| Group type  | Security                 |

6. Open the group → **Members** → **Add**.
7. Add `jaison-admin`.

> [!NOTE]
> - This group defines which accounts receive the stricter password policy. 
> - Membership does not grant administrative privileges.


---
## 2 - Create the Fine-Grained Password Policy

1. Open *Active Directory Users and Computers* → *Active Directory Administrative Center*.
2. Navigate to: `corp (local)` → `System` → `Password Settings Container`.
3. In the Tasks panel, click **New** → **Password Settings**.
4. Configure:

| Setting                                    | Value                 |
| ------------------------------------------ | --------------------- |
| Name                                       | `AdminPasswordPolicy` |
| Precedence                                 | 1                     |
| Enforce Minimum password length            | 20                    |
| Enforce password history                   | 24                    |
| Password must meet complexity requirements | Enabled               |
| Store password using reversible encryption | Disabled              |
| Protect from accidental deletion           | Enabled               |
| Enforce Minimum password age               | 1                     |
| Enforce Maximum password age               | 42                    |
| Enforce account lockout policy             | Disabled              |
5. Under *Directly Applies To*, click **Add...**.
6. Enter `GG_Privileged_Accounts` → **Check Names** → **OK** → **OK**.


> [!important]
> - **Precedence**: Determines the order in which the policy objects are applied when multiple password settings are applied to a user or a group.
> - **Password Settings Objects (PSOs)**: The password setting with the lowest precedence number has the highest priority and will be applied.


---
## 3 - Test Password Policy Enforcement

- [ ] Create a temporary standard user account named `fgpp-test`.
- [ ] Add the account to `GG_Privileged_Accounts`.
- [ ] Attempt to reset its password to a complex password containing between 14 and 19 characters.
- [ ] Verify that Active Directory rejects the password.
- [ ] Set a compliant password containing at least 20 characters.
- [ ] Verify that the operation succeeds.
- [ ] Remove the temporary account after completing the test.