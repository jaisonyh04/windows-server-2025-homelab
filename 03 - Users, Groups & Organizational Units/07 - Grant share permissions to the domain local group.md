### Objective

Assign access to shared folders using Domain Local groups.

---
### 1 - Create the shared folder
- On `DC01`, create a folder:

```
C:\File-sharing
│
├── SysAdmins
├── HelpDesk
├── HR
├── Finance
└── Operations
```
<img width="1275" height="763" alt="image" src="https://github.com/user-attachments/assets/54cdaa2e-063a-49ff-9ad1-0a2c3e8cc784" />

---
### 2 - Set Up the Share (SMB)

>**Share permissions** Control who can access the shared folder over the network.

1. Right-click the `SysAdmins` folder and select **Properties**.
2. Go to the **Sharing** tab and click the **Advanced Sharing...** button.
3. Check the **Share this folder** box.
4. Click the **Permissions** button.
5. Remove `Everyone `group. Add `DL_FS_IT_SysAdmins_RW`.
6. Set the Share Permissions to `Change`.
7. Click **OK** → **OK**.
8. Repeat the same pattern for `HelpDesk`, `HR`, `Finance` and `Operations` folders.


---
### 3 - Configure NTFS Security Permissions

>**NTFS permissions** Control what users can do with files and folders (read, modify, delete, etc.).

1. In the same folder **Properties** window, go to the **Security** tab.
2. Click **Edit...**, then **Add...**.
3. Type `dl`, click **Check Names**.
4. Select `DL_FS_IT_SysAdmins_RW`, click **OK**.
5. Grant it `read`/`write` permissions. Click **OK** → **Close**.
6. Repeat the same pattern for `HelpDesk`, `HR`, `Finance` and `Operations` folders.



> [!NOTE]
> When accessing a shared folder over the network, both SMB and NTFS permissions apply. 
> The effective access is the more restrictive combination.
> 

---
### 4 - Test delegated permissions

1. On `WIN11-01` sign in as: `CORP\jsmith`
2. Open File Explorer.
3. In the `Address bar` enter: `\\DC01.corp.test\`
4. `jsmith` (`SysAdmins`) should **NOT** have access to `HelpDesk`, `HR`, `Finance` or `Operations` folders.
5. Verify that `jsmith` can create, read, and modify files in the `SysAdmins` shared folder but cannot delete them. 

| Folder     | jsmith (ITAdmins)   |
| ---------- | ------------------- |
| SysAdmins  | ==🟢read/write==    |
| HelpDesk   | ==🔴Access Denied== |
| HR         | ==🔴Access Denied== |
| Finance    | ==🔴Access Denied== |
| Operations | ==🔴Access Denied== |

<img width="1275" height="763" alt="image" src="https://github.com/user-attachments/assets/494a1419-3d8e-48fb-81c0-d70bb0bbce6a" />

<img width="1275" height="763" alt="image" src="https://github.com/user-attachments/assets/5f800d3d-aa55-403b-9833-2fe10ca7169d" />

---
### 5 - SMB Administrative Shares

Windows automatically creates hidden administrative shares such as `C$`, `ADMIN$`, and `IPC$` for remote system administration.

Administrators can access a remote computer's `C:` drive using its **UNC** path:

```
\\WIN11-01\C$
```

**Requirements:**

- Administrative privileges on the remote computer.
- Network connectivity and SMB access (TCP 445).
- Windows Firewall configured to allow the required SMB traffic.

Verification (PowerShell):

On `WIN11-01`:

```
Get-SmbShare -Special $true
```

Lists the special SMB shares on the local computer.

On `DC01`:

```
Test-NetConnection WIN11-01 -Port 445
```

Verifies SMB TCP connectivity to `WIN11-01`.


> [!NOTE]
> Administrative shares should only be accessible to authorized administrators. 
> The `$` hides the share from normal browsing but does not provide security by itself.

