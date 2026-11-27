### Objective

Prevent users from using USB storage devices.

---
## 1 - Configure the GPO

1. Open Server Manager → Tools → Group Policy Management.
2. Navigate to: `Forest: corp.test` → `Domains` → `corp.test` → `Corp` → `Computers`.
3. Right-click `Desktops` OU → **Create a GPO in this domain, and Link it here...**.
4. Type `Disable USB Storage` and click **OK**.
5. Right-click `Disable USB Storage` → **Edit**.
6. Navigate to: Computer Configuration → Policies → Administrative Templates → System → Removable Storage Access.
7. Double-click *All Removable Storage classes: Deny all access*.
8. Select **Enabled**.
9. Click **Apply** → **OK**.

---
## 2 - Verification

1. Log in using a domain account.
2. Connect a USB storage device.
3. Verify that the device is not accessible in **File Explorer**.
4. Open **Device Manager** and verify that the USB storage device is detected but cannot be used.
5. Open PowerShell and run:

```
gpresult /scope computer /r
```

Expected output:

```
 Applied Group Policy Objects
    -----------------------------
        Disable USB Storage
```

---
## 3 - Understanding the policy

| Device                | Effect of this GPO           |
| --------------------- | ---------------------------- |
| USB flash drive       | ==🔴Storage access blocked== |
| CD/DVD                | ==🔴Storage access blocked== |
| Removable memory card | ==🔴Storage access blocked== |
| USB keyboard          | ==🟢Unaffected==                   |
| USB mouse             | ==🟢Unaffected==                   |
| USB printer           | ==🟢Printing unaffected==          |


> [!NOTE]
> The policy restricts **storage access**, not USB connectivity itself. 
> It does not disable USB ports or prevent device detection.