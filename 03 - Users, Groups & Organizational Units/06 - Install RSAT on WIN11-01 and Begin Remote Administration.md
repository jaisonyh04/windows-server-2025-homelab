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

3. Appropriate permissions on the remote Windows Server. Administrative privileges may be required for certain operations, while delegated permissions can be sufficient for others.

4. Network connectivity to the remote Windows Server systems you want to manage.

---
## 1 - Install RSAT (Remote Server Administration Tools)

1. On `WIN11-01` sign in as `jaison-admin@corp.test`.
2. Go to Settings → System → Optional features → View features → See available features.
3. Search for and install:
- *RSAT: Active Directory Domain Services and Lightweight Directory Services Tools*
- *RSAT: DNS Server Tools*
- *RSAT: Group Policy Management Tools*
- *RSAT: Server Manager*
4. Click **Add**.
5. Wait for the installation to complete and click **Close**.
6. Open **Windows Tools** and verify that Active Directory Users and Computers, DNS, Group Policy Management, and Server Manager are available.

---
## 2 - Begin Remote Server Administration Using Server Manager

1. On `WIN11-01`, open *Server Manager* → *Manage* → *Add Servers*.
2. Select the **Active Directory** tab.
3. Verify *Location* is set to: `corp`.
4. Click **Find Now** → Select `DC01` and click **→**.
5. Click **OK**.
6. Select **All Servers**.
7. Verify that `DC01` appears with an **Online** status.
8. Right-click `DC01` to access available remote management tools, such as **Computer Management** or **Event Viewer**.
9. Perform future administration from `WIN11-01` instead of signing in directly to `DC01`.



> [!NOTE]  
> **Firewall requirements**
> 
>- **Server Manager / PowerShell Remoting:** WinRM requires inbound TCP port `5985` on `DC01` for the default HTTP listener.
>- **Event Viewer:** Remote event log access may require the **Remote Event Log Management** firewall rule group.
>- **Computer Management:** Certain functions require additional RPC, WMI, or Remote Service Management firewall rules.
>- **Disk Management:** Remote disk administration may require the **Remote Volume Management** firewall rule group and supporting services.
>- **Core Network Diagnostics – ICMP Echo Request (ICMPv4-In)**: This Allow ICMP traffic for network connectivity testing.


