## Purpose

Identify and resolve common Group Policy processing issues on domain-joined computers using built-in Windows troubleshooting tools.

---
## 1 - Verify the Resultant Set of Policy (RSoP)

On the affected computer, run:

```
gpresult /scope user /r
gpresult /scope computer /r
```

Run the user-scope command as the affected user and the computer-scope command with administrative privileges.

Verify that:

- The expected GPO appears under **Applied Group Policy Objects**.
- The GPO has not been filtered out.
- The policy applies to the intended user or computer.

To generate a detailed report:

```
gpresult /h "$env:TEMP\GPReport.html" /f
```

---
## 2 - Verify the GPO configuration

Open Group Policy Management and verify that:

1. The user or computer object is located in the correct OU.
2. The GPO is linked to the correct OU.
3. **Link Enabled** is enabled.
4. The relevant User or Computer Configuration settings are enabled.
5. Security Filtering and Delegation permissions are correctly configured.
6. No conflicting GPO overrides the expected setting.

---
## 3 - Check Group Policy event logs

On the affected computer, open Event Viewer and navigate to:

```
Event Viewer
└── Applications and Services Logs
    └── Microsoft
        └── Windows
            └── GroupPolicy
                └── Operational
```

Review recent Group Policy processing warnings and errors.

---
## 4 - Refresh Group Policy

After correcting any configuration issues, run:

```
gpupdate /force
```

Restart the computer or sign out and sign back in if required by the configured policy.

---
## 5 - Verify the resolution

1. Run `gpresult` again to verify that the expected GPO has been applied.
2. Test the actual policy functionality.
3. Verify that the identified Group Policy processing errors no longer occur.