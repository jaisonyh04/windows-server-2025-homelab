## Scenario
A user is unable to log in and receives a message that their account is locket out.

---
## 1 - Lock the User Account
To simulate a real Help Desk ticket, intentionally lock a user account.

1. On `WIN11-01` Sign out of Windows.
2. At the sign-in screen, select one of your domain test users.
3. Enter an incorrect password multiple times until the account becomes locked.

>The number of failed attempts depends of the Account Lockout Policy.

4. When the account becomes locked, Windows displays a message similar to: 

> **The referenced account is currently locked out and may not be logged on to.**
<img width="1273" height="765" alt="image" src="https://github.com/user-attachments/assets/5c98a530-2b77-4a9a-8a60-63fbb3cefe39" />

---
## 2 - Verify the Account Status

1. On `DC01` Open *Server Manager* → *Tools* → *Active Directory Users and Computers* → `corp.test`.
2. Right-click `corp.test` → **Find...**.
3. Enter the affected user name → **Find Now**.
4. Right-click the user → **Properties** → **Account**.
5. If the account is locked, Windows displays: 

```
Unlock account.
This account is currently locked out on this Active Directory Domain Controller.
```
<img width="1271" height="764" alt="image" src="https://github.com/user-attachments/assets/f8e3c9ce-635f-4e2b-bb3d-3a7113f5425d" />


---
## 3 - Unlock the Account

1. If the user remember the password just check `Unlock account` → **Apply** → **OK**.
2. If the user doesn't remember the password, right click the user name → **Reset Password...**.
3. Enter a temporary password.
4. Enable `User must change password at next logon` and `Unlock the user's account`.
5. Click **OK** → **OK**.

---
## 4 - Test the Resolution

1. Return to `WIN11-01`.
2. At the sign-in screen, sign in using the temporary password.
3. Windows displays: `The user's password must be changed before signing in`.
4. The new password must meet complexity requirements.
<img width="1271" height="764" alt="image" src="https://github.com/user-attachments/assets/ca92f3d3-7f93-4263-98c9-4f2fa0c89bbe" />



