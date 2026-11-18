### Objective

Organize Active Directory objects and create user accounts based on organizational roles and departments.

---
## 1 - Create the Organizational Units (OU):

1. Open Server Manager → Tools → Active Directory Users and Computers.
2. Right-click on `corp.test` → **New** → **Organizational Unit**.
3. Enter: `CORP`.
4. Right-click on `CORP` → **New** → **Organizational Unit**.
5. Create the following structure:

```
corp.test
│
└── OU=CORP
    │
    ├── OU=Users
    │   │
    │   ├── OU=IT
    │   │   ├── OU=ITAdmins
    │   │   └── OU=HelpDesk
    │   │
    │   ├── OU=HR
    │   ├── OU=Finance
    │   └── OU=Operations
    │
    ├── OU=Groups
    │   ├── OU=Global
    │   └── OU=Domain Local
    │
    └── OU=Workstations
        └── WIN11-01
```
<img width="1274" height="763" alt="image" src="https://github.com/user-attachments/assets/98ee9a70-807d-4cbd-9b5a-43433e576e34" />

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

