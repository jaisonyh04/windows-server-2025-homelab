## Purpose

Apply a default desktop wallpaper to domain users.

---
## 1 - Create a folder for the wallpaper

1. On `DC01`, create a folder:  `C:\Wallpapers`
2. Copy an image into it.
<img width="896" height="589" alt="image" src="https://github.com/user-attachments/assets/7265883c-64e0-466d-a76d-8e6c72f0dde4" />

---
## 2 - Share the folder

1. Right-click the `Wallpapers` folder and select **Properties**.
2. Go to the Sharing tab and click the **Advanced Sharing...** button.
3. Check the **Share this folder** box.
4. Click the **Permissions** button.
5. Remove `Everyone` group. 
6. Add: `Authenticated Users`.
7. Set the Share Permissions to `Read`.
8. Set the NTFS Permission to `Read & Execute`.

---
## 3 - Create the Desktop Wallpaper GPO

1. Open Server Manager → Tools → Group Policy Management.
2. Navigate to: `CORP` → `Users`.
3. Right-click `Users` → **Create a GPO in this domain, and Link it here...**.
4. Type `Desktop Wallpaper` and click **OK**.
5. Right-click `Desktop Wallpaper` → **Edit**.
6. Navigate to: User Configuration → Policies → Administrative Templates → Desktop → Desktop.
7. Open *Desktop Wallpaper*.
8. Configure:

```
State: Enabled
Wallpaper Name: \\DC01\Wallpapers\wallpaper.jpg
Wallpaper Style: Fill or Fit
```

9. Click **Apply** → **OK**.

---
## 4 - Prevent users from changing it

1. Navigate to User Configuration → Policies → Administrative Templates → Control Panel → Personalization.
2. Open `Prevent changing desktop background` and set it to `Enabled`.
3. Click **Apply** → **OK**.

---
## 5 - Verification

1. Log in using a domain account.
2. Verify that the corporate desktop wallpaper is applied.
3. Verify that the **Background** settings are disabled (Settings → Personalization → Background).
4. Open PowerShell and run:

```
gpresult /scope user /r
gpresult /scope computer /r
```

Expected output:

```
 Applied Group Policy Objects
    -----------------------------
        Desktop Wallpaper
```
<img width="1276" height="764" alt="image" src="https://github.com/user-attachments/assets/da043ed3-eabd-4cd4-94c1-75b0e3de20d5" />

---
### Why use a UNC (Universal Naming Convention) path?

A **UNC path** (Universal Naming Convention path) is a standardized format used in Microsoft Windows to locate and access files and shared resources (like printers or folders) on a local area network (LAN).

Unlike local file paths that rely on drive letters (e.g., `C:\Documents\file.txt`), a **UNC path** points directly to a network host and shared volume.

### Structure of a UNC Path

A UNC path always follows this syntax: `\\ServerName\ShareName\DirectoryPath\Filename.ext`

- **`\\ServerName`**: The computer, server, NAS device, or IP address hosting the resource (preceded by two backslashes).
- **`\ShareName`**: The specific folder or resource that has been shared publicly on that network device.
- **`\DirectoryPath\Filename`**: The standard subfolder path and file name leading to the final target.
