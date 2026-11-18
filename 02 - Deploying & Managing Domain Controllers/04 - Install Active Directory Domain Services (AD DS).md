### Objective

Deploy Active Directory for centralized identity management.

---

1. Open *Server Manager* → *Manage* → Add Roles and Features.
2. Installation Type: *Role-based or feature-based installation* → **Next**.
3. Server Selection: `DC01` → **Next**.
4. Server Roles: Select *Active Directory Domain Services* → *Add Features* → *DNS Server* → *Add Features* → **Next**.
5. Features: Leave the default selections → **Next**.
6. Active Directory Domain Services: Read the information → **Next**.
7. DNS Server: Read the information → **Next**.
8. Confirmation: Enable *Restart the destination server automatically if required* → **Yes** → **Install**.
9. Wait for the installation to finish → **Close**.
10. Open PowerShell:

```powershell
Get-WindowsFeature AD-Domain-Services,DNS
```

Expected output:

```
Display Name                                            Name                       Install State
------------                                            ----                       -------------
[X] Active Directory Domain Services                    AD-Domain-Services             Installed
[X] DNS Server                                          DNS                            Installed
```

