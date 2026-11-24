## Problem
Windows Server Backup failed to open on `DC01` with the following error:
`A fatal error occurred during a Windows Server Backup snap-in operation. The server threw an exception.`

---
## 1 - Reset the Backup Catalog

Open powershell as administrator and run: 

```powershell
wbadmin delete catalog
```

## 2 - Reconfigure the schedule

1. In the *Actions* panel click **Backup Schedule...**.
2. This will start the *Backup Schedule Wizard* Click **Next**.
3. Select Backup Configuration: **Full Server** → **Next**.
4. Specify Backup Time: `Once a day 21:00` → **Next**.
5. Specify Destination Type: `Back up to a hard disk that is dedicated for backups` → **Next**.
6. Select Destination Disk: Click **Show All Available Disk...**.
7. Select `Red Hat VirtIO SCSI Disk` → **OK**.
8. Confirmation: Click **Finish**.

---
## 3 - Run a Backup

1. In the *Actions* panel click **Backup Once...**.
2. Backup Options: *Scheduled backup options*.
3. Click **Next** → **Backup**.
4. Verify that the backup completes successfully.