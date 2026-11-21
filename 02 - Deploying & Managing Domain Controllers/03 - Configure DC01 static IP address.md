### Purpose

Assign a permanent IP address to `DC01`.

> [!IMPORTANT]
> A Domain Controller requires a static IP address because all domain clients depend on it for DNS, authentication, and Active Directory services. If the IP address changes, clients may be unable to locate the Domain Controller, causing logon failures, Group Policy issues, and other domain service disruptions. A static IP ensures the server is always reachable at the same address.

---
## 1 - Configure the static IP address

1. Open: *Settings* → *Network & internet* → *Advanced network settings*.
2. Click **Ethernet** → **More adapter options** → **Edit**.
3. Select **Internet Protocol Version 4 (TCP/IPv4)** → **Properties**.
4. Select **Use the following IP address** and enter:

```
IP address: 10.10.10.10
Subnet mask: 255.255.255.0
DefaultGateway: 10.10.10.1
Preferred DNS server: 10.10.10.1   ← temporal
```

5. Click **OK** → **Close**.
<img width="1052" height="680" alt="image" src="https://github.com/user-attachments/assets/69982443-77f3-4d61-a0a6-edcdf1d8c444" />

---
## 2 - Verify Network Configuration

Run powershell as administrador:

```
Get-NetIPConfiguration
```

Expected output:

```
InterfaceAlias       : Ethernet
InterfaceIndex       : 4
InterfaceDescription : Intel(R) 82574L Gigabit Network Connection
NetProfile.Name      : Network
IPv4Address          : 10.10.10.10
IPv6DefaultGateway   :
IPv4DefaultGateway   : 10.10.10.1
DNSServer            : 10.10.10.1
```

---
## 3 - Verify Network Connectivity


```
Test-NetConnection 10.10.10.1
```

>Test connectivity.


```
Test-NetConnection 1.1.1.1
```

>Tests outbound network connectivity from your machine to Cloudflare's public DNS server (`1.1.1.1`).


```
Resolve-DnsName microsoft.com
```

>Confirms that the server can successfully query a DNS server and translate domain names into IP addresses.
