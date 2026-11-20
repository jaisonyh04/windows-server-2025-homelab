### Purpose

Troubleshoot `G`roup `P`olicy `O`bjects.

---

## 1 - Force a Group Policy update

1. Open PowerShell and run:

```powershell
gpupdate /force
```

---
## 2 - Verify the Resultant Set of Policy (RSoP) 


1. If it is a **Computer Configuration** policy, restart the computer.
2. If it is a **User Configuration** policy, sign out and sign back in.
3. Verify that the GPO was applied:

```powershell
gpresult /scope computer /r
gpresult /scope user /r
```

4. Verify that **Computer Settings** or **User Settings** match the expected target.
5. The correct **Applied Group Policy Objects** are listed.
6. The GPO does not appear under **filtered out**.

---
## 3 - Verify the GPO configuration

1. Verify that the user or computer object is located in the correct **Organizational Unit (OU)**.
2. Verify that the GPO is linked to the correct `OU` and that **Link Enabled** is enabled.
3. Verify the GPO's **Security Filtering** and **Delegation** permissions.
4. Check **Event Viewer** for Group Policy processing errors.

```text
Event Viewer
└── Applications and Services Logs
    └── Microsoft
        └── Windows
            └── GroupPolicy
                └── Operational
```

<img width="1275" height="763" alt="image" src="https://github.com/user-attachments/assets/09e7a1cd-ac0f-434d-9a56-053f69a20cf3" />
