### Objective

Verify that `DC01` was successfully promoted to a Domain Controller and that essential Active Directory services are operational.

---
Run the following commands in an elevated PowerShell session on `DC01`:

## 1 - Report domain controller diagnostic errors

```
dcdiag /q
```

Expected result: No errors reported.

---
## 2 - Perform detailed DNS diagnostics

```
dcdiag /test:DNS /v
```

Expected result: Relevant DNS tests pass.

---
## 3 - Verify SYSVOL and NETLOGON shares

```
net share
```

Expected result: `SYSVOL` and `NETLOGON` are present.

---
## 4 - Identify FSMO role holders

```
netdom query fsmo
```

Expected result: All five roles are held by `DC01.corp.test`.

---
## 5 - Verify domain configuration

```
Get-ADDomain
```

Expected result: `DNSRoot: corp.test`, `NetBIOSName: CORP`, `DomainMode: Windows2025Domain`.

---
## 6 - Verify forest configuration

```
Get-ADForest
```

Expected result: `RootDomain: corp.test`, `ForestMode: Windows2025Forest`.

---
## 7 - Verify time synchronization

```
w32tm /query /status
```

Expected result: Valid time source and recent successful synchronization.

---
## 8 - Verify time source

```
w32tm /query /source
```

If the output is `Local CMOS Clock` or `Free-running System Clock`, Configure an external NTP source:

```
w32tm /config /manualpeerlist:"0.pool.ntp.org,0x8 1.pool.ntp.org,0x8 2.pool.ntp.org,0x8" /syncfromflags:manual /reliable:yes /update
```

### Final verification

Run:

```
w32tm /query /configuration
```

Expected:

```
Type: NTP (Local)
NtpServer: 0.pool.ntp.org,0x8 1.pool.ntp.org,0x8 2.pool.ntp.org,0x8 (Local)
```

Then:

```
w32tm /query /peers
```

Expected: Three configured NTP peers.

---
## 9 - Verify critical Active Directory services

```
Get-Service NTDS,DNS,Netlogon,DFSR,KDC,W32Time
```

Expected result:

```
Status   Name               DisplayName
------   ----               -----------
Running  DFSR               DFS Replication
Running  DNS                DNS Server
Running  KDC                Kerberos Key Distribution Center
Running  Netlogon           Netlogon
Running  NTDS               Active Directory Domain Services
Running  W32Time            Windows Time
```

---
## 10 - Verify Active Directory DNS SRV records

```
Resolve-DnsName -Name _ldap._tcp.dc._msdcs.corp.test -Type SRV
```

Expected: An SRV record pointing to `dc01.corp.test` on port 389.

---
## 11 - Verify external DNS resolution

```
Resolve-DnsName microsoft.com -Server 10.10.10.10
```

Example output:

```
Name                                           Type   TTL   Section    IPAddress
----                                           ----   ---   -------    ---------
microsoft.com                                  AAAA   696   Answer     2603:1061:14:76::1
microsoft.com                                  A      84    Answer     150.171.109.119
```

