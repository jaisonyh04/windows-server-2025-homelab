## Purpose

Map network drives for users when they log in.

---

1. Open *Server Manager* → *Tools* → *Group Policy Management*.
2. Navigate to: `Forest: corp.test` → `Domains` → `corp.test` → `Corp` → `Users`.
3. Right-click `HR` OU → **Create a GPO in this domain, and Link it here....**
4. Type `DriveMapping-HR` and click **OK**.
5. Right-click `DriveMapping-HR` → **Edit**.
6. Navigate to *User Configuration* → *Preferences* → *Windows Settings* → *Drive Maps*. 
7. Right-click *Drive Maps* → **New** → **Mapped Drive**.
8. Configure:

```
Action: Update
Location: \\DC01\HR
Drive Letter: P
Show this drive
```

9. Click **Apply**.
10. Select `Common` tab →` Item-level targeting` → `Targeting...`.
11. Click **New Item** → **Security Group**.
12. Click **Group ...** selection button.
13. Type `dl`, click **Check Names**.
14. Select `DL_FS_HR_RW` and click **OK**.
15. Click **OK** to close the remaining dialogs.
16. Return to Group Policy Management.
17. Repeat the same pattern for the rest of the departments:

| Group                     | GPO                       | Drive | Share location      |
| ------------------------- | ------------------------- | ----- | ------------------- |
| **DL_FS_IT_SysAdmins_RW** | `DriveMapping-SysAdmins`  | `P`   | `\\DC01\SysAdmins`  |
| **DL_FS_IT_HelpDesk_RW**  | `DriveMapping-HelpDesk`   | `P`   | `\\DC01\HelpDesk`   |
| **DL_FS_HR_RW**           | `DriveMapping-HR`         | `P`   | `\\DC01\HR`         |
| **DL_FS_Finance_RW**      | `DriveMapping-Finance`    | `P`   | `\\DC01\Finance`    |
| **DL_FS_Operations_RW**   | `DriveMapping-Operations` | `P`   | `\\DC01\Operations` |

---
## Verification

1. On `WIN11-01`, sign in as `CORP\mjohnson`.
2. Open File Explorer and Verify that the mapped drive appears under **This PC**.
3. Open the mapped drive and verify that the user can access the shared folder.
4. Open PowerShell and run:

```
gpresult /scope user /r
```

Expected output:

```
 Applied Group Policy Objects
    -----------------------------
        DriveMapping-HR
```

<img width="1276" height="764" alt="image" src="https://github.com/user-attachments/assets/80d31444-f61a-473f-8df6-16f798345aa2" />



