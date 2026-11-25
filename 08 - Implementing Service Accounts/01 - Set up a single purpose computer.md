## Purpose
Configure a single-purpose computer to display a specific web page without human intervention.

- Use a service account as login account.
- The account should auto login when computer was rebooted.
- Web browser should startup automatically once logged in and in full screen.
- Set the computer to always be ON.
- Restrict logon for service account.

---
## 1 - Create the user

1. Open Server Manager → Tools → Active Directory Users and Computers.
2. Navigate to corp.test → Corp → Service Accounts.
3. Right-click `Service Accounts` OU → New → User.
4. Enter:


| Setting         | Value       |
| --------------- | ----------- |
| Firts Name      | Service     |
| Last Name       | Website     |
| User Logon Name | svc_website |
5. Click **Next**.
6. Set the password.
7. Enable `User cannot change password` and `Password never expires`.
8. Click **Next** → **Finish**.
9. Open the account properties and enter the following description:
```
Dedicated service account for automatic logon and website display.
```

---
## 2 - Create a new client

1. Create a new Windows Pro or Enterprise client.
2. Rename it `KIOSK-01`.
3. 
