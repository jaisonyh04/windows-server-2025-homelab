### Objective

Assign access to shared folders using Domain Local groups.

---
### 1 - Create the shared folder

```
C:\File-sharing
│
├── ITAdmins
├── HelpDesk
├── HR
├── Finance
└── Operations
```

---
### 2 - Set Up the Share (SMB)

>**Share permissions** Control who can access the shared folder over the network.

1. Right-click the `ITAdmins` folder and select **Properties**.
2. Go to the **Sharing** tab and click the **Advanced Sharing...** button.
3. Check the **Share this folder** box.
4. Click the **Permissions** button.
5. Remove `Everyone `group. Add `DL_ITAdmins_Share_Change`.
6. Set the Share Permissions to `Change`.
7. Click **OK** → **OK**.

---
### 3 - Configure NTFS Security Permissions

>**NTFS permissions** Control what users can do with files and folders (read, modify, delete, etc.).

1. In the same folder **Properties** window, go to the **Security** tab.
2. Click **Edit...**, then **Add...**.
3. Type `dl`, click **Check Names**.
4. Select `DL_ITAdmins_Share_Change`, click **OK**.
5. Grant it `read`/`write` permissions. Click **OK** → **Close**.
6. Repeat the same pattern for `HelpDesk`, `HR`, `Finance` and `Operations` folders.

---
### 4 - Test delegated permissions

1. On `WIN11-01` sign in as: `CORP\jsmith`
2. Open File Explorer.
3. In the `Address bar` enter: `\\DC01.corp.test\`
4. `jsmith` (`ITAdmins`) should **NOT** have access to `HelpDesk`, `HR`, `Finance` or `Operations` folders.

| Folder     | jsmith (ITAdmins)   |
| ---------- | ------------------- |
| ITAdmins   | ==🟢Modify==        |
| HelpDesk   | ==🔴Access Denied== |
| HR         | ==🔴Access Denied== |
| Finance    | ==🔴Access Denied== |
| Operations | ==🔴Access Denied== |


