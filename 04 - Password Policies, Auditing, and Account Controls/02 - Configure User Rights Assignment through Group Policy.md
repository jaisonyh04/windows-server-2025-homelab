## Purpose
Assign and restrict user rights to enhance security.

---
## 1 - Define the User Rights Assignment Strategy

|Account / Group|DC01 Local Logon|WIN11-01 Local Logon|
|---|---|---|
|`jaison-admin`|Allowed|Allowed|
|`GG_IT_SysAdmins`|Not allowed|Allowed|
|`GG_IT_HelpDesk`|Not allowed|Allowed|
|`GG_HR`|Not allowed|Not allowed|
|`GG_Finance`|Not allowed|Not allowed|
|`GG_Operations`|Not allowed|Not allowed|

Remote Desktop logon is restricted to members of the respective Administrators group.

> [!NOTE]  
> `WIN11-01` is a dedicated IT Administrator Workstation. Testing policies with non-IT user accounts requires temporarily adjusting the workstation logon restrictions.

---
## 2 - Configure User Rights Assignment for Domain Controllers

1. Open *Group Policy Management* (`gpmc.msc`).
2. Navigate to: `Forest: corp.test` → `Domains` → `corp.test`.
3. Right-click `Domain Controllers` → **Create a GPO in this domain, and Link it here...**.
4. Type `DC - User Rights Assignment` and click **OK**.
5. Right-click the GPO → **Edit**.
6. Navigate to:

```
Computer Configuration
└── Policies
    └── Windows Settings
        └── Security Settings
            └── Local Policies
                └── User Rights Assignment
```

7. Configure the following policies:

|Policy|User or Group|
|---|---|
|Allow log on locally|`BUILTIN\Administrators`|
|Allow log on through Remote Desktop Services|`BUILTIN\Administrators`|
|Deny log on locally|`BUILTIN\Guests`|
|Deny log on through Remote Desktop Services|`BUILTIN\Guests`|

> [!IMPORTANT]  
> Do not restrict **Access this computer from the network** to administrators. DC01 provides Active Directory, DNS and SMB file-sharing services.

---
## 3 - Configure User Rights Assignment for Workstations

1. Open *Group Policy Management*.
2. Navigate to: `corp.test` → `Corp` → `Computers`.
3. Right-click `Desktops` → **Create a GPO in this domain, and Link it here...**.
4. Type `Workstations - User Rights Assignment` and click **OK**.
5. Right-click the GPO → **Edit**.
6. Navigate to **User Rights Assignment**.
7. Configure the following policies:

|Policy|User or Group|
|---|---|
|Allow log on locally|`BUILTIN\Administrators`, `CORP\GG_IT_SysAdmins`, `CORP\GG_IT_HelpDesk`|
|Allow log on through Remote Desktop Services|`BUILTIN\Administrators`|
|Deny log on locally|`BUILTIN\Guests`|
|Deny log on through Remote Desktop Services|`BUILTIN\Guests`|

> [!NOTE]  
> Configuring a user right replaces its previous assignment list. Explicit deny rights take precedence over corresponding allow rights.

---
## 4 - Verification

> [!IMPORTANT]  
> Before applying the GPOs, verify that your administrative account has the required logon rights and maintain an active administrative session.

1. On both `DC01` and `WIN11-01`, open PowerShell as administrator and run:

```
gpupdate /force
gpresult /scope computer /r
```

2. Verify that the corresponding GPO has been applied:

|Computer|Applied Group Policy Object|
|---|---|
|`DC01`|`DC - User Rights Assignment`|
|`WIN11-01`|`Workstations - User Rights Assignment`|

3. Test local logon using the following domain accounts:

|Account|DC01|WIN11-01|
|---|---|---|
|`CORP\jaison-admin`|Allowed|Allowed|
|`CORP\jsmith`|Not allowed|Allowed|
|`CORP\dwilson`|Not allowed|Allowed|
|`CORP\mjohnson`|Not allowed|Not allowed|
4. If Remote Desktop is enabled, verify that only members of the respective Administrators group can establish RDP sessions.

> [!NOTE]  
> User rights assignment changes take effect during subsequent logons. A computer restart is generally not required.