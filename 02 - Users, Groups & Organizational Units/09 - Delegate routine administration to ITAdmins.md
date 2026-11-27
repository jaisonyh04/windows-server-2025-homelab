### Objective

Delegate user account administration to the IT Administrators group.

---
### Manage user accounts

1. Open Server Manager → Tools → Active Directory Users and Computers.
2. Expand `corp.test`.
3. Navigate to: `Corp` → `Users`.
4. Right-click `Users` → **Delegate Control**.
5. Click **Next** → **Add...**.
6. Type: `GG` and click **Check Names** and select: `GG_IT_SysAdmins`.
7. Click **OK** → **OK** → **Next**.
8. Select *Create a custom task to delegate* → **Next**.
9. Select *Only the following objects in the folder* → *User Objects*.
10. Enable:

```
[x] Create selected objects in this folder
[x] Delete selected objects in this folder
```

11. Click **Next**.
12. Select *General* and enable `read`/`write` permissions.
13. Click **Next** → **Finish**.
14. Right-click `Users` → **Delegate Control**.
15. Click **Next** → **Add...**.
16. Type: `GG` and click **Check Names** and select: `GG_IT_SysAdmins`.
17. Click **OK** → **OK** → **Next**.
18. *Delegate the following common tasks*:

```
[x] Create, delete, and manage user accounts
```

19. Click **Next** → **Finish**.

---

### Manage Computers accounts

1. Right-click `Computers` OU → **Delegate Control**.
2. Click **Next** → **Add...**.
3. Type: `GG` and click **Check Names** and select: `GG_IT_SysAdmins`.
4. Click **OK** → **OK** → **Next**.
5. Select *Create a custom task to delegate* → **Next**.
6. Select *Only the following objects in the folder* → *Computer Objects*.
7. Enable:

```
[x] Create selected objects in this folder
[x] Delete selected objects in this folder
```

8. Click **Next**.
9. Select *General* and enable `read`/`write` permissions.
10. Click **Next** → **Finish**.

---

### Manage Domain Local group membership

1. Navigate to: `Corp` → `Groups`.
2. Right-click `Groups` OU → **Delegate Control**.
3. Click **Next** → **Add...**.
4. Type: `GG` and click **Check Names** and select: `GG_IT_SysAdmins`.
5. Click **OK** → **OK** → **Next**.
6. Select *Delegate the following common tasks*:

```
[x] Modify the membership of a group
```

7. Click **Next** → **Finish**.

---

### Test delegated permissions

1. On `WIN11-01` sign in using test accounts for `GG_IT_SysAdmins` (jsmith / abrown).
2. Test the following:

- [ ] Create a test user account in `OU=Users`
- [ ] Modify the user's department and job title
- [ ] Disable a test user account
- [ ] Create a test computer account in `OU=Computers`
- [ ] Add `GG_HR` to `DL_FS_HR_RW`
- [ ] Verify that `GG_IT_SysAdmins` cannot modify `Domain Admins` membership (corp.test → Users → Domain Admins security group).


