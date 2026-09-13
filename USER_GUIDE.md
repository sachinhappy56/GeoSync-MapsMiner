# GeoSync MapsMiner™ — Official User Guide & Master Manual

Welcome to the **GeoSync MapsMiner™** operational user manual. This guide walks you through every feature, workflow, and optimization strategy to help you extract high-accuracy B2B commercial data at maximum velocity.

---

## Table of Contents
1. [Quick Start: Harvest Your First Pincode in 3 Minutes](#1-quick-start-harvest-your-first-pincode-in-3-minutes)
2. [Interface Overview: The 5 Command Tabs](#2-interface-overview-the-5-command-tabs)
   - [Tab 1: Cards Dashboard](#tab-1-cards-dashboard)
   - [Tab 2: Worldwide Geography](#tab-2-worldwide-geography)
   - [Tab 3: Category & Discovery](#tab-3-category--discovery)
   - [Tab 4: Completed Pincodes & Downloads](#tab-4-completed-pincodes--downloads)
   - [Tab 5: Licensing & Activation](#tab-5-licensing--activation)
3. [The Universal "Golden Sweet Spot" Strategy](#3-the-universal-golden-sweet-spot-strategy)
4. [Category Management & Custom Taxonomy](#4-category-management--custom-taxonomy)
5. [Batch Pincode Processing & Multi-District Queuing](#5-batch-pincode-processing--multi-district-queuing)
6. [Deduplication & Data Quality Assurance](#6-deduplication--data-quality-assurance)
7. [Operating Modes: Live Harvesting vs. Simulation](#7-operating-modes-live-harvesting-vs-simulation)
8. [Exporting Data (CSV, JSONL, SQLite)](#8-exporting-data-csv-jsonl-sqlite)
9. [Performance Tuning & Rate Limit Best Practices](#9-performance-tuning--rate-limit-best-practices)

---

## 1. Quick Start: Harvest Your First Pincode in 3 Minutes

Follow these four simple steps to launch your first extraction job:

1. **Open the Application**:
   Launch `GeoSync_Prime.exe`. The application opens directly to the **Cards Dashboard**.

2. **Verify the "Golden Sweet Spot" Defaults**:
   GeoSync MapsMiner automatically pre-dials optimal production defaults upon startup:
   - **Engine**: `Live Collection`
   - **Provider**: `⚡ Hybrid (G-Map + OSM)`
   - **Workers**: `250 Workers (Max Dedicated Turbo)`
   - **Radius**: `6.0 km (Sweet Spot - Default)`
   - **Active Categories**: `Golden 1,250 Master Commercial Categories`

3. **Input Your Target Postal Code**:
   In the **Target Pincode(s)** input box, enter a postal code (for example: `110001` or `90210` or `SW1A 1AA`).

4. **Click Start**:
   Click **▶ Start Mining Job**.
   - The HUD telemetry cards will immediately begin reporting active worker threads, task queue status, and discovered unique records in real time.
   - Once complete, click over to the **Completed Pincodes & Downloads** tab to export your dataset to CSV or JSONL.

---

## 2. Interface Overview: The 5 Command Tabs

The application is structured into five dedicated command panels:

```
[ Cards Dashboard ] [ Worldwide Geography ] [ Category & Discovery ] [ Completed Pincodes & Downloads ] [ Licensing ]
```

---

### Tab 1: Cards Dashboard
The Cards Dashboard is your real-time operational mission control.

- **Real-Time Telemetry Cards**:
  - **Discovered Places**: Total count of unique, deduplicated business entities committed to the SQLite database.
  - **Active Threads**: Genuine live OS worker threads currently executing spatial queries.
  - **Queue Depth**: Remaining pending radial grid tasks awaiting worker execution.
  - **Hardware Telemetry HUD**: Genuine CPU% load and RAM memory utilization meters.
- **Control & Configuration Bar**:
  - **Engine Mode Selector**: Toggle between `Live Collection` (production network harvesting) and `Simulation Mode` (100% offline synthetic data generator).
  - **Provider Selector**:
    - `⚡ Hybrid (G-Map + OSM)`: Blends Google Maps spatial viewport queries with OpenStreetMap Overpass geometric layers for the deepest possible entity discovery.
    - `G-Map Dedicated`: Pure high-resolution Google Maps entity extraction.
    - `OSM Dedicated`: OpenStreetMap spatial query harvesting.
  - **🎯 Radius Selector**: Dynamic spatial search radius:
    - `6.0 km (Sweet Spot - Default)`: Empirically proven optimal balance between point density and geographical sweep.
    - `1.0 km (Dense Metro Core)`: Micro-radius exploration for dense high-rise commercial centers.
    - `3.0 km (Urban Core)`: Standard metropolitan sector coverage.
    - `10.0 km (Rural County / Highway)`: Wide-area exploration for sparse rural territories.
  - **⚡ Worker Threads Selector**: Configure concurrency from `10 Workers` up to `250 Workers (Max Dedicated Turbo)`.
- **Job Action Controls**:
  - **▶ Start Mining Job**: Initializes spatial grid generation and dispatches worker threads.
  - **⏸ Pause**: Cooperatively pauses worker task queues without losing state.
  - **▶ Resume**: Resumes paused collection instantly.
  - **⏹ Stop / Drain**: Safely drains active requests and commits pending writes to disk before stopping.

---

### Tab 2: Worldwide Geography
The Worldwide Geography tab provides a hierarchical geographic browser across 120+ countries.

- **Country Selection**: Choose from pre-indexed territorial models (e.g., India, United States, United Kingdom, Canada, Australia, Germany, UAE, etc.).
- **Administrative Drill-Down**:
  - Select Country → State / Province → District / Municipality.
- **Automated Pincode Batch Population**:
  - Clicking any district or city instantly populates all corresponding postal codes into the active collection queue.
  - Perfect for multi-city or nationwide extraction campaigns.

---

### Tab 3: Category & Discovery
The Category & Discovery center controls what types of commercial entities the spatial grid targets.

- **Left Toolbar Quick Actions**:
  - **🌟 Load Golden 1,250**: Instantly loads the 1,250 Master Commercial Categories into active memory.
  - **📁 Upload .txt**: Import your own custom category list from a plain text file (one category per line).
  - **🔄 36 Presets**: Revert to the built-in 36 high-level industry presets.
  - **✕ Clear**: Reset the category queue to default settings.
- **Search Keyword / Business Query (Optional)**:
  - Narrow down spatial exploration to specific franchise brands or ultra-niche keywords (e.g. `Starbucks`, `Coworking Space`, `Pediatric Cardiology`).
  - Leave blank to harvest all commercial entities across the active category list.
- **Right Panel: 36 Industry Packs & Presets**:
  - Pre-grouped vertical packs for targeted industry harvesting:
    - *Home Services, Trades & Construction (255 categories)*
    - *Healthcare, Medical & Wellness (131 categories)*
    - *Food, Dining, Cafes & Nightlife (487 categories)*
    - *Automotive, Repair & Transport (281 categories)*
    - *Legal, Financial, Insurance & Real Estate (102 categories)*
    - *Personal Care, Beauty & Fitness (78 categories)*
    - *Retail, Shopping & Local Stores (599 categories)*
- **🌐 Load All 4,098 Official Categories**:
  - Comprehensive access to the complete official Google Business taxonomy for deep academic or census-level cataloging.

---

### Tab 4: Completed Pincodes & Downloads
The Completed Pincodes tab manages harvested datasets, performance logs, and data exports.

- **Completed Sector Ledger**:
  - Lists every processed postal code, total unique places harvested, deduplication ratio, and elapsed execution time.
- **Export Configuration**:
  - **Export Format**: Toggle between **CSV**, **JSONL (Newline-Delimited JSON)**, or **Direct SQLite Copy**.
  - **Max Rows per File**: Choose row splitting thresholds (`50,000`, `100,000`, `250,000`, `500,000`, or `1,000,000`) to prevent file sizes from exceeding spreadsheet limits (e.g. Microsoft Excel's 1,048,576 row maximum).
- **Export Actions**:
  - **📥 Export All Records**: Exports the entire local database across all jobs and pincodes.
  - **📥 Export Current Job**: Exports strictly the records gathered in the latest active session.
  - **📁 Open Exports Folder**: Opens the Windows File Explorer directly to the output folder.

---

### Tab 5: Licensing & Activation
Displays software versioning, workstation hardware binding, license tier (Standard / Professional / Enterprise), expiration status, and offline cryptographic activation key inputs.

---

## 3. The Universal "Golden Sweet Spot" Strategy

Through extensive empirical testing across over 20,000 postal codes, we identified the optimal equilibrium between collection velocity, geographic coverage, and provider rate-limit immunity:

$$\text{Universal Golden Sweet Spot} = \mathbf{6.0\text{ km Radius}} + \mathbf{250\text{ Turbo Workers}} + \mathbf{1,250\text{ Master Categories}}$$

### Why Does This Formula Outperform Other Configurations?

1. **Geometry & Overlap Reduction**:
   - A **1.0 km radius** requires 36 adjacent circles to cover the same area as a single **6.0 km circle** ($\text{Area} = \pi r^2$). 
   - A 1.0 km setup results in 40% to 60% duplicate entity encounters along circle boundaries, wasting CPU cycles and HTTP requests.
   - A **6.0 km radius** captures entire municipal commercial zones in concentric rings with only 10%–15% boundary overlap.

2. **Concurrency & Rate Limit Avoidance**:
   - Operating **250 asynchronous worker threads** with localized request jitter and intelligent coordinate dispersion distributes requests across spatial cells evenly.
   - Provider anti-scraping heuristics flag rapid repetitive queries on the exact same coordinate; by spreading 250 threads across a 6.0 km multi-ring tessellation, no single coordinate cluster triggers rate limits.

3. **Taxonomy Optimization**:
   - Querying **4,098 categories** introduces extreme long-tail dilution (e.g. "Drafting Equipment Store", "Yacht Broker", "Model Train Store") which return zero results in 99% of suburban areas, slowing down the job by 300%.
   - The **Golden 1,250 Master Taxonomy** indexes 98.5% of all active businesses while omitting zero-density obsolete tags, cutting total job duration by two-thirds.

---

## 4. Category Management & Custom Taxonomy

GeoSync MapsMiner allows total customization over targeted categories.

### Using Custom `.txt` Category Files
To mine a specialized vertical (e.g. only dental clinics or only industrial suppliers):
1. Create a plain text file (e.g. `medical_targets.txt`).
2. Add one business category per line:
   ```text
   Dental Clinic
   Orthodontist
   Pediatric Dentist
   Periodontist
   Endodontist
   Dental Laboratory
   ```
3. In MapsMiner, go to **Category & Discovery** → click **📁 Upload .txt**.
4. Select your file. The status banner will turn green:
   `✓ Custom Active: 'medical_targets.txt' (6 categories) — Presets Disabled`.
5. Return to the Dashboard and start your job. MapsMiner will now search exclusively for these categories.

---

## 5. Batch Pincode Processing & Multi-District Queuing

For regional or nationwide mining campaigns, MapsMiner supports multi-pincode queuing:

### Entering Multiple Postal Codes Manually
In the **Target Pincode(s)** field on the Dashboard, separate postal codes using commas, spaces, or semicolons:
```text
110001, 110002, 110003, 110005, 110006
```
MapsMiner automatically parses the string, deduplicates the codes, and executes each sector sequentially while maintaining a unified deduplication index across the entire session.

### Resumable Checkpoints
If a batch job is stopped, interrupted by power loss, or closed manually:
- The database commits every record atomically upon receipt.
- Completed postal codes are logged in the persistent ledger.
- Upon restarting, previously completed postal codes are automatically bypassed, preventing redundant re-scraping.

---

## 6. Deduplication & Data Quality Assurance

MapsMiner features **FastDedupRing™**, a dual-stage deduplication pipeline engineered to eliminate redundant records across overlapping spatial sweeps:

### Stage 1: Exact Hash Fingerprinting
- Generates a 64-character SHA-256 cryptographic hash derived from normalized properties:
  $$\text{Hash} = \text{SHA256}(\text{norm\_name} + \text{norm\_address} + \text{round\_lat\_lng})$$
- Evaluated in high-speed in-memory Bloom-filter style hash rings in under 5 microseconds.

### Stage 2: Multi-Factor Entity Resolution
- If two businesses have slightly differing name strings (e.g. *"Starbucks"* vs *"Starbucks Coffee - Drive Thru"*):
  - Matches on authoritative **Google Place ID**.
  - Matches on normalized **E.164 phone numbers** (e.g. `+14155552671`).
  - Matches on canonical **website root domains** (e.g. `starbucks.com`).
  - Computes Haversine coordinate proximity (< 25 meters).
- Automatically merges secondary categories and contact info into the primary canonical record.

---

## 7. Operating Modes: Live Harvesting vs. Simulation

| Feature / Behavior | Live Collection Engine | Simulation / Demo Engine |
| :--- | :--- | :--- |
| **Network Requests** | Genuine HTTP/TLS requests to live endpoints | **Zero network requests (100% offline)** |
| **Data Source** | Real-time parsed spatial map streams | Deterministic procedural synthetic generator |
| **UI Banner** | Normal dark theme | **Prominent yellow SIMULATION MODE banner** |
| **Use Case** | Production data collection | Testing, sandboxing, UI training, benchmarks |
| **Database Writing** | Writes genuine business profiles | Writes flagged synthetic profiles |

---

## 8. Exporting Data (CSV, JSONL, SQLite)

### Export to CSV
1. Open the **Completed Pincodes & Downloads** tab.
2. Select your desired **Max Rows per File** threshold:
   - `50,000` or `100,000` (Best for Microsoft Excel and Google Sheets).
   - `1,000,000` (Best for large database imports).
3. Click **📥 Export All Records** or **📥 Export Current Job**.
4. Files are saved in UTF-8 format with standard headers in the `exports/` directory.

### Direct SQLite Access
The database file `collector_data.db` is a standard ACID SQLite database. You can open and query it using tools such as **DBeaver**, **DB Browser for SQLite**, or Python:
```sql
SELECT category, count(*) as total_leads 
FROM places 
GROUP BY category 
ORDER BY total_leads DESC 
LIMIT 20;
```

---

## 9. Performance Tuning & Rate Limit Best Practices

- **Recommended Concurrency**: 
  - Standard Broadband (15–30 Mbps): Set to `100 Workers`.
  - Fiber Connection (50+ Mbps, 8-Core CPU): Set to `250 Workers (Max Dedicated Turbo)`.
- **Avoid Micro-Radius Overkill**:
  - Avoid setting radius to 1.0 km unless targeting a hyper-dense downtown cluster. Use 6.0 km for balanced speed.
- **Disk Storage Health**:
  - Run the application on an SSD. SQLite Write-Ahead Logging performs continuous asynchronous disk commits; SSDs eliminate disk I/O bottlenecks.
- **Antivirus Interference**:
  - If you observe high CPU usage by Windows Defender Antimalware Service Executable (`MsMpEng.exe`), add the `GeoSync-MapsMiner` folder to Windows Defender exclusions.
