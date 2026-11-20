### Objective

Organize Active Directory objects and create user accounts based on organizational roles and departments.

---
## 1 - Create the Organizational Units (OU):

1. Open Server Manager → Tools → Active Directory Users and Computers.
2. Right-click on `corp.test` → **New** → **Organizational Unit**.
3. Enter: `Corp`.
4. Right-click on `Corp` → **New** → **Organizational Unit**.
5. Create the following structure:

```
corp.test
└── OU=Corp                      Root of the managed structure; delegation and GPO boundary
    ├── OU=Admins                 Privileged adm- accounts only; strict GPOs, no HelpDesk delegation
    ├── OU=Users                 Standard user accounts; base user GPOs (desktop, drive maps)
    │   ├── OU=IT                IT staff daily-use accounts; parent for IT-specific policy
    │   │   ├── OU=HelpDesk      Support staff; delegated password reset and unlock rights
    │   │   └── OU=SysAdmins     Sysadmins' regular accounts (admin tasks use Admin accounts)
    │   ├── OU=HR                HR users; HR-specific GPOs and app settings
    │   ├── OU=Finance           Finance users; Finance-specific GPOs and app settings
    │   └── OU=Operations        Operations users; Operations-specific GPOs and app settings
    ├── OU=Groups                All security groups; type and scope shown by name (G_, DL_)
    ├── OU=Computers             Parent for workstation objects; redircmp default target
    │   ├── OU=Desktops          Fixed PCs; standard workstation GPOs
    │   └── OU=Laptops           Mobile devices; BitLocker, Wi-Fi, VPN, power policies
    ├── OU=Servers               Member servers; hardening and patching GPOs (no DCs here)
    └── OU=Service Accounts      Service accounts and gMSAs; no interactive logon, password policy exceptions
```

> [!NOTE]
> Domain controllers stay in the built-in `Domain Controllers` OU at the domain root, outside `Corp`, because the Default Domain Controllers Policy is linked there.


---
## 2 - Create the users

1. Right-click the `Users` OU.
2. Select **New** → **User**.
3. Fill in the first name, last name and user logon name fields.
4. Click **Next**.
5. Enter the password: `P@ssword123!`
6. Disable *user must change password at next logon*, check the *Password never expires* option and click **Next** → **Finish**.
7. Create the following users:

| First Name | Last Name | User Logon Name | Department / Role |
| ---------- | --------- | --------------- | ----------------- |
| John       | Smith     | jsmith          | ITAdmins          |
| Alice      | Brown     | abrown          | ITAdmins          |
| David      | Wilson    | dwilson         | HelpDesk          |
| Sarah      | Lee       | slee            | HelpDesk          |
| Michael    | Johnson   | mjohnson        | HR                |
| Emily      | Davis     | edavis          | HR                |
| James      | Anderson  | janderson       | Finance           |
| Sophia     | Martinez  | smartinez       | Finance           |
| Daniel     | Miller    | dmiller         | Operations        |
| Olivia     | Garcia    | ogarcia         | Operations        |


> [!note]
> This Lab is following Microsoft's **AGDLP** model, which is the standard way to assign permissions in a **single-domain Active Directory** environment.
>  
>  **A →            G →                         DL →                                     P**
>  
>  **Accounts → Global Groups → Domain Local Groups → Permissions**

