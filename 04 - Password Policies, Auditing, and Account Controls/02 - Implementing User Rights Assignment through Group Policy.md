## Purpose
Assign and restrict user rights to enhance security.

---
## 1 - Configure User Rights Assignment for Domain Controllers

1. Open *Server Manager* → *Tools* → *Group Policy Management*.
2. Navigate to `Forest: corp.test` → `Domains` → `corp.test`.
3. Right-click `Domain Controllers` → **Create a GPO in this domain, and Link it here...**.
4. Name the GPO `User Rights`.
5. Right-click the GPO → **Edit**.
6. Navigate to:

```
Computer Configuration
└── Policies
    └── Windows Settings
        └── Security Settings
            └── Local Policies
                └── User Rights Assignment
```


7. Double-click *Deny log on locally*.
8. Check *Define these policy settings* → **Add User or Group...** → **Browse...**.
9. Add: `CORP\GG_HelpDesk`, `CORP\GG_HR`, `CORP\GG_Finance`, `CORP\GG_Operations`.
10. Double-click *Allow log on through Remote Desktop Services*.
11. Check *Define these policy settings* → **Add User or Group...** → **Browse...**.
12. Add: `BUILTIN\Administrators`.

---
## 2 - Testing deny log on locally

1. On `DC01` sign-out from Admin account.
2. Sign-in using test accounts for `GG_IT_HelpDesk`, `GG_HR`, `GG_Finance` and `GG_Operations`.
3. Verify Windows display the error message: `The sign-in method you're trying to use isn't allowed. For more info, contact your network administrator`.

---
## 3 - Testing Allow log on through Remote Desktop Services

1. Verify *Remote Desktop* is enabled on `DC01`.
2. On `WIN11-01`, sign-in as `dwilson`, `mjohnson`, `janderson` and `dmiller`.
3. Open *Remote Desktop Connection*.
4. Type: `DC01` → `Connect`.
5. Enter the password →**OK**.
6. Verify Windows display the error message: `The connection was denied because the user account is not authorized for remote login`.



