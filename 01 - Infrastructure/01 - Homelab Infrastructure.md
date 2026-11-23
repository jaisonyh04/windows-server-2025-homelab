### Purpose

Deployment of a virtualized Windows Server 2025 Homelab with a domain controller and a client to simulate an enterprise Active Directory environment.

---
## Host Hardware

- **Operating System**: Arch Linux 
- **CPU**: 12th Gen Intel(R) Core(TM) i5-12400F (12) @ 2.50 GHz
- **GPU**: NVIDIA GeForce RTX 3070
- **Memory**: 16 G of RAM
---
## Hypervisor and Virtualization

- KVM / QEMU / libvirt
---
## Virtual Network

- corp.test (NAT)
- 10.10.10.0/24
---
## Domain

- Forest: `corp.test`
- Domain: `corp.test`
- NetBIOS: `CORP` 
---
## Virtual Machines

### DC01

- Windows Server 2025 Standard Evaluation (Desktop Experience).
- Domain Controller.
- DNS.
- Active Directory Domain Services.
- SMB File Server.
<img width="1279" height="864" alt="image" src="https://github.com/user-attachments/assets/76677e2e-def9-4fdb-aaae-067174473c8e" />

### WIN11-01

- Windows 11 Pro.
- Domain Client / IT Administrator Workstation.
<img width="1279" height="865" alt="image" src="https://github.com/user-attachments/assets/d01aa991-9a92-48f2-9f9b-7ac9a4082072" />

---

## Learning Resources & Tools

[https://www.youtube.com/@EastCharmer]()

[https://labitpro.com/]()

[https://www.writethedocs.org/]()

[https://github.com/kiril4ik/project-docs-guide]()

[https://obsidian.md/help/]()

[https://www.youtube.com/watch?v=BTLRQ_PZwp4]()

[https://learn.microsoft.com/en-us/]()

[https://chatgpt.com/]()



---
### Homelab Infrastructure Layout

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

