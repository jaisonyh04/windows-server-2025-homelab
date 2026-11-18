### Objective

Prevent users from using USB storage devices.
<img width="942" height="523" alt="image" src="https://github.com/user-attachments/assets/3b098884-3299-43d3-9565-b4584d8ef4e1" />

---
1. Open Server Manager → Tools → Group Policy Management.
2. Navigate to: `CORP` → `Workstations`.
3. Right-click `Workstations` → **Create a GPO in this domain, and Link it here...**.
4. Type `Disable USB Storage` and click **OK**.
5. Right-click `Disable USB Storage` → **Edit**.
6. Navigate to: Computer Configuration → Policies → Administrative Templates → System → Removable Storage Access.
7. Double-click *All Removable Storage classes: Deny all access*.
8. Select **Enabled**.
9. Click **Apply** → **OK**.

---
## Verification

1. Log in using a domain account.
2. Connect a USB storage device.
3. Verify that the device is not accessible in **File Explorer**.
4. Open **Device Manager** and verify that the USB storage device is detected but cannot be used.
5. Open PowerShell and run:

```
gpresult /scope user /r
gpresult /scope computer /r
```

Expected output:

```
 Applied Group Policy Objects
    -----------------------------
        Disable USB Storage
```
