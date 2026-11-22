## Purpose
Create a separate privileged account for administration and keep the **built-in Administrator** account for emergency recovery ("break-glass" account).

---
## 1 - Create an Admins OU

1. Open *Server Manager* → *Tools* → *Active Directory Users and Computers*.
2. Right-click on `corp.test` → **New** → **Organizational Unit**.
3. Enter: `Corp`.
4. Right-click on `Corp` → **New** → **Organizational Unit**.
5. Type: `Admins`.

---
## 2 - Create the user

1. Right-click `Admins` OU → **New** → **User**.
2. Enter:

| Setting         | Value        |
| --------------- | ------------ |
| First Name      | Jaison       |
| Last Name       | Hernandez    |
| User Logon Name | jaison-admin |
3. Click **Next**.
4. Assign a strong password.
5. For simplicity, disable *user must change password at next logon*, enable *Password never expires* option and click **Next** → **Finish**.

---
## 3 - Add the account to Domain Admins

1. Right-click `Jaison Hernandez` user → **Properties**.
2. Click **Member Of** → **Add...**.
3. Enter `Domain Admins` → **Check Names** → **OK** → **Apply** → **OK**.

---
## 4 - Verify Group Membership

1. Open PowerShell and run: `Get-ADGroupMember "Domain Admins"`.
2. Expected output: 

```
Administrator
jaison-admin
```

