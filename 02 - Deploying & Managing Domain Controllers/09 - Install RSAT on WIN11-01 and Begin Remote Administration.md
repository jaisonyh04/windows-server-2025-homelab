### Purpose

Manage Windows Server remotely from the administrator workstation.

---
### Prerequisites

To use Remote Server Administration Tools, you need the following prerequisites:

1. A computer running one of the following operating systems:

- Windows 10 (October 2018 Cumulative Update or later) Pro or Enterprise editions only
- Windows 11 Pro or Enterprise editions only
- Any supported version of Windows Server

2. Administrative privileges on the computer where RSAT is installed.

3. Administrative privileges on the remote Windows Server systems for the service you want to manage.

4. Network connectivity to the remote Windows Server systems you want to manage.

---
## 1 - Install RSAT (Remote Server Administration Tools)

1. On `WIN11-01` sign in as `CORP\Administrator`.
2. Go to Settings → System → Optional features → View features → See available features.
3. Install:
- *RSAT: Active Directory Domain Services and Lightweight Directory Services Tools*
- *RSAT: DNS Server Tools*
- *RSAT: Group Policy Management Tools*
- *RSAT: Server Manager*
- *RSAT: File Services Tools*
- *RSAT: Remote Desktop Services Tools*
- *RSAT: Windows Server Update Services Tools*
4. Click **Add**.
5. Wait for the installation to complete and click **Close**.
6. Verify that *Active Directory Users and Computers*, *DNS*, and *Group Policy Management* are available from the **Start** menu.

---
## 2 - Configure WinRM Maximum Envelope Size on Both Machines

### Purpose

When Server Manager requests the server inventory, `DC01` generates a large WS-Management response (roles, features, services, performance data, etc.). On Windows Server 2025, the default `500 KB` envelope appears to be too small for that response. Increasing the server's `MaxEnvelopeSizeKb` allows it to process and return the larger payload successfully.

1. Sign in to `DC01` and `WIN11-01` as `CORP\Administrator`.
2. Open PowerShell and run:

   ```powershell
   Set-Item WSMan:\localhost\MaxEnvelopeSizeKb 8192
   ```

3. Verify the configuration:

   ```powershell
   Get-Item WSMan:\localhost\MaxEnvelopeSizeKb
   ```

4. Confirm the value is:

   ```text
   8192
   ```

5. Restart the WinRM service:

```
   Restart-Service WinRM
```

---
## 3 - Begin Remote Administration

1. On `WIN11-01`, open *Server Manager* → *Manage* → *Add Servers*.
2. Select the **Active Directory** tab.
3. Verify *Location* is set to: `corp`.
4. Click **Find Now** → Select `DC01` and click **→**.
5. Click **OK**.
6. Select **All Servers**.
7. Verify that `DC01` appears with an **Online** status.
8. Right-click `DC01` to access remote management tools such as:
   - *Computer Management*
   - *DNS Manager*
   - *Active Directory Users and Computers*
   - *Group Policy Management*
   - *Event Viewer*
1. Perform future administration from `WIN11-01` instead of signing in directly to `DC01`.

> **Note:** If you plan to use **Event Viewer** remotely, enable the **Remote Event Log Management** firewall rule group on `DC01`.
> If you plan to use **Disk Management** remotely, enable the **Remote Volume Management** firewall rule group on `DC01`.
