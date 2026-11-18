### Objective

Prevent users from accessing the Control Panel.

---

1. Open Server Manager → Tools → Group Policy Management.
2. Navigate to: `CORP` → `Group Policy Objects`.
3. Right-click `Group Policy Objects` → **New**.
4. Type `Restrict Control Panel` and click **OK**.
5. Right-click `Restrict Control Panel` → **Edit**.
6. Navigate to:

```
User Configuration
└── Policies
    └── Administrative Templates
        └── Control Panel
```

7. Double-click *Prohibit access to Control Panel and PC settings*.
8. Select **Enabled**.
9. Click **Apply** → **OK**.
10. Return to Group Policy Management.
11. Navigate to: `CORP` → `Users` → `HR`.
12. Right-click `HR` → **Link an Existing GPO...**.
13. Select `Restrict Control Panel` → **OK**.
14. Navigate to: `CORP` → `Users` → `Finance`.
15. Right-click `Finance` → **Link an Existing GPO...**.
16. Select `Restrict Control Panel` → **OK**.
17. Navigate to: `CORP` → `Users` → `Operations`.
18. Right-click `Operations` → **Link an Existing GPO...**.
19. Select `Restrict Control Panel` → **OK**.

---
## Verification

1. Log in as a domain user located in the `HR`, `Finance`, or `Operations` OU.
2. Press `Win` + `R`, type `control`, and verify that access is blocked.
3. Press `Win` + `I` (Settings) and verify that access is blocked.
4. Open PowerShell and run:

```
gpresult /scope user /r
gpresult /scope computer /r
```

Expected output:

```
 Applied Group Policy Objects
    -----------------------------
        Restrict Control Panel
```