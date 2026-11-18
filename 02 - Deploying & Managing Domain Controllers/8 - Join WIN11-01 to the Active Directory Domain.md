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
6. Username: `CORP\Administrator`, Password: `P@ssword456!`.
7. Expected: Welcome to the corp.test domain.
8. Restart.
---
## 4 - Log On with a Domain Account

1. Select: `Other User`
2. Sign in using: Username: `CORP\Administrator`, Password: `P@ssword456!`.

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
## 6 - Verify Domain Connectivity

```powershell
nltest /dsgetdc:corp.test
```

Expected output:

```
  DC: \\DC01.corp.test
      Address: \\10.10.10.10
     Dom Guid: 5e56184d-991a-45aa-ae28-a0b7b4a9eab9
     Dom Name: corp.test
  Forest Name: corp.test
 Dc Site Name: Default-First-Site-Name
Our Site Name: Default-First-Site-Name
        Flags: PDC GC DS LDAP KDC TIMESERV GTIMESERV WRITABLE DNS_DC DNS_DOMAIN DNS_FOREST CLOSE_SITE FULL_SECRET WS DS_8 DS_9 DS_10 KEYLIST DS_13
The command completed successfully
```


>The command **`nltest /dsgetdc:itlab.local`** is used in Active Directory environments to locate an active **Domain Controller (DC)** for the specified domain (`itlab.local`).

### What exactly does it do?

1. **Queries the directory service (DS):** It instructs the NetLogon tool (`nltest`) to send a request to find an available Domain Controller (DC) for the `itlab.local` domain.
2. **Uses DNS and network protocols:** Queries the DNS SRV records to locate which server on the network holds the authentication and domain control roles for that domain name.

### What information does it return if successful?

When the command runs successfully on a machine joined to the domain (or one that has connectivity and the correct DNS configuration for the domain), it displays key information such as:

- **DC (Domain Controller):** The name of the responding server (for example, `\\WIN-SRV01`).
- **Address:** The IP address of the domain controller (`\\10.10.10.10`).
- **Domain GUID and Domain Name:** Confirmation of the verified domain.
- **Flags:** Features and services available on that server (such as Global Catalog server, PDC, etc.).

### What is it used for?

This is the standard quick diagnostic command to check whether a computer **has actual communication and can locate** its Active Directory server on the network. If it fails, it usually indicates a problem with DNS resolution, network connectivity, or that the computer is not properly joined to the domain.