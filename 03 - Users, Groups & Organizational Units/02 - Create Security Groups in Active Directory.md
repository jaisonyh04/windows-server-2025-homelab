### Objective

Organize users and manage permissions through security groups.

---
## 1 - Create the Global Groups (Users)

>A Global Group represents **who** people are.
>Membership in these groups defines a user's **department or role**.


1. Open Server Manager → Tools → Active Directory Users and Computers.
2. Navigate to: `corp.test` → `CORP` → `Groups`.
3. Right-click the `Global` OU → **New** → **Group**.
4. Give it a name, set Group scope to `Global` and Group type to `Security`, click **OK**.
5. Create the following groups:

| Group Name    |
| ------------- |
| GG_ITAdmins   |
| GG_HelpDesk   |
| GG_HR         |
| GG_Finance    |
| GG_Operations |

---
## 2 - Assign User Membership

1. Double-click on a group.
2. Go to the `Members` tab → **Add...**.
3. Type the user logon name → **Check names** → **OK**.
4. Add the rest of the members → **Apply** → **OK**.
5. Add users to their corresponding Golbal Security Groups:

| Group Name    | Members               |
| ------------- | --------------------- |
| GG_ITAdmins   | jsmith / abrown       |
| GG_HelpDesk   | dwilson / slee        |
| GG_HR         | mjohnson / edavis     |
| GG_Finance    | janderson / smartinez |
| GG_Operations | dmiller / ogarcia     |

---
## 3 - Create the Domain Local Groups (Permissions)

>A **Domain Local Group** represents **what resource can be accessed**.

1. Open Server Manager → Tools → Active Directory Users and Computers.
2. Navigate to: `corp.test` → `CORP` → `Groups`.
3. Right-click the `Domain Local` OU → **New** → **Group**.
4. Give it a name, set Group scope to `Domain Local` and Group type to `Security`, click **OK**.
5. Create the following groups:

| Group Name                 |
| -------------------------- |
| DL_ITAdmins_Share_Change   |
| DL_HelpDesk_Share_Change   |
| DL_HR_Share_Change         |
| DL_Finance_Share_Change    |
| DL_Operations_Share_Change |

---
## 4 - Configure Group Nesting

1. Right-click the `GG_ITAdmins` global group → **Add to a group...**.
2. Write `dl` → **Check Names**.
3. Select `DL_ITAdmins_Share_Change` → **OK** → **OK**.
4. Add each Global Group to its corresponding Domain Local Group.

| Global Group  | Member of                  |
| ------------- | -------------------------- |
| GG_ITAdmins   | DL_ITAdmins_Share_Change   |
| GG_HelpDesk   | DL_HelpDesk_Share_Change   |
| GG_HR         | DL_HR_Share_Change         |
| GG_Finance    | DL_Finance_Share_Change    |
| GG_Operations | DL_Operations_Share_Change |

---

### **5 - Verify Group Membership**

1. Open Server Manager → Tools → Active Directory Users and Computers.
2. Navigate to `corp.test` → `CORP` → `Groups`.
3. Open `DL_ITAdmins_Share_Change`.
4. Verify that `GG_ITAdmins` appears under the `Members` tab.

