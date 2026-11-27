## Purpose
Understand how *SMB Share* and *NTFS permissions* work together to control access to shared folders.

---
## 1. SMB and NTFS Permissions

|Permission type|Description|Applies to|
|---|---|---|
|SMB Share Permissions|Control access to shared folders over the network.|Network access|
|NTFS Permissions|Control access to files and folders at the filesystem level.|Local and network access|

When accessing a shared folder over the network, both SMB and NTFS permissions apply. The effective access is determined by the most restrictive combination.

### 1.1 Permission Levels

|SMB Permission|Description|
|---|---|
|Read|Read files and browse folders.|
|Change|Read, create, edit and delete files.|
|Full Control|Change permissions and perform all Change operations.|

|NTFS Permission|Description|
|---|---|
|Read|Read files and view folder contents.|
|Write|Create files and edit file contents.|
|Read & Execute|Read files and execute applications.|
|Modify|Read, create, edit, execute and delete files.|
|Full Control|Modify files, change permissions and take ownership.|

### 1.2 Effective Permission Examples

|SMB Share|NTFS|Effective Network Access|
|---|---|---|
|Read|Read|Read only|
|Read|Modify|Read only|
|Read|Full Control|Read only|
|Change|Read|Read only|
|Change|Read + Write|Read, create and edit without deletion|
|Change|Modify|Read, create, edit and delete|
|Change|Full Control|Change-level access|
|Full Control|Modify|Modify-level access|
|Full Control|Full Control|Full Control|

---
## 2. Homelab Configuration Example

| Setting            | Configuration           |
| ------------------ | ----------------------- |
| User               | `CORP\jsmith`           |
| Global Group       | `GG_IT_SysAdmins`       |
| Domain Local Group | `DL_FS_IT_SysAdmins_RW` |
| Shared Folder      | `\\DC01\SysAdmins`      |
| SMB Permission     | `Change`                |
| NTFS Permission    | `Read` + `Write`        |

**Expected Results:**

| Operation          | Access       |
| ------------------ | ------------ |
| Read files         | ==🟢Allowed==      |
| Create files       | ==🟢Allowed==      |
| Edit file contents | ==🟢Allowed==      |
| Rename files       | ==🔴Denied== |
| Delete files       | ==🔴Denied== |
| Change permissions | ==🔴Denied== |

> [!NOTE]  
> These examples assume that no additional group memberships, inherited permissions or ownership-related permissions grant broader access. Always verify effective permissions using the intended user account.