## Purpose
Assign and restrict user rights to enhance security.

---
## 1 - Define the User Rights Assignment Strategy

| Account           | DC01 logon                          | WIN11-01 logon |
| ----------------- | ----------------------------------- | -------------- |
| `jaison-admin`    | Allowed                             | Allowed        |
| `GG_IT_SysAdmins` | Denied by absence of an allow right | Allowed        |
| `GG_IT_HelpDesk`  | Denied by absence of an allow right | Allowed        |
| `GG_HR`           | Not allowed                         | Not allowed    |
| `GG_Finance`      | Not allowed                         | Not allowed    |
| `GG_Operations`   | Not allowed                         | Not allowed    |

> [!NOTE]
> `WIN11-01` is the IT Administrator Workstation, this proposed configuration restricts interactive access to IT personnel.


---
## 2 - Define the GPO Structure

Create two separate GPOs instead of modifying the Default Domain Policy or Default Domain Controllers Policy.

```
corp.test
│
├── Domain Controllers
│   ├── DC01
│   └── GPO: DC - User Rights Assignment
│
└── Corp
    └── Computers
        └── Desktops
            ├── WIN11-01
            └── GPO: Workstations - User Rights Assignment
```

> [!NOTE]
> User Rights Assignment is a **Computer Configuration** policy. Therefore, the GPOs must be linked to the OUs containing the computer objects, not the user accounts.

---
## 3 - Configure User Rights Assignment for Domain Controllers

1. On `WIN11-01`, sign in as `jaison-admin@corp.test`.
2. Open **Group Policy Management** (`gpmc.msc`).
3. Navigate to `corp.test` → `Domain Controllers`.
4. Right-click → **Create a GPO in this domain, and Link it here...**
5. Enter: `DC - User Rights Assignment`.
6. Right-click the GPO → **Edit**.
7. Navigate to:

```
Computer Configuration
└── Policies
    └── Windows Settings
        └── Security Settings
            └── Local Policies
                └── User Rights Assignment
```

8. Configure the following policies:

|Policy|User or Group|
|---|---|
|Allow log on locally|`BUILTIN\Administrators`|
|Allow log on through Remote Desktop Services|`BUILTIN\Administrators`|
|Deny log on locally|`BUILTIN\Guests`|
|Deny log on through Remote Desktop Services|`BUILTIN\Guests`|

> [!IMPORTANT]
> Do not restrict **Access this computer from the network** to administrators. `DC01` also provides Active Directory, DNS and SMB File Shares. Incorrectly restricting network logon could disrupt domain operations and access to shared resources.

---
## 4 - Configure User Rights Assignment for Workstations

1. Open **Group Policy Management**.
2. Navigate to: `corp.test` → `Corp` → `Computers` → `Desktops`.
3. Right-click → **Create a GPO in this domain, and Link it here...**
4. Enter: `Workstations - User Rights Assignment`.
5. Edit the GPO and navigate to **User Rights Assignment**.
6. Configure:

|Policy|User or Group|
|---|---|
|Allow log on locally|`BUILTIN\Administrators`, `CORP\GG_IT_SysAdmins`, `CORP\GG_IT_HelpDesk`|
|Allow log on through Remote Desktop Services|`BUILTIN\Administrators`|
|Deny log on locally|`BUILTIN\Guests`|
|Deny log on through Remote Desktop Services|`BUILTIN\Guests`|

> [!NOTE]
> Configuring a user right replaces its previous assignment list. 
> It does not simply append additional groups. 
> Explicit deny rights also take precedence over corresponding allow rights.

---
## 5 - Apply and Verify the Group Policies

Before applying the policies, ensure that you have working administrative access through the KVM console.

On both `DC01` and `WIN11-01`, run PowerShell as Administrator:

```
gpupdate /force
```

Verify that the corresponding GPO has been applied:

```
gpresult /scope computer /r
```

