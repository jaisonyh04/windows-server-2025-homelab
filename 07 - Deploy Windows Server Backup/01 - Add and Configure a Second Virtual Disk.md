## Purpose
Add and configure a dedicated virtual disk for backup storage on `DC01`.

---
## 1 - Configure the Virtual Disk In KVM/QEMU (libvirt)

1. Shut down `DC01`.
2. Open *Virtual Machine Manager* (virt-manager).
3. Select `DC01`.
4. Open → *Show Virtual Hardware Details*.
5. Click `Add Hardware`.
6. Select *Storage*.
7. Create a new QCOW2 disk.
8. Size: 120 GB.
9. Bus Type: VirtIO.
10. Click **Finish** and start the VM.

<img width="1278" height="863" alt="image" src="https://github.com/user-attachments/assets/c343ac18-0caf-4d97-947a-caf798bc0473" />


---
## 2 - Configure the Virtual Disk in Windows Server

1. Open Server Manager → File and Storage Services → Volumes → Disks.
2. Right-click `Red Hat VirtIO` → **Bring Online**.
3. Right-click `Red Hat VirtIO` → **Initialize**.
4. Right-click `Red Hat VirtIO` → **New Volume...**.
5. This will start the *New Volume Wizard*.
6. Before you begin: Click **Next**
7. Server and Disk: Click **Next**
8. Size: Click **Next**
9. Drive Letter: `F` → **Next**
10. File Systems Settings:
 - File System: `NTFS`
 - Allocation Unit Size: `Default`
 - Volume Label: `Backup`
 - **Next**
11. Confirmation: **Create** → **Close**.
12. Verify that the new **Backup (F:)** volume appears under **Volumes** and in **File Explorer**.

