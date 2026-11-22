### Purpose

Allow ICMP traffic for network connectivity testing.

---

## 1 - Check connectivity with the gateway

```powershell
ping 10.10.10.1
```

---
## 2 - Check Internet connectivity

```powershell
ping 1.1.1.1
```

---
## 3 - Verify DNS resolution

```powershell
Resolve-DnsName microsoft.com
```

---
## 4 - Verify client-server communication

From `DC01`:

```powershell
ping <IP WIN11-01>
```

Expected output:

```text
Request timed out.
```

---
## 5 - Enable the predefined ICMP rule (GUI)

1. Press `Win + R`.
2. Type:

```
 wf.msc
```

3. Press **Enter**.
4. Select **Inbound Rules**.
5. Find one of these rules:

- **File and Printer Sharing (Echo Request - ICMPv4-In)**.
- **Core Network Diagnostics – ICMP Echo Request (ICMPv4-In)**.

3. Right-click the rule → **Enable Rule** (Private and Domain).

---
## 6 - Repeat the test

```powershell
ping <IP WIN11-01>
```

Expected output:

```text
Pinging 10.10.10.XXX with 32 bytes of data:
Reply from 10.10.10.XXX: bytes=32 time<1ms TTL=128
Reply from 10.10.10.XXX: bytes=32 time<1ms TTL=128
Reply from 10.10.10.XXX: bytes=32 time<1ms TTL=128
Reply from 10.10.10.XXX: bytes=32 time<1ms TTL=128

Ping statistics for 10.10.10.XXX:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
```



```
WIN11-01 ───── ping ─────► DC01
WIN11-01 ◄──── ping ────── DC01
```

