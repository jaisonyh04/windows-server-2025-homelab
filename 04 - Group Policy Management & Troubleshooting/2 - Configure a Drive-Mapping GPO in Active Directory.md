## Purpose

Map network drives for users when they log in.

---

1. Open Server Manager → Tools → Group Policy Management.
2. Navigate to: `CORP` → `Users` → `HR`.
3. Right-click `HR` → **Create a GPO in this domain, and Link it here....**
4. Type `DriveMapping-HR` and click **OK**.
5. Right-click `DriveMapping-HR` → **Edit**.
6. Navigate to User Configuration → Preferences → Window Settings.
7. Right-click Drive Maps → **New** → **Mapped Drive**.
8. Configure:

```
Location: \\DC01\HR
Drive Letter: P
Show this drive
```

9. Click **Apply**.
10. Select `Common` tab →` Item-level targeting` → `Targeting...`.
11. Click **New Item** → **Security Group**.
12. Click **Group ...** selection button.
13. Type `dl`, click **Check Names**.
14. Select `DL_HR_Share_Change` and click **OK**.
15. Click **OK** to close the remaining dialogs.
16. Return to Group Policy Management.
17. Repeat the same pattern for the rest of the departments:

| Group                          | GPO                       | Drive | Share location      |
| ------------------------------ | ------------------------- | ----- | ------------------- |
| **DL_ITAdmins_Share_Change**   | `DriveMapping-ITAdmins`   | `P`   | `\\DC01\ITAdmins`   |
| **DL_HelpDesk_Share_Change**   | `DriveMapping-HelpDesk`   | `P`   | `\\DC01\HelpDesk`   |
| **DL_HR_Share_Change**         | `DriveMapping-HR`         | `P`   | `\\DC01\HR`         |
| **DL_Finance_Share_Change**    | `DriveMapping-Finance`    | `P`   | `\\DC01\Finance`    |
| **DL_Operations_Share_Change** | `DriveMapping-Operations` | `P`   | `\\DC01\Operations` |

---
## Verification

1. Log in using a domain account.
2. Open File Explorer and Verify that the mapped drive appears under **This PC**.
3. Open PowerShell and run:

```
gpresult /scope user /r
gpresult /scope computer /r
```

Expected output:

```
 Applied Group Policy Objects
    -----------------------------
        DriveMapping-ITAdmins
```
<img width="1276" height="764" alt="image" src="https://github.com/user-attachments/assets/1dc47d33-9634-4b0e-8443-5eddac194148" />



