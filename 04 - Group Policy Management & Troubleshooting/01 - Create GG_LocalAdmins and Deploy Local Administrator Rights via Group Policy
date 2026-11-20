## Purpose

Grant local administrator rights through Group Policy.

---
## 1 - Create GG_LocalAdmins

1. Open *Server Manager* → *Tools* → *Active Directory Users and Computers*.
2. Navigate to: `Corp` → `Groups`.
3. Right-click the `Groups` OU.
4. Select **New** → **Group**.
5. Type: `GG_LocalAdmins`.
6. Set Group scope to `Global` and Group type to `Security` → **OK**.
7. Add `jsmith`  (`GG_IT_SysAdmins`) to `GG_LocalAdmins`.

---
## 2 - Create the Group Policy

1. Open *Server Manager* → *Tools* → *Group Policy Management*.
2. Navigate to: `Forest: corp.tes`t → `Domains` → `corp.test` → `Corp`.
3. Right-click `Computers` → **Create a GPO in this domain, and Link it here...**.
4. Type `Local Admins` and click **OK**.****
5. Right-click `Local Admins` → **Edit**.
6. Navigate to: *Computer Configuration* → *Preferences* → *Control Panel Settings* → Local Users and Groups.
7. Right-click *Local Users and Groups* → **New** → **Local Group**.
8. Configure:

```
Action: Update
Group Name: Administrators (built-in)
Members: CORP\GG_LocalAdmins
```

9. Click **OK** → **OK**.
10. Close the Group Policy Management Editor.

---
## 3 - Test delegated permissions

1. On `WIN11-01` sign in as: `CORP\jsmith`.
2. Run Command Prompt and type:

```
whoami /groups
```

Expected output:

```
BUILTIN\Administrators
```

3. Click **Win** and type: `cmd`
4. `Command Prompt` → `Run as administrator`.

Instead of asking for administrator credentials, Windows should display the standard UAC confirmation dialog:

```
Do you want to allow this app to make changes to your device?

        Yes      No
```

>This confirms `jsmith` is a local administrator on `WIN11-01`.

> [!NOTE]
> Signing out and signing back in as `CORP\jsmith` rebuilds the user's logon token.

