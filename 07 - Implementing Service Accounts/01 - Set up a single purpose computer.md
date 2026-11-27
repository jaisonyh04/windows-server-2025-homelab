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
3. Join `KIOSK-01 ` to the active directory domain.

---
## 3 - Configure Automatic Logon Using Sysinternals

1. On `KIOSK-01`, download Microsoft Sysinternals Autologon: [https://learn.microsoft.com/en-us/sysinternals/downloads/autologon]()
2. Extract the downloaded ZIP file.
3. Right-click `Autologon64.exe` → **Run as administrator**.
4. Accept the license agreement.
5. Enter the following information:

| Setting  | Value           |
| -------- | --------------- |
| Username | svc_website     |
| Domain   | corp.test       |
| Password | <YOUR_PASSWORD> |
6. Click **Enable**.
7. Restart the computer.
8. Verify that Windows automatically signs in as `CORP\svc_website`.

---
## 4 - Configure Google Chrome to Display a Specific Website

Perform the following steps while signed in as `CORP\svc_website`.

1. Open Google Chrome.
2. Navigate to: `chrome://settings/onStartup`
3. Select **Open a specific page or set of pages**.
4. Click **Add a new page**.
5. Enter the desired URL: `https://www.microsoft.com`
6. Close and reopen Google Chrome.
7. Verify that the configured website opens automatically.

---
## 5 - Configure Google Chrome to Start in Full-Screen Mode

