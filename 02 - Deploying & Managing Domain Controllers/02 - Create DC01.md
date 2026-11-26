### Purpose

Deploy the primary Domain Controller.

---
## VM Configuration

| Hardware     | Configuration                                                |
| ------------ | ------------------------------------------------------------ |
| **Chipset**  | Q35                                                          |
| **Firmware** | UEFI / OVMF_CODE.secboot                                     |
| **CPU**      | 4 vCPU/host-passthrough                                      |
| **RAM**      | 6144 MiB                                                     |
| **Disk**     | VirtIO, 120 GiB                                              |
| **Storage**  | Add Harware/Storage/CDROM device/SATA/virtio-win.iso         |
| **Network**  | Virtual network `corp.test`                                  |
| **Video**    | Virtio                                                       |
| **Display**  | SPICE                                                        |
| **TPM**      | No                                                           |
| **OS**       | Windows Server 2025 Standard Evaluation (Desktop Experience) |

> [!NOTE]
> During Windows Server installation, if the virtual disk is not detected, select **Load driver**, browse the VirtIO driver ISO, and load the appropriate storage driver for the configured virtual storage controller.
> The `viostor` driver is used for VirtIO block storage, while `vioscsi` is used for VirtIO SCSI.

---
## 1. Rename PC

1. Press **Win `+` I** → **Home** → **Rename**.
2. Type: `DC01`.
3. Restart.
---
## 2. Verify Time zone

1. Press **Win** `+` **I** → Time & language → Date & time.
2. Check and set the time zone correctly.

---
## 3. Verify network connectivity

- Run powershell as administrador:

```
ping 1.1.1.1
```

>Check the IP connection to the Internet.

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

---
## 4. Install VirtIO Guest Tools

1. Open File Explorer → `This PC`.
2. Open CD Drive: `virtio-win`.
3. Run `virtio-win-guest-tools.exe`.

---
## 5. Update Windows

1. Press **Win** `+` **I** → Windows Updates.
2. `Check for updates`.

---
## 6. Verify Device Manager

- Make sure there are no important devices marked with ⚠️ or `Unknown device`.





