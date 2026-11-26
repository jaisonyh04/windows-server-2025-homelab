### Objective

Create the `corp.test` Active Directory domain by promoting `DC01` to a Domain Controller.

---
## 1 - Open the Promotion Wizard

1. Open: *Server Manager* → Click the notification flag.
2. Select: **Promote this server to a domain controller**.

---
## 2 - Deployment Configuration

1. Select: **Add a new forest**.
2. Root domain name: `corp.test`.
3. Click **Next**.

---
## 3 - Domain Controller Options

1. Forest functional level: Windows Server 2025
2. Domain functional level: Windows Server 2025
3. Domain Name System (DNS): Enabled
4. Global Catalog (GC): Enabled
5. Read Only Domain Controller (RODC): Disabled
6. Directory Services Restore Mode (DSRM): `<DSRM_PASSWORD>`
7. Click **Next**.

> This password is only used for Active Directory recovery.

---
## 4 - DNS Options

1. A warning similar to the following is expected: *A delegation for this DNS server cannot be created...*
2. This is expected because this is the first Domain Controller.
3. Click **Next**.
---
## 5 - Additional Options

1. The NetBIOS domain name: `CORP`
2. Click **Next**.

---
## 6 - Paths

1. Database folder: `C:\Windows\NTDS`.
2. Log files folder: `C:\Windows\NTDS`.
3. SYSVOL folder: `C:\Windows\SYSVOL`.
4. Click **Next**.

---
## 7 - Review Options

1. Review the configuration.
2. Click **Next**.

---
## 8 - Prerequisites Check

1. Wait until validation completes.
2. Errors must be resolved before continuing.
3. Expected: *All prerequisite checks passed successfully*.
4. Click **Install**.

---
## 9 - Automatic Restart

1. The server will restart automatically.
2. Do not interrupt the process.

---
## 10 - Log On

1. After the restart, log in using: `CORP\Administrator`
2. Password: `<ADM_PASSWORD>`





