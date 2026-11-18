### Objective

Confirms the promotion actually succeeded before building on top of it.

---
## 1 - Check the Domain Controllers OU

1. Open: *Server Manager* → *Tools* → *Active Directory Users and Computers*.
2. Expand `corp.test` → Domain Controllers.
3. Right-click `DC01` and click **Properties**.
4. Review the settings and click **Cancel**.
5. Close the window.
---
## 2 - Check Active Directory Sites and Services

1. Open: *Server Manager* → *Tools* → *Active Directory Sites and Services*.
2. Expand Sites → Default-First-Site-Name → Servers.
3. Right-click `DC01` and click **Properties**.
4. Review the settings and click **Cancel**.
5. Close the window.
---
## 3 - Check the DNS records

1. Open: *Server Manager* → *Tools* → *DNS*.
2. Click `DC01`, then expand `DC01`.
3. Expand Forward Lookup Zones.
4. Expand `corp.test`.
5. Review the records and minimize/close the window.
