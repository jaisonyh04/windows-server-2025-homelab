### Objective

Organize users and manage permissions through security groups.

---
## 1 - Create the Global Groups (Users)

>A Global Group represents **who** people are.
>Membership in these groups defines a user's **department or role**.


1. Open Server Manager → Tools → Active Directory Users and Computers.
2. Navigate to: `corp.test` → `Corp` → `Groups`.
3. Right-click the `Groups` OU → **New** → **Group**.
4. Give it a name, set Group scope to `Global` and Group type to `Security`, click **OK**.
5. Create the following groups:

| Group Name      |
| --------------- |
| GG_IT_SysAdmins |
| GG_IT_HelpDesk  |
| GG_HR           |
| GG_Finance      |
| GG_Operations   |

Where:
- **GG** = Global Group

---
## 2 - Assign User Membership

1. Double-click on a group.
2. Go to the `Members` tab → **Add...**.
3. Type the user logon name → **Check names** → **OK**.
4. Add the rest of the members → **Apply** → **OK**.
5. Add users to their corresponding Golbal Security Groups:

| Group Name      | Members               |
| --------------- | --------------------- |
| GG_IT_SysAdmins | jsmith / abrown       |
| GG_IT_HelpDesk  | dwilson / slee        |
| GG_HR           | mjohnson / edavis     |
| GG_Finance      | janderson / smartinez |
| GG_Operations   | dmiller / ogarcia     |

---
## 3 - Create the Domain Local Groups (Permissions)

>A **Domain Local Group** represents **what resource can be accessed**.

1. Open Server Manager → Tools → Active Directory Users and Computers.
2. Navigate to: `corp.test` → `Corp` → `Groups`.
3. Right-click the `Groups` OU → **New** → **Group**.
4. Give it a name, set Group scope to `Domain Local` and Group type to `Security`, click **OK**.
5. Create the following groups:

| Group Name            |
| --------------------- |
| DL_FS_IT_SysAdmins_RW |
| DL_FS_IT_HelpDesk_RW  |
| DL_FS_HR_RW           |
| DL_FS_Finance_RW      |
| DL_FS_Operations_RW   |

Where:
- **DL** = Domain Local
- **FS** = File Server (resource type)
- **RW** = Read/Write
- **RO** = Read Only
<img width="1275" height="763" alt="image" src="https://github.com/user-attachments/assets/0ea6df8b-1f4c-4882-a980-6e92c0c0edf8" />


---
## 4 - Configure Group Nesting

1. Right-click the `GG_IT_SysAdmins` global group → **Add to a group...**.
2. Write `dl` → **Check Names**.
3. Select `DL_FS_IT_SysAdmins_RW` → **OK** → **OK**.
4. Add each Global Group to its corresponding Domain Local Group.

| Global Group    | Member of             |
| --------------- | --------------------- |
| GG_IT_SysAdmins | DL_FS_IT_SysAdmins_RW |
| GG_IT_HelpDesk  | DL_FS_IT_HelpDesk_RW  |
| GG_HR           | DL_FS_HR_RW           |
| GG_Finance      | DL_FS_Finance_RW      |
| GG_Operations   | DL_FS_Operations_RW   |

---

### **5 - Verify Group Membership**

1. Open Server Manager → Tools → Active Directory Users and Computers.
2. Navigate to `corp.test` → `Corp` → `Groups`.
3. Open `DL_FS_IT_SysAdmins_RW`.
4. Verify that `GG_IT_SysAdmins` appears under the `Members` tab.
5. Repeat the same pattern for the rest of the departments.

---
> [!note]
> This Lab is following Microsoft's **AGDLP** model, which is the standard way to assign permissions in a **single-domain Active Directory** environment.
>  
>  **A →            G →                         DL →                                     P**
>  
>  **Accounts → Global Groups → Domain Local Groups → Permissions**

## AGDLP example

```
User: Alice
        │
        ▼
      GG_SysAdmins
        │
        ▼
      DL_FS_IT_SysAdmins_RW
        │
        ▼
      \\DC01\SysAdmins
```


