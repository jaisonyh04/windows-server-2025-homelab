### Purpose

Assign a permanent IP address to `DC01`.

---
## Configure the static IP address

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

---
## Verify network connectivity

Run powershell as administrador:

```
Get-NetIPConfiguration
```

Expected output:

```
InterfaceAlias: Ethernet
IPv4 address: 10.10.10.10
IPv4DefaultGateway: 10.10.10.1
DNSServer: 10.10.10.1
```

Then:

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
