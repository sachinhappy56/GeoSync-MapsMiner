# Changelog

All notable changes to **GeoSync MapsMiner™** are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [3.3.0] - 2026-09-13 — *Universal Golden Sweet Spot Release*

### Added
- **Curated Golden 1,250 Master Commercial Categories**:
  - Pre-indexed, empirically calibrated taxonomy covering ~98.5% of all active commercial entities across Healthcare, Legal, Finance, Hospitality, Automotive, Retail, Home Trades, and Professional Services.
  - Bypasses low-density long-tail categories to triple collection speed without sacrificing lead completeness.
- **Dynamic Search Radius Selector**:
  - Added interactive radius configuration on the Cards Dashboard:
    - `6.0 km (Sweet Spot - Default)` — Empirically proven optimal balance of area coverage and point density.
    - `1.0 km (Dense Metro Core)` — Micro-radius exploration for ultra-dense downtown high-rises.
    - `3.0 km (Urban Core)` — Standard metropolitan sector coverage.
    - `10.0 km (Rural County / Highway)` — Macro-radius exploration for sparse regional corridors.
  - Dynamically updates spatial grid generator and request viewports in real time.
- **250 Turbo Worker Thread Concurrency**:
  - Introduced `250 Workers (Max Dedicated Turbo)` option in the concurrency dropdown for high-bandwidth fiber connections.
- **Unified Category & Discovery Controls**:
  - Unified left-hand and right-hand action buttons to `🌟 Load Golden 1,250` for seamless, one-click catalog activation.

### Optimized
- **Compact Standalone Binary Distribution**:
  - Maintained executable footprint at **10.58 MB** using UPX compression and dependency pruning, with zero external runtime requirements.
- **Database Write Barriers**:
  - Enhanced asynchronous WAL flush routines, reducing SQLite lock contention during peak 250-worker thread bursts.

---

## [3.2.0] - 2026-08-28

### Added
- **Concentric Multi-Ring Radial Tessellation**:
  - Upgraded spatial exploration algorithm to compute concentric, equidistant radial rings around postal code centroids, guaranteeing zero blind spots.
- **Real-Time Hardware HUD Meters**:
  - Added live CPU% utilization and RAM consumption telemetry cards to the top HUD header.
- **Batch Pincode Parser**:
  - Added support for comma, space, and newline-separated postal code batch inputs directly on the dashboard.
- **Hybrid Provider Mode**:
  - Integrated OpenStreetMap (OSM) Overpass geometric nodes with Google Maps spatial streams for deeper POI discovery.

### Improved
- **UI Responsiveness**:
  - Decoupled GUI event loop completely from network I/O and disk flushing to prevent Windows "Not Responding" titlebar states during heavy workloads.

---

## [3.1.0] - 2026-07-15

### Added
- **Two-Stage FastDedupRing™**:
  - Stage 1: Cryptographic 64-character SHA-256 property fingerprinting for microsecond exact matches.
  - Stage 2: Multi-factor entity resolution evaluating Place ID, standardized E.164 phone numbers, and root domain URLs.
- **Streaming Multi-Chunk CSV Exporter**:
  - Configurable row-split thresholds (`50,000`, `100,000`, `250,000`, `500,000`, `1,000,000` rows per file) to prevent spreadsheet application crashes.
- **JSONL Streaming Exporter**:
  - High-speed newline-delimited JSON exporter for direct ingestion into cloud data warehouses (Snowflake, BigQuery).

### Fixed
- Fixed memory leakage during continuous multi-hour jobs by implementing bounded deduplication sliding windows.

---

## [3.0.0] - 2026-05-10 — *Architectural Redesign*

### Added
- **Decoupled Architecture**:
  - Complete architectural rewrite separating Presentation (HUD), Service Coordination, Worker Thread Pools, Spatial Generators, Deduplication, and Database Storage.
- **Dual-Engine Architecture (Live vs. Simulation)**:
  - Added 100% offline synthetic simulation engine for risk-free UI demos, sandboxing, and training.
  - Added live collection engine with jitter, exponential backoff, and localized request headers.
- **ACID Transactional SQLite Storage**:
  - Integrated SQLite with Write-Ahead Logging (`PRAGMA journal_mode=WAL`) and atomic OS-level schema checkpointing.
- **Worldwide Territorial Index**:
  - Built-in administrative hierarchy for 120+ countries with country-level postal code models.
