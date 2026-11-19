## Scenario
Recurring lockout issue.

---
## 1 - Find the computer causing the issue

1. On `DC01` open `Event Viewer` (`Win` **+** `R` → `eventvwr.msc`).
2. Navigate to: *Windows Logs* → Click on *Security*.
3. In the *Actions* panel on the right side click **Filter Current Log...**.
4. Enter `Event ID 4740` → Click **OK**.

>**Event ID 4740** is generated on domain controllers, Windows Servers and Workstations everytime an account gets locket out.

5. In the event logs search for the affected user name.
6. In the `General` tab at the bottom it will show you the computer name that's causing the lockout.
<img width="1271" height="764" alt="Screenshot_20261118_233133" src="https://github.com/user-attachments/assets/51e81202-baf7-4fba-9029-1b678e576f9f" />

---
## 2 - Resolve the Issue

1. Go to the computer identified in the previous step.
2. Restart the computer to clear any existing authentication sessions.
3. Ask the user to sign in using their current password.
4. Open **Credential Manager** and remove any saved credentials that use the old password.
5. Check for applications (such as Outlook, VPN clients, or other software) that may still be configured with the old password.
6. If the user signs in on multiple devices, update the password on each device.

---
## 3 - Verify the resilution

1. Ask the user to continue working normally for several minutes.
2. On `DC01`, monitor the **Security** log for new **Event ID 4740** entries.
3. Confirm that no additional account lockout events are generated.
4. Verify that the user can continue signing in without the account becoming locked again.
