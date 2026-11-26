### Purpose

Create a private virtual network for the homelab, allowing communication between virtual machines and outbound Internet access through NAT.

---
## 1 - Create the Virtual Network

1. Open *Virtual Machine Manager* → *Edit* → *Connection Details* → *Virtual Networks*.
2. Press **Add Network** `+` to create a new network.
3. Configure:

```
Name: corp.test
Mode: NAT
Forward to: Any physical device

IPv4 configuration:

Network: 10.10.10.0/24

DHCP:
Enabled

DHCP range:
10.10.10.100
10.10.10.200
```

4. Click **Finish**.
<img width="800" height="625" alt="image" src="https://github.com/user-attachments/assets/0f6616b6-63d1-4a27-80c8-358f1632ebfc" />

---
## 2 - Verify network configuration

After deploying `DC01` run powershell as administrator:

```
Get-NetIPConfiguration
```

Example output:

```
InterfaceAlias       : Ethernet
InterfaceIndex       : 5
InterfaceDescription : Intel(R) 82574L Gigabit Network Connection
NetProfile.Name      : Network
IPv4Address          : 10.10.10.150
IPv6DefaultGateway   :
IPv4DefaultGateway   : 10.10.10.1
DNSServer            : 10.10.10.1
```

Then:

```
ipconfig /all
```

Example output:

```
Windows IP Configuration

   Host Name . . . . . . . . . . . . : DC01
   Primary Dns Suffix  . . . . . . . :
   Node Type . . . . . . . . . . . . : Hybrid
   IP Routing Enabled. . . . . . . . : No
   WINS Proxy Enabled. . . . . . . . : No
   DNS Suffix Search List. . . . . . : corp.test

Ethernet adapter Ethernet:

   Connection-specific DNS Suffix  . : corp.test
   Description . . . . . . . . . . . : Intel(R) 82574L Gigabit Network Connection
   Physical Address. . . . . . . . . : 52-54-00-14-15-62
   DHCP Enabled. . . . . . . . . . . : Yes
   Autoconfiguration Enabled . . . . : Yes
   Link-local IPv6 Address . . . . . : fe80::afe2:bb60:a8b7:1ea9%5(Preferred)
   IPv4 Address. . . . . . . . . . . : 10.10.10.150(Preferred)
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Lease Obtained. . . . . . . . . . : martes, 17 de noviembre de 2026 20:57:03
   Lease Expires . . . . . . . . . . : martes, 17 de noviembre de 2026 21:57:05
   Default Gateway . . . . . . . . . : 10.10.10.1
   DHCP Server . . . . . . . . . . . : 10.10.10.1
   DHCPv6 IAID . . . . . . . . . . . : 106058752
   DHCPv6 Client DUID. . . . . . . . : 00-01-00-01-32-8E-E6-45-52-54-00-14-15-62
   DNS Servers . . . . . . . . . . . : 10.10.10.1
   NetBIOS over Tcpip. . . . . . . . : Enabled
```

---
## 3 - Verify network connectivity

```
ping 1.1.1.1
```

Example output:

```
Pinging 1.1.1.1 with 32 bytes of data:
Reply from 1.1.1.1: bytes=32 time=2ms TTL=56
Reply from 1.1.1.1: bytes=32 time=2ms TTL=56
Reply from 1.1.1.1: bytes=32 time=2ms TTL=56
Reply from 1.1.1.1: bytes=32 time=2ms TTL=56

Ping statistics for 1.1.1.1:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 2ms, Maximum = 2ms, Average = 2ms
```
