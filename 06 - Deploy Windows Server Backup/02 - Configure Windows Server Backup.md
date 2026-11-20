## Purpose
Install and configure Windows Server Backup on `DC01` to create scheduled backups of the Domain Controller.

---
## 1 - Install Windows Server Backup

1. Open *Server Manager* → *Manage*→ *Add Roles and Features*.
2. Click **Next** until *Features*.
3. Select: *Windows Server Backup*.
4. Click **Next** → **Install**.
5. Wait for the installation to finish → **Close**.

---
## 2 - Configure Windows Server Backup

1. Open: *Server Manager* → *Tools* → *Windows Server Backup*.
2. Select *Local Backup*.
3. In the *Actions* panel click **Backup Schedule...**.
4. This will start the *Backup Schedule Wizard* Click **Next**.
5. Select Backup Configuration: **Full Server** → **Next**.
6. Specify Backup Time: `Once a day 22:00` → **Next**.
7. Specify Destination Type: `Back up to a hard disk that is dedicated for backups` → **Next**.
8. Select Destination Disk: Click **Show All Available Disk...**, select Volume `F:\` → **OK**.
9. Confirmation: Click **Finish**.
>When you configure Windows Server Backup, if you choose "Back up to a hard disk that is dedicated for backups", Windows will reserve that disk exclusively for backups and may remove its drive letter automatically. This is expected behavior.
---
## 3 - Run the First Backup

1. In the *Actions* panel click **Backup Once...**.
2. Backup Options: *Scheduled backup options*.
3. Click **Next** → **Backup**.
4. Verify that the backup completes successfully.
