### Purpose

Deploy the primary Windows 11 client.

---
## VM Configuration

| Hardware     | Configuration                                        |
| ------------ | ---------------------------------------------------- |
| **Chipset**  | Q35                                                  |
| **Firmware** | UEFI / OVMF_CODE.secboot                             |
| **CPU**      | 4 vCPU / host-passthrough                            |
| **RAM**      | 4096 MiB                                             |
| **Disk**     | VirtIO, 120 GiB                                      |
| **Storage**  | Add Harware/Storage/CDROM device/SATA/virtio-win.iso |
| **Network**  | Virtual network `corp.test`                          |
| **Video**    | Virtio                                               |
| **Display**  | SPICE                                                |
| **TPM**      | Emulated / 2.0 / CRB                                 |
| **OS**       | Windows 11 Pro / Windows Server 2025                 |

---
## 1. Rename PC

1. Press **Win `+` I** → Home → **Rename**.
2. Type: `WIN11-01`.
3. Restart.
---
## 2. Run System File Checker (SFC)

1. Run powershell as administrador:

```
sfc /scannow
```

2. If fails run:

```
DISM /Online /Cleanup-Image /RestoreHealth
```

Run again: 

```
sfc /scannow
```

---
## 3. Time zone

1. Press **Win** `+` **I** → Time & language → Date & time.
2. Check and set the time zone correctly.
---
## 4. Verify network connectivity

- Run powershell as administrador:

```
ping 1.1.1.1
```

>Check the IP connection to the Internet.

```
Test-NetConnection download.windowsupdate.com -Port 443
```

>Check the HTTPS connection to Windows Update.

---
## 5. Install VirtIO Guest Tools

1. Open File Explorer → `This PC`.
2. Open CD Drive: `virtio-win`.
3. Run `virtio-win-guest-tools.exe`.
---
## 6. Update Windows

1. Press **Win** `+` **I** → Windows Updates.
2. `Check for updates`.
---
## 7. Verify Device Manager

- Make sure there are no important devices marked with ⚠️ or `Unknown device`.







