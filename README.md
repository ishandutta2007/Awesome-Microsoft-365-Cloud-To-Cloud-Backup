# Awesome-Microsoft-365-Cloud-To-Cloud-Backup

# Awesome Microsoft 365 Cloud-to-Cloud Backup

> A curated list of top Microsoft 365 Cloud-to-Cloud Backup platforms — both SaaS/Hosted commercial solutions and open-source alternatives for protecting Exchange Online, SharePoint Online, OneDrive for Business, and Microsoft Teams data.
> 🌟 Star this repo if you find it useful! 🌟

---

## 📋 Table of Contents

- [SaaS / Hosted Platforms](#-saas--hosted-platforms)
  - [Druva Microsoft 365 Backup](#druva-microsoft-365-backup)
  - [Veeam Backup for Microsoft 365](#veeam-backup-for-microsoft-365)
  - [Keepit for M365](#keepit-for-m365)
  - [AvePoint Cloud Backup](#avepoint-cloud-backup)
  - [Commvault Cloud for M365](#commvault-cloud-for-m365)
  - [Rubrik (via Sophos)](#rubrik-via-sophos)
- [Open-Source Software](#-open-source-software)
  - [BackupZit](#backupzit)
  - [mailvault](#mailvault)

---

## 🟦 SaaS / Hosted Platforms

Commercial, cloud-hosted Microsoft 365 Cloud-to-Cloud Backup platforms. These are not open-source but are included as reference points for feature comparison.

**Important context:** Microsoft's native Microsoft 365 Backup service is a **pay-as-you-go add-on** priced at **$0.15 per GB per month** of protected content, covering Exchange, OneDrive, and SharePoint, with free restores and no annual contract [citation:1][citation:8]. Standard Microsoft 365 licenses **do not include a full backup solution** .

### Druva Microsoft 365 Backup
**Type:** Fully managed SaaS backup with air-gapped cloud storage
Druva provides agentless, fully managed backup for Microsoft 365 including Exchange, OneDrive, SharePoint, and Teams, with immutable air-gapped storage in the Druva Cloud. The platform eliminates infrastructure management entirely, with granular recovery of files, folders, mailboxes, or entire sites.

### Veeam Backup for Microsoft 365
**Type:** Self-managed backup with a free Community Edition
Veeam provides comprehensive backup for Exchange Online, SharePoint Online, OneDrive for Business, and Microsoft Teams. A key differentiator is the **Community Edition**, which is **free for up to 10 users, 10 teams, and 1 TB of SharePoint data**, with no time limit and no feature restrictions [citation:3][citation:9][citation:12]. **Important:** The Veeam EULA prohibits using the Community Edition to provide services to third parties (e.g., as an MSP) [citation:12]. The paid edition removes these limits for larger organizations.

### Keepit for M365
**Type:** Independent, vendor-neutral cloud backup
Keepit provides automated, immutable backups for Microsoft 365, storing data in its own independent cloud infrastructure rather than the Microsoft tenant. This vendor-neutral architecture is positioned as essential because SaaS providers operate under a shared responsibility model and typically do not offer comprehensive built-in backup.

### AvePoint Cloud Backup
**Type:** Multi-SaaS backup with flexible storage options
AvePoint provides automated backup for Microsoft 365, Google Workspace, and Salesforce, with a centralized command center for managing backup health. Storage options include AvePoint's Azure storage or your private cloud, with compliance certifications including SOC 2 Type II, ISO 27001, and FedRAMP.

### Commvault Cloud for M365
**Type:** Cyber-resilient M365 protection with air-gap
Commvault Cloud extends its enterprise data protection platform to Microsoft 365, providing backup, recovery, and compliance capabilities. The platform includes AI-powered threat detection and air-gapped immutable copies for ransomware recovery, suited for organizations already using Commvault for centralized data protection.

### Rubrik (via Sophos)
**Type:** Air-gapped M365 backup integrated into Sophos Central
Sophos Backup and Recovery Powered by Rubrik provides Microsoft 365 protection covering Exchange Online, OneDrive, SharePoint, and Teams, managed within Sophos Central alongside threat detection and response [citation:4]. Key capabilities include **air-gapped, WORM-locked immutable backups** with customer-controlled encryption, and fast granular or bulk recovery to original or alternate users [citation:4]. This integration is available as an add-on for Sophos customers, eliminating the need for separate tools [citation:4].

---

## 🟩 Open-Source Software

Self-hosted, community-driven Microsoft 365 Cloud-to-Cloud Backup tools. The open-source ecosystem for **full M365 backup** is **extremely limited**, with only a handful of projects providing production-oriented functionality.

### BackupZit
**Stack:** Linux agent / Microsoft Graph API | **License:** AGPLv3 (free and open source) [citation:14]
BackupZit is a **free and open-source, self-hosted Microsoft 365 backup solution** with no per-user licensing [citation:14]. Key characteristics:
- **Read-only access via Microsoft Graph**: Uses an Entra ID app registration with read-only permissions (Mail.Read, Files.Read.All, Sites.Read.All, Calendars.Read, Contacts.Read), so nothing in the tenant is changed or deleted [citation:14]
- **Full workload coverage**: Exchange Online mailboxes, OneDrive, SharePoint sites, calendars, and contacts [citation:14]
- **Self-hosted storage**: Data lands on your own NAS, server, S3 bucket, Azure Blob, or SFTP/SMB share—the only cost is your storage [citation:14]
- **Encryption and deduplication**: AES-256 encryption on the agent before data leaves, with deduplication and retention policies [citation:14]
- **Restore testing**: Includes restore tests to verify backups are recoverable [citation:14]
- **Deployment**: Requires a small Linux VM (2 vCPU, 2–4 GB RAM) as the console, plus an agent for data download [citation:14]

**Trade-off:** It is a self-hosted solution—you manage the infrastructure, storage, and scheduling. It is not a managed service like Druva or Veeam.
**Best for:** Organizations wanting a free, self-hosted M365 backup with read-only Graph permissions and full control over storage and data residency, accepting the operational responsibility of running the backup infrastructure.

### mailvault
**Stack:** Python / MS Graph / SQLite | **License:** Open Source (PyPI) [citation:15]
mailvault is a focused **email backup and archive tool** for IMAP and **Microsoft 365 mailboxes via MS Graph** [citation:15]. Key characteristics:
- **Incremental backups**: Skips already-archived messages, with per-folder resume points so repeated runs cost only new mail [citation:15]
- **Verify and repair**: Compares the mailbox against the archive and reports missing messages, with `--repair` to fetch them [citation:15]
- **Compression**: Optional zstd compression [citation:15]
- **SQLite query database**: Search archived mail by sender, recipient, subject, date, and folder, with CSV/JSON export and MCP server for AI client access [citation:5][citation:15]
- **Microsoft 365 configuration**: Uses an Azure app registration with tenant ID, client ID, and client secret [citation:15]

**Important limitation:** mailvault is **email-only**—it backs up Exchange Online mailboxes but not OneDrive, SharePoint, or Teams data. It is an archiving tool rather than a full M365 backup platform.
**Best for:** Organizations wanting a self-hosted, verifiable email archive for Microsoft 365 mailboxes, accepting that OneDrive and SharePoint are outside its scope.

---

## 📊 Comparison at a Glance

| Software | License | Stack | Exchange | OneDrive/SharePoint | Teams | Self-Hosted | Best For |
|----------|---------|-------|----------|---------------------|-------|-------------|----------|
| **Druva** | Proprietary | Cloud | ✅ | ✅ | ✅ | ❌ | Fully managed SaaS |
| **Veeam** | Proprietary | On-prem/Cloud | ✅ | ✅ | ✅ | ✅ | Free Community Edition (10 users) |
| **Keepit** | Proprietary | Cloud | ✅ | ✅ | ✅ | ❌ | Independent vendor-neutral |
| **Commvault** | Proprietary | Cloud/On-prem | ✅ | ✅ | ✅ | (On-prem) | Air-gap cyber recovery |
| **Rubrik (Sophos)** | Proprietary | Cloud | ✅ | ✅ | ✅ | ❌ | Sophos Central integration |
| **BackupZit** | AGPLv3 | Linux/Graph | ✅ | ✅ | (Check) | ✅ | Free self-hosted, no per-user fees |
| **mailvault** | Open Source | Python/Graph | ✅ (Email only) | ❌ | ❌ | ✅ | Verifiable email archiving |

---

## 🤝 Contributing

Contributions are welcome! If you know of an open-source Microsoft 365 Cloud-to-Cloud Backup tool that should be listed here, please open a pull request with:

- Project name and URL
- Brief description (1–2 sentences)
- Stack and license
- Why it stands out

Please ensure the project is actively maintained (releases within the last 12 months) and genuinely open-source.

**Note on the open-source ecosystem:** The open-source landscape for **Microsoft 365 backup** is **extremely sparse** compared to the commercial market. **BackupZit** is the most complete open-source option, providing self-hosted backup for Exchange, OneDrive, SharePoint, and calendars with read-only Graph permissions and no per-user fees [citation:14]. **mailvault** fills a narrower need for verifiable email archiving with a query database and MCP access, but does not cover OneDrive or SharePoint [citation:15]. On the commercial side, **Veeam's Community Edition** is notable for offering a genuinely free tier (10 users, 1 TB SharePoint) for small organizations [citation:3][citation:9]. For any production requirement at scale, commercial platforms like Druva, Keepit, or Commvault remain the practical choice, with the choice depending on whether you prioritize managed SaaS simplicity, independent vendor-neutral storage, or air-gap cyber recovery.

---

## 📄 License

This list is released under CC0 1.0 Universal (Public Domain). The software projects listed retain their respective licenses.

---

⭐ **If this list helped you discover a useful tool, please star the repo!** ⭐
