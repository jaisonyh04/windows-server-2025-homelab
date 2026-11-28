## Purpose
Create a separate privileged account for administration and keep the **built-in Administrator** account for emergency recovery ("break-glass" account).

---
## 1 - Create the user

1. Open *Server Manager* → *Tools* → *Active Directory Users and Computers*.
2. Navigate to: `corp.test` → `Corp`.
3. Right-click `Admins` OU → **New** → **User**.
4. Enter:

| Setting         | Value        |
| --------------- | ------------ |
| First Name      | Jaison       |
| Last Name       | Hernandez    |
| User Logon Name | jaison-admin |
3. Click **Next**.
4. Assign a strong password.
5. Click **Next** → **Finish**.

---
## 2 - Add the Account to Domain Admins

1. Right-click `Jaison Hernandez` user → **Properties**.
2. Click **Member Of** → **Add...**.
3. Enter `Domain Admins` → **Check Names** → **OK** → **Apply** → **OK**.

---
## 3 - Verify Group Membership

1. Open PowerShell and run: 

```
Get-ADGroupMember "Domain Admins" |
    Select-Object -ExpandProperty SamAccountName
```

Example output: 

```
Administrator
jaison-admin
```

<img width="1278" height="766" alt="image" src="https://github.com/user-attachments/assets/1e9edb7c-20a1-4631-b392-82f386525887" />
<img width="1920" height="1080" alt="Captura de pantalla 2026-11-28 045729" src="https://github.com/user-attachments/assets/471f9a34-fcf3-487f-84bd-3b8f386c2766" />
