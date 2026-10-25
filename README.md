# Active Directory & Enterprise IT Support Home Lab

## 📌 Project Overview
This project demonstrates the design, deployment, and administration of a virtualized Windows Server Active Directory enterprise network. Built using VMware Workstation, this lab models a corporate IT infrastructure featuring centralized domain management, role-based access control (RBAC), network file sharing with NTFS/Share permissions, automated Group Policy Objects (GPOs), and IT Service Management (ITSM) ticketing using Jira.

---

## 🏗 Network & Lab Architecture

### Environment Details
* **Hypervisor:** VMware Workstation
* **Domain Controller:** Windows Server 2019 Datacenter (`TechWorld.com` / `SHIINE`)
* **Client Operating System:** Windows 10 Enterprise
* **IP Scheme:** Static IP (`192.168.1.129/24`) for Domain Controller & Preferred DNS
* **Security & Testing OS:** Kali Linux

---

## 🛠️ Implementation & Technical Tasks

### 1. Active Directory Domain Services (AD DS) Setup
* Installed and configured **Active Directory Domain Services (AD DS)** and **DNS Server** roles on Windows Server 2019.
* Configured the forest root domain: `TechWorld.com`.
* Assigned a static IP address (`192.168.1.129`) to the Domain Controller and directed network interfaces to use it as the primary DNS server.
* Verified domain connectivity using `nslookup` and `ping` commands from Windows 10 client machines.

### 2. Organizational Structure & User Management
Designed a structured Active Directory layout reflecting departmental hierarchy:
* **OU Structure:** Created Organizational Units (OUs) for geographical and functional divisions (e.g., `Deutschland`, `IT-Support`, `Sales`).
* **Role-Based Access Control (RBAC):** Created targeted Security Groups (`IT-Support-Users`, `Sales`) rather than assigning permissions directly to individual users.
* **User Onboarding:**
  * Provisioned domain users (e.g., `Anna` as IT Support Department Manager, `Alisa` in Sales).
  * Enforced initial logon password changes and domain profile setups.

### 3. Network File Sharing & Security Permissions
Implemented network file shares with secure privilege segregation on dedicated storage volumes (`CompanyShares E:`):
* **Sales Share (`\\SHIINE\Sales`):** Configured with Share and NTFS permissions granting Read/Write access strictly to members of the `Sales` security group.
* **IT-Support Share (`\\SHIINE\IT-Support`):** Secured with Modify and Read/Execute permissions restricted to `IT-Support-Users`.
* **Verification:** Logged into client nodes as specific domain users (`techworld\alisa`, `techworld\anna`) to confirm proper grant/deny authorization behavior.

### 4. Group Policy Management (GPO)
Created and enforced targeted GPOs to strengthen system security and restrict unauthorized configuration changes:
* **Password Security Policy:**
  * Minimum password length: 8 characters.
  * Maximum password age: 60 days.
  * Password complexity requirements: Enabled.
* **Sales Desktop Restriction GPO:**
  * Enforced **"Prohibit access to Control Panel and PC settings"** linked to the `Sales` OU.
  * Verified policy propagation on client endpoints using `gpupdate /force` and confirmed restrictions via user session error prompts.

### 5. Helpdesk Operations & ITSM Documentation (Jira)
Simulated real-world Level 1/2 IT Support workflow operations:
* Handled password resets and account unlock requests for domain users.
* Maintained ticket logging, categorization, prioritization, and resolution documentation within Jira to align with ITSM best practices.

---

## 🧪 Verification & Testing Results

| Test Scenario | Executed Command / Action | Expected Result | Outcome |
| :--- | :--- | :--- | :--- |
| **Domain Join** | System Properties -> Join `TechWorld.com` | "Welcome to the TechWorld.com domain" message | **PASS** |
| **DNS Resolution** | `nslookup TechWorld.com` | Resolves to IP `192.168.1.129` | **PASS** |
| **User Identity** | `whoami` | Displays `techworld\alisa` or `techworld\anna` | **PASS** |
| **File Access Control** | Access `\\SHIINE\Sales` as `techworld\alisa` | Access granted; file creation successful (`Alisa2026.txt`) | **PASS** |
| **GPO Restriction** | Open Control Panel as `techworld\alisa` | Blocked by system restriction message | **PASS** |

---

## 💡 Key Takeaways & Skills Demonstrated
* **System Administration:** Windows Server 2019 configuration, AD DS, DNS, GPO management.
* **Network Security:** Principle of least privilege, NTFS vs. Share permissions, Group Policies.
* **Client Troubleshooting:** Windows 10 domain joining, network folder mapping, command-line diagnostics (`whoami`, `ping`, `nslookup`, `gpupdate`).
* **ITSM Processes:** Incident handling and ticketing workflows in Jira.
