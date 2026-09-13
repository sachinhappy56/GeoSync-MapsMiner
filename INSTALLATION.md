# GeoSync MapsMiner™ — Installation & Deployment Guide

This guide provides comprehensive instructions for deploying and running **GeoSync MapsMiner™** on Windows environments.

---

## 1. System Requirements

GeoSync MapsMiner is engineered for high-concurrency spatial processing and asynchronous disk persistence. Ensure your host system meets the following specifications:

| Component | Minimum Specification | Recommended (Enterprise Production) |
| :--- | :--- | :--- |
| **Operating System** | Windows 10 (64-bit, version 1909+) | Windows 11 (64-bit) or Windows Server 2022 |
| **CPU Architecture** | 4-Core x86_64 Processor | 8-Core to 16-Core Processor (Intel Core / AMD Ryzen) |
| **System Memory (RAM)**| 4 GB Available Physical RAM | 16 GB+ High-Speed RAM |
| **Storage Medium** | Standard HDD / SSD (2 GB Free Space) | High-Speed NVMe PCIe SSD (for sustained SQLite WAL writes) |
| **Network Interface** | 10 Mbps Broadband Internet | 50+ Mbps Low-Latency Fiber Connection |
| **Display Resolution** | 1280 x 720 (HD) | 1920 x 1080 (Full HD) or higher |
| **External Runtimes** | **None** (Self-Contained Executable) | **None** (Zero External Dependencies) |

---

## 2. Portable Standalone Deployment

GeoSync MapsMiner is distributed as a single, fully compiled, self-contained Windows executable: `GeoSync_Prime.exe`.

> [!TIP]
> **Zero Runtime Dependencies**:
> You do **not** need Python, Node.js, Git, or browser automation engines (Chromium, Selenium, Puppeteer) installed. The binary embeds its own optimized CPython runtime, Tk graphic engine, SQLite database driver, and spatial math libraries.

### Step-by-Step Setup

1. **Download Release**:
   Obtain the official `GeoSync-MapsMiner-v3.3.0-win64.zip` from your authorized distribution channel or GitHub Releases.

2. **Extract to a Dedicated Working Directory**:
   Extract the contents into a dedicated folder where the application has full read/write privileges.
   * **Recommended Path**: `D:\GeoSync-MapsMiner\` or `C:\Users\<YourUsername>\GeoSync-MapsMiner\`
   * *Avoid* running directly out of `C:\Program Files\` or `C:\Windows\System32\` unless executing with elevated administrator permissions, as Windows restricts automated SQLite database creation in system roots.

3. **Verify Folder Contents**:
   A standard deployment contains:
   ```text
   GeoSync-MapsMiner/
   ├── GeoSync_Prime.exe          # Main application executable (~10.5 MB)
   ├── exports/                   # Directory where CSV/JSONL files are saved (auto-created)
   └── collector_data.db          # Embedded ACID database file (auto-created on first run)
   ```

4. **Launch**:
   Double-click `GeoSync_Prime.exe`. The application HUD will initialize and display the **Cards Dashboard** in under two seconds.

---

## 3. Windows SmartScreen & Antivirus Transparency

When launching a freshly downloaded standalone executable on Windows, you may encounter a standard Windows Defender SmartScreen prompt stating:
> *"Windows protected your PC — Microsoft Defender SmartScreen prevented an unrecognized app from starting."*

### Why Does This Occur?
1. **Packaging Heuristics**: GeoSync MapsMiner is packaged into a compact standalone binary using PyInstaller and compressed with UPX (Ultimate Packer for eXecutables) to keep the file size under 11 MB.
2. **Reputation-Based Trust**: Microsoft SmartScreen flags any newly compiled executable that has not yet accumulated thousands of downloads through the Microsoft Store or been signed with an expensive Enterprise Extended Validation (EV) certificate.
3. **No Malicious Code**: The binary contains strictly legitimate spatial exploration, HTTP networking, and SQLite storage routines.

### How to Proceed:
1. Click **More info** on the SmartScreen dialog.
2. Click **Run anyway**.
3. To whitelist the folder permanently in Windows Defender:
   - Open **Windows Security** → **Virus & threat protection**.
   - Select **Manage settings** under *Virus & threat protection settings*.
   - Scroll to **Exclusions** → **Add or remove exclusions**.
   - Add your extracted `GeoSync-MapsMiner` folder.

---

## 4. Integrity & Checksum Verification

To ensure that your downloaded executable is authentic and has not been altered or corrupted in transit, verify its SHA-256 checksum using Windows PowerShell.

Open PowerShell in the folder containing `GeoSync_Prime.exe` and execute:

```powershell
Get-FileHash -Algorithm SHA256 .\GeoSync_Prime.exe
```

Compare the resulting 64-character hash with the official release checksum published on the release page:

```text
Algorithm : SHA256
Hash      : [Check release notes for official SHA-256 string]
Path      : D:\GeoSync-MapsMiner\GeoSync_Prime.exe
```

---

## 5. Network & Firewall Configuration

GeoSync MapsMiner operates as a client that establishes outbound HTTPS/TLS connections to mapping providers and spatial endpoints.

- **Outbound Ports**: Port `80` (HTTP) and Port `443` (HTTPS).
- **Inbound Ports**: None required. MapsMiner does not listen on any incoming server ports.
- **Proxy Configuration**:
  If your enterprise network routes traffic through an upstream proxy, set standard Windows environment variables before launching:
  ```powershell
  $env:HTTP_PROXY = "http://proxy.yourdomain.com:8080"
  $env:HTTPS_PROXY = "http://proxy.yourdomain.com:8080"
  .\GeoSync_Prime.exe
  ```

---

## 6. Upgrading to Newer Releases

To update GeoSync MapsMiner to a newer version without losing previously mined data or active jobs:

1. Close the running instance of `GeoSync_Prime.exe`.
2. Replace `GeoSync_Prime.exe` with the new version binary.
3. **Preserve** the following files and folders:
   - `collector_data.db` (and any `.db-wal` / `.db-shm` files) — contains all your mined records and deduplication indexes.
   - `exports/` — contains your generated CSV and JSONL datasets.
   - `checkpoints/` — contains resumable job state manifests.
4. Launch the updated `GeoSync_Prime.exe`. Database schemas migrate automatically if required.

---

## 7. Troubleshooting Launch Issues

### Issue: Application closes immediately or fails to open
- **Cause**: Missing Visual C++ Runtime on older, un-updated Windows 10 installations.
- **Remedy**: Install the official [Microsoft Visual C++ 2015–2022 Redistributable (x64)](https://aka.ms/vs/17/release/vc_redist.x64.exe).

### Issue: "Permission Denied" or SQLite Lock Error on Startup
- **Cause**: The application is placed in a read-only folder or on a network drive without write permissions.
- **Remedy**: Move the folder to your local user directory (e.g. `C:\Users\<Name>\Documents\GeoSync\`).

### Issue: High CPU usage during massive jobs
- **Cause**: Running 250 Turbo Workers on an older dual-core or quad-core processor.
- **Remedy**: On the Cards Dashboard, adjust the Worker selector from `250 Workers (Max Dedicated Turbo)` to `50 Workers` or `100 Workers` to match your CPU thread count.
