### Objective

Uses PowerShell commands to confirm the promotion actually succeeded.

---
## 1 - Report domain controller diagnostic errors

```
dcdiag /q
```

---
## 2 - Perform detailed DNS diagnostics

```
dcdiag /test:DNS /v
```

---
## 3 - Verify SYSVOL and NETLOGON shares

```
net share
```

---
## 4 - Identify FSMO role holders

```
netdom query fsmo
```

---
## 5 - Verify domain configuration

```
Get-ADDomain
```

---
## 6 - Verify forest configuration

```
Get-ADForest
```

---
## 7 - Verify time synchronization

```
w32tm /query /status
```

