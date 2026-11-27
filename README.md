<img width="1276" height="862" alt="image" src="https://github.com/user-attachments/assets/63f0d43a-1bd8-4925-8058-036fee13335a" />
## 1. Windows Server 2025 Homelab

Deployment of a virtualized Windows Server 2025 Homelab with a domain controller and a client on Arch Linux to practice Windows administration and IT support. 

The lab documents domain deployment, user and group administration, workstation management, and troubleshooting from initial diagnosis through resolution checks.

---
## 2. Architecture

### 2.1 Host Hardware
- **Operating System**: Arch Linux.
- **CPU**: 12th Gen Intel(R) Core(TM) i5-12400F (12) @ 2.50 GHz.
- **GPU**: NVIDIA GeForce RTX 3070.
- **Memory**: 16 G of RAM.

### 2.2 Hypervisor and Virtualization
- KVM / QEMU / libvirt.

### 2.3 Virtual Network
- `corp.test` NAT networking.
- Private subnet: `10.10.10.0/24`.
- DHCP range: `10.10.10.100 – 10.10.10.200`.
- Gateway: `10.10.10.1`.
<img width="799" height="628" alt="image" src="https://github.com/user-attachments/assets/f1df4edc-e473-46b5-8a39-06143ac245da" />
### 2.4 Domain
- Forest: `corp.test`.
- Domain: `corp.test`.
- NetBIOS: `CORP` .

### 2.5 Virtual Machines

#### DC01
- Windows Server 2025 Standard Evaluation (Desktop Experience).
- Domain Controller.
- DNS.
- Active Directory Domain Services.
- SMB File Server.
- IP address: `10.10.10.10`.
- Subnet mask: `255.255.255.0`.
- DefaultGateway: `10.10.10.1`.
- Preferred DNS server: `10.10.10.10`.
<img width="1279" height="864" alt="image" src="https://github.com/user-attachments/assets/76677e2e-def9-4fdb-aaae-067174473c8e" />
#### WIN11-01
- Windows 11 Pro.
- Domain Client / IT Administrator Workstation.
- Preferred DNS server: `10.10.10.10`.
<img width="1279" height="865" alt="image" src="https://github.com/user-attachments/assets/d01aa991-9a92-48f2-9f9b-7ac9a4082072" />
---
## 3. Windows Administration and Technologies Practiced

- **Active Directory Domain Services and DNS**: Deployed the `corp.test` forest, joined `WIN11-01` to the domain, and documented domain controller checks for DNS, SYSVOL, NETLOGON, and FSMO roles.
- **Identity and Access Management**: Created organizational units, user accounts, and security groups. Documented Help Desk delegation for password resets and account unlocks, plus SMB and NTFS permissions assigned through domain-local groups.
- **Group Policy**: Documented six workstation policies covering drive mapping, local administrator membership, desktop wallpaper, personal Microsoft accounts, Control Panel access, and USB storage. Also documented domain-wide and fine-grained password policies.
- **Remote Server Administration Tools (RSAT)**: Set up RSAT on `WIN11-01` for remote administration.
- **Windows Server Backup**: Documented Windows Server Backup configuration using a dedicated virtual disk.

---
## 4. Troubleshooting

- **Domain sign-in failures**: Documented four simulated Help Desk tickets covering account lockout, recurring lockout, disabled accounts, and expired accounts. Used Security Event ID 4740 to trace recurring lockouts and documented how to verify sign-in after remediation.
- **Group Policy application**: Used gpresult to check applied policies, reviewed OU placement, GPO links, and security filtering, and checked the Group Policy operational log in Event Viewer. |
- **Windows Server Backup failure**: Documented recovery from a backup snap-in error, including schedule reconfiguration and a follow-up backup check. |

---
## 5. Learning Resources & Tools

[https://www.youtube.com/@EastCharmer]()

[https://labitpro.com/]()

[https://www.writethedocs.org/]()

[https://github.com/kiril4ik/project-docs-guide]()

[https://obsidian.md/help/]()

[https://www.youtube.com/watch?v=BTLRQ_PZwp4]()

[https://learn.microsoft.com/en-us/]()

[https://chatgpt.com/]()

---
## 6. Homelab Infrastructure Layout

```
                                   Internet
                                       │
                                       │
                               Arch Linux Host
                             KVM / QEMU / libvirt
                                       │
                                corp.test (NAT)
                                10.10.10.0/24
                                       │
                     ┌─────────────────┴─────────────────┐
                     │                                   │
                     │                                   │
                DC01                             WIN11-01
         Windows Server 2025                     Windows 11 Pro
         Domain Controller                       IT Administrator Workstation \ Domain accounts
                     │
                     ├── DNS
                     ├── Active Directory Domain Services
                     ├── File Shares (SMB)
                     
```

---
## 7. Technical Documentation Workflow
```text
                 Obsidian
          Technical Documentation
                    │
                    ▼
           Local Git Repository
            Version Control             
                    │
                    │ git push / git pull
                    ▼
                  GitHub
            Remote Repository
                    │
                    ▼
                  ChatGPT
       Technical Review & Validation
```
