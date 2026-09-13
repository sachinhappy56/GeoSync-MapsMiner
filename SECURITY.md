# Security Policy — GeoSync MapsMiner™

Security, privacy, and data isolation are core architectural pillars of **GeoSync MapsMiner™**. This document outlines our security commitments, data isolation guarantees, and the procedure for responsibly reporting vulnerabilities.

---

## 1. Supported Releases

We actively maintain and provide security patches for the following versions:

| Version | Release Date | Security Support Status |
| :--- | :--- | :--- |
| **v3.3.x (Latest)** | September 2026 | :white_check_mark: Active Maintenance & Security Patches |
| **v3.2.x** | August 2026 | :warning: Critical Security Fixes Only |
| **< v3.2.0** | Earlier | :x: End of Life (Upgrade Recommended) |

---

## 2. Core Security & Privacy Commitments

### 100% Local Data Isolation (Zero Telemetry)
- **Zero Cloud Phone-Home**: GeoSync MapsMiner does not transmit your search queries, target postal codes, category choices, or harvested business data to any central server or third-party analytics collector.
- **Local Persistence Only**: All collected records, deduplication rings, and performance logs reside exclusively within your local SQLite database file (`collector_data.db`) on your physical hard drive.
- **Offline Simulation Capability**: The application features a 100% offline synthetic simulation engine that operates without any network connectivity whatsoever.

### Transport Security & Network Safety
- **Encrypted Outbound Connections**: All network communications with public map and spatial data providers are conducted strictly via encrypted Transport Layer Security (TLS 1.2 / TLS 1.3 over HTTPS).
- **No Inbound Attack Surface**: MapsMiner operates strictly as a client. It does not bind, listen, or open any inbound network ports, eliminating the risk of unauthorized remote exploitation over the local network.
- **Proxy Support**: Enterprise users can route all outbound HTTP/HTTPS traffic through inspected corporate proxy gateways.

### Binary Integrity Verification
Every official release binary is accompanied by an authoritative SHA-256 cryptographic checksum. Users can verify the integrity of their executable prior to launch using PowerShell:
```powershell
Get-FileHash -Algorithm SHA256 .\GeoSync_Prime.exe
```

---

## 3. Reporting a Security Vulnerability

We welcome responsible security research and take all vulnerability disclosures seriously. If you discover a security flaw or potential exploit in GeoSync MapsMiner, please follow these guidelines:

### How to Report
- **Email**: Send detailed disclosure information to: `security@geosync-prime.org` (or contact the repository maintainers directly).
- **Please DO NOT file public GitHub issues for security vulnerabilities.**

### What to Include in Your Report
To help us triage and resolve the issue quickly, please provide:
1. A descriptive title and type of vulnerability (e.g., memory corruption, injection, unhandled exception).
2. The specific version of GeoSync MapsMiner tested (e.g. v3.3.0).
3. The exact operating system and build number (e.g., Windows 11 Pro 64-bit).
4. Step-by-step reproduction instructions or a minimal Proof of Concept (PoC).
5. The potential impact if exploited by an attacker.

### Response Timelines
- **Initial Acknowledgment**: Within **48 hours** of receiving the report.
- **Triage & Assessment**: Within **5 business days**, detailing validity and severity rating.
- **Remediation & Patch**: Target release of a patched binary within **14 business days** for high-severity findings.
- **Public Disclosure**: Coordinated after the patch has been published and users have been given adequate time to upgrade.
