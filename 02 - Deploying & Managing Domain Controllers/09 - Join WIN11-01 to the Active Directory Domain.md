### Purpose

Join the client to the `corp.test` domain.

---
## 1 - Configure DNS Server

1. Open: *Settings* → *Network & internet* → *Advanced network settings*.
2. Click **Ethernet** → **More adapter options** → **Edit**.
3. Select **Internet Protocol Version 4 (TCP/IPv4)** → **Properties**.
4. Select **Use the following DNS server addresses** and enter:

```
Preferred DNS server: 10.10.10.10
```

5. Click **OK** → **Close**.
6. Run powershell as administrador:

```
Get-NetIPConfiguration
```

Expected output:

```
InterfaceAlias       : Ethernet
InterfaceIndex       : 5
InterfaceDescription : Intel(R) 82574L Gigabit Network Connection
NetProfile.Name      : Network
IPv4Address          : 10.10.10.185
IPv6DefaultGateway   :
IPv4DefaultGateway   : 10.10.10.1
DNSServer            : 10.10.10.10
```

---
## 2 - Verify DNS Resolution

Run powershell as administrador:

```powershell
Resolve-DnsName corp.test
```

Expected output:

```
Name                                           Type   TTL   Section    IPAddress
----                                           ----   ---   -------    ---------
corp.test                                      A      600   Answer     10.10.10.10
```

---
## 3 - Join the Domain

1. Open: Settings → System → About → **Domain or workgroup**.
2. Click **Change...**.
3. Select: Domain.
4. Enter: `corp.test`.
5. Click **OK**.
6. Username: `jaison-admin@corp.test`, Password: `XXXXXXXXXXX!`.
7. Expected: Welcome to the corp.test domain.
8. Restart.
---
## 4 - Log On with a Domain Account

1. Select: `Other User`
2. Sign in using: Username: `jaison-admin@corp.test`, Password: `XXXXXXXXXXX!`.

---
## 5 - Verify Domain Membership

1. Open: Settings → System → About → **Domain or workgroup**.
2. Run powershell as administrador:

```
systeminfo
```

or:

```powershell
Get-ComputerInfo |
Select CsDomain, CsPartOfDomain
```

Expected output:

```
CsDomain    CsPartOfDomain
--------    --------------
corp.test             True
```

---
## 6 - Move WIN11-01 to the correct OU [IMPORTANT]

1. On `DC01`, open *Server Manager* → *Tools* → *Active Directory Users and Computers*.
2. Navigate to: `corp.test` → `Computers` (This is the default container).
3. Right-click `WIN11-01` → **Move...**.
4. Select: `corp` → `Corp` → `Computers` → `Desktops`.
5. Double-click `WIN11-01` and enter a description.

---
## 7 - Verify Connectivity with the Domain

1. Open powershell and run: 

```
ping DC01
```

Expected Output:

```
PS C:\WINDOWS\system32> ping DC01

Pinging dc01.corp.test [10.10.10.10] with 32 bytes of data:
Reply from 10.10.10.10: bytes=32 time<1ms TTL=128
Reply from 10.10.10.10: bytes=32 time=1ms TTL=128
Reply from 10.10.10.10: bytes=32 time<1ms TTL=128
Reply from 10.10.10.10: bytes=32 time<1ms TTL=128

Ping statistics for 10.10.10.10:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 1ms, Average = 0ms
```

