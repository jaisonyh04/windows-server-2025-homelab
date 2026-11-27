## Purpose
Restrict local and Remote Desktop logon rights according to security group membership and administrative responsibilities.

---
## 1 - Configure User Rights Assignment for Domain Controllers

1. Open *Server Manager* → *Tools* → *Group Policy Management*.
2. Navigate to `Forest: corp.test` → `Domains` → `corp.test`.
3. Right-click `Domain Controllers` → **Create a GPO in this domain, and Link it here...**.
4. Name the GPO `DC - User Rights Assignment`.
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
|Allow log on locally|`CORP\Domain Admins`|
|Allow log on through Remote Desktop Services|`CORP\Domain Admins`|

> [!NOTE]  
> Only members of Domain Admins are granted local and Remote Desktop logon rights on `DC01` by these settings.

---
## 2 - Configure User Rights Assignment for Workstations

1. Open *Server Manager* → *Tools* → *Group Policy Management*.
2. Navigate to `corp.test` → `Corp` → `Computers`.
3. Right-click `Desktops` → **Create a GPO in this domain, and Link it here...**.
4. Name the GPO `Workstations - User Rights Assignment`.
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

7. Configure the following policy:

|Policy|User or Group|
|---|---|
|Deny log on through Remote Desktop Services|`BUILTIN\Guests`, `CORP\GG_HR`, `CORP\GG_Finance`, `CORP\GG_Operations`|

> [!NOTE]  
> Leave Allow log on locally unconfigured in this GPO to preserve existing workstation logon rights. 
> Departmental users can continue signing in locally to `WIN11-01` for testing purposes.

> [!IMPORTANT]  
> Deny rights take precedence over corresponding allow rights. When defining a user right, review its existing assignments before replacing them.

---
## 3 - Verification

1. Ensure that Remote Desktop is enabled on the target computer before testing RDP logon.
2. Verify administrative access before testing restrictions.
3. On `DC01` and `WIN11-01`, open PowerShell as administrator and run:

```
gpupdate /force
gpresult /scope computer /r
```

4. Verify that the corresponding GPO has been applied.

|Computer|Applied GPO|
|---|---|
|DC01|DC - User Rights Assignment|
|WIN11-01|Workstations - User Rights Assignment|

5. Test local and Remote Desktop logon using the following domain accounts:

|Account|DC01 Local|DC01 RDP|WIN11-01 Local|WIN11-01 RDP|
|---|---|---|---|---|
|`CORP\jaison-admin`|Allowed|Allowed|Allowed|Allowed*|
|`CORP\jsmith`|Denied|Denied|Allowed|Existing rights*|
|`CORP\dwilson`|Denied|Denied|Allowed|Existing rights*|
|`CORP\mjohnson`|Denied|Denied|Allowed|Denied|
|`CORP\janderson`|Denied|Denied|Allowed|Denied|
|`CORP\dmiller`|Denied|Denied|Allowed|Denied|

> [!important]
> Workstation RDP access depends on existing Remote Desktop permissions and group membership.

> [!NOTE]  
> User rights assignment changes take effect during subsequent logons. 
> A computer restart is not required for these user rights changes.