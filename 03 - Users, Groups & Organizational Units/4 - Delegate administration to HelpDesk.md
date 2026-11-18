### Objective

Delegate routine user account management tasks to the HelpDesk team.

---
### Delegate Passwords Resets

1. Open Server Manager → Tools → Active Directory Users and Computers.
2. Expand corp.test.
3. Navigate to: `CORP` →` Users`.
4. Right-click `HR` → **Delegate Control**.
5. Click **Next** → **Add...**.
6. Type: `GG` and click **Check Names** and select: `GG_HelpDesk`.
7. Click **OK** → **OK** → **Next**.
8. Delegate the following common tasks:

```
[x] Reset user passwords and force password change at next logon.
[x] Read all user information.
```

9. Click **Next** → **Finish**.
10. Repeat the same pattern for `Finance` and `Operations` OU.

---
### Delegate account unlocking

1. Right-click `HR` → **Delegate Control**.
2. Click **Next** → **Add...**.
3. Type: `GG` and click **Check Names** and select: `GG_HelpDesk`.
4. Click **OK** → **OK** → **Next**.
5. Select Create a custom task to delegate → **Next**.
6. Select Only the following objects in the folder → User Objects → **Next**.
7. Select Property-specific permissions.
8. Locate and select:

```
[x] Read lockoutTime
[x] Write lockoutTime
```

9. Click **Next** → **Finish**.
10. Repeat the same pattern for `Finance` and `Operations` OU.

---
### Test delegated permissions

1. On `WIN11-01` sign in using test accounts for `GG_HelpDesk` (dwilson / slee).
2. Test the following:

- [ ] Open Active Directory Users and Computers.
- [ ] Locate an HR user account.
- [ ] Reset the user's password.
- [ ] Unlock a locked user account.
- [ ] Attempt to create a new user account (should be denied).
- [ ] Attempt to modify security group membership (should be denied).

```
CORP
└── Users
    ├── HR          ← Delegate GG_HelpDesk
    ├── Finance     ← Delegate GG_HelpDesk
    └── Operations  ← Delegate GG_HelpDesk
```



> [!NOTE]
> **Why is control delegated to `GG_HelpDesk` only for the HR, Finance, and Operations OUs?**  
> In a real-world organization, the HelpDesk typically supports end users but does not manage IT staff accounts. 
> This separation of duties helps protect privileged accounts and follows the principle of least privilege.

