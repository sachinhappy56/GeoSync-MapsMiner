# Support & Troubleshooting Portal — GeoSync MapsMiner™

Welcome to the **GeoSync MapsMiner™** technical support center. This guide helps you diagnose common runtime issues, review answers to frequently asked questions, and submit structured support tickets.

---

## 1. Support Channels & Service Levels

| Support Tier | Scope | Response SLA | Contact Channel |
| :--- | :--- | :--- | :--- |
| **Community Support** | Public GitHub Issues, documentation, community discussions | Best Effort (24–72 hours) | [GitHub Issues](https://github.com/your-org/GeoSync-MapsMiner/issues) |
| **Commercial / Enterprise** | Priority email support, private bug triage, architecture guidance | < 12 Hours (Business Days) | `support@geosync-prime.org` |

---

## 2. Pre-Flight Diagnostic Checklist

Before opening a support inquiry, perform these quick diagnostic checks to resolve 95% of common workstation issues:

- [ ] **Windows 64-bit Verification**: Confirm you are running on 64-bit Windows 10 (v1909+) or Windows 11. GeoSync MapsMiner does not support 32-bit (x86) environments.
- [ ] **Directory Write Permissions**: Ensure the application is located in a writable folder (e.g., `D:\GeoSync-MapsMiner\` or `C:\Users\<Name>\GeoSync\`). Running directly out of `C:\Program Files\` or read-only network shares will prevent database creation.
- [ ] **Antivirus / SmartScreen Exclusion**: Ensure Windows Defender or third-party endpoint security software is not locking `GeoSync_Prime.exe` or blocking local SQLite disk writes.
- [ ] **Microsoft Visual C++ Runtime**: Confirm the [Microsoft Visual C++ 2015–2022 Redistributable (x64)](https://aka.ms/vs/17/release/vc_redist.x64.exe) is installed.
- [ ] **Check the Log File**: Examine `geosync.log` in your application folder for detailed error stack traces and network timeout reports.

---

## 3. Frequently Asked Questions (FAQ)

### Q1: Why are my CSV exports split into multiple files (e.g. `export_part1.csv`, `export_part2.csv`)?
**Answer**: On the **Completed Pincodes & Downloads** tab, the **Max Rows per File** setting is designed to safeguard your workflow. Traditional spreadsheet applications (such as Microsoft Excel) enforce a strict limit of 1,048,576 rows per sheet. MapsMiner automatically chunks large multi-million record exports into sequential parts so that every file can be opened directly without truncating data.

### Q2: How do I resume an interrupted job after a system crash or power outage?
**Answer**: GeoSync MapsMiner features transactional atomic checkpointing. Every unique record is committed to `collector_data.db` upon receipt, and processed postal codes are marked complete in the ledger. Simply re-launch `GeoSync_Prime.exe`, re-enter your target postal codes, and click **▶ Start Mining Job**. The engine will automatically detect and skip already completed sectors.

### Q3: Why does Windows Defender flag `GeoSync_Prime.exe` on first launch?
**Answer**: As a high-performance compiled standalone executable packed with PyInstaller and UPX, Windows SmartScreen treats newly released binaries with caution until they establish a reputation. This is a well-known false positive. Simply click **More info** → **Run anyway**. You can verify the official SHA-256 hash using `Get-FileHash -Algorithm SHA256 .\GeoSync_Prime.exe`.

### Q4: Can I run multiple instances of MapsMiner simultaneously?
**Answer**: Yes, provided each instance runs out of its own dedicated directory with its own distinct `collector_data.db` database file to prevent SQLite file locking conflicts.

### Q5: How do I harvest only specific niche businesses (e.g. only Italian Restaurants)?
**Answer**: Navigate to the **Category & Discovery** tab:
1. In the **Search Keyword / Business Query** field, type `Italian Restaurant`.
2. Leave the category presets as default, or select the *Food, Dining & Nightlife* pack.
3. Start the job. MapsMiner will now filter its spatial exploration to target only Italian dining establishments.

---

## 4. Submitting a Support Ticket

If your issue persists after completing the pre-flight checklist, submit an issue report with the following template:

```markdown
### Environment
- **GeoSync MapsMiner Version**: [e.g. v3.3.0]
- **Operating System**: [e.g. Windows 11 Pro 64-bit, Build 22631]
- **CPU & RAM**: [e.g. AMD Ryzen 7 5800X, 32 GB RAM]
- **Target Country & Postal Code**: [e.g. India / 110001 or US / 90210]

### Problem Description
A clear and concise description of the error encountered.

### Steps to Reproduce
1. Launch `GeoSync_Prime.exe`.
2. Configure provider to `Hybrid`, workers to `250`, radius to `6.0 km`.
3. Click 'Start Mining Job'.
4. Observe error state.

### Expected Behavior
What you expected to happen.

### Relevant Log Snippet (from geosync.log)
```text
[Paste error lines from geosync.log here - do NOT include confidential credentials]
```
```

---

## 5. Enterprise Inquiries & Custom Deployments

For inquiries regarding custom geographic boundary integration, dedicated high-volume enterprise licenses, or private cloud worker clusters, contact our solutions engineering group at:
- **Email**: `enterprise@geosync-prime.org`
- **Hours of Operation**: Monday – Friday, 09:00 – 18:00 UTC.
