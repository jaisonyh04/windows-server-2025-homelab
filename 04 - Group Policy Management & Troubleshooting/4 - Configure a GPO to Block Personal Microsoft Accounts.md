## Purpose

Prevent users from adding or signing in with personal Microsoft accounts on domain-joined computers.

---

1. Open *Server Manager* → *Tools* → *Group Policy Management*.
2. Navigate to: `Forest: corp.tes`t → `Domains` → `corp.test` → `Corp`.
3. Right-click `Computers` OU → **Create a GPO in this domain, and Link it here...**.
4. Type `Block Personal Microsoft accounts` and click **OK**.
5. Right-click `Block Personal Microsoft accounts` → **Edit**.
6. Navigate to *Computer Configuration* → *Policies* → *Windows Settings* → *Security Settings* → *Local Policies* → *Security Options* → *Accounts: Block Microsoft accounts*.
7. Open *Accounts: Block Microsoft accounts*.
8. Select **Define this policy setting**.
9. Select **Users can't add Microsoft accounts**.
10. **Apply** → **OK**.

---
## Verification

1. Log in using a domain account.
2. Open **Settings → Accounts**.
3. Attempt to add a personal Microsoft account and verify that Windows prevents it.
4. Open PowerShell and run:

```
gpresult /scope user /r
gpresult /scope computer /r
```

Expected output:

```
 Applied Group Policy Objects
    -----------------------------
        Block Personal Microsoft accounts
```
