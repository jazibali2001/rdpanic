# RDPanic Server

[![Platform](https://img.shields.io/badge/Platform-Windows%20x64-0078D6?logo=windows&logoColor=white)](https://github.com/jazibali2001/rdpanic/releases)
[![Runtime](https://img.shields.io/badge/.NET-8.0%20LTS-512BD4?logo=dotnet&logoColor=white)](https://dotnet.microsoft.com/)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Release](https://img.shields.io/github/v/release/jazibali2001/rdpanic?color=blue&label=Latest%20Release)](https://github.com/jazibali2001/rdpanic/releases/latest)

RDPanic is a self-hosted Remote Desktop (RDP) gateway and centralized session broker for Windows environments. It gives IT administrators a single dashboard to manage, secure, and monitor remote desktop access across their server fleet without the complexity or licensing costs of Microsoft RDS and CALs.

Users can connect to remote machines in two ways:
1. **Native Windows RDP Client (`mstsc.exe`):** Direct launch using secure one-time launch tokens and protocol handling, giving users full native desktop performance, multi-monitor support, and peripherals.
2. **In-Browser Web RDP (HTML5):** Zero-install browser access rendered directly via an HTML5 canvas engine, perfect for quick access from laptops, Macs, Chromebooks, or locked-down machines.

---

## What RDPanic Does

Setting up Microsoft Remote Desktop Services usually means dealing with Active Directory domain controllers, dedicated gateway servers, network policy servers, and purchasing per-user or per-device CAL licenses. 

RDPanic eliminates that overhead:
- **No CAL Licenses Required:** Runs on standalone Windows Server (2016 through 2025) or standard 64-bit Windows 10/11.
- **Dual Session Launch Modes:** Launch full native Windows RDP sessions (`mstsc.exe`) or open sessions directly in any web browser without installing plugins.
- **Centralized Server & User Directory:** Group servers into pools (Production, Staging, DMZ, Databases), group users by department or role, and assign access in seconds.
- **Self-Service Access Requests:** Team members can request temporary or permanent access to specific servers directly from their user portal, with audio alerts and approval queues for admins.
- **Built-in System Updater:** Check for updates directly inside the web console, review release notes, automatically back up the database, and apply upgrades without manual file swapping.
- **Two Database Options:** Ships with a fast, zero-configuration JSON store (`store.json`) for smaller setups, or a high-concurrency SQLite storage engine (`store.db`) with Write-Ahead Logging (WAL) for 100+ active users.
- **Runs as a Managed Windows Service:** Operates in the background via `RDPBrokerService` with automatic crash recovery, or runs interactively for testing.

---

## Security Features

RDPanic is designed to keep backend RDP ports (3389) off the open internet:

- **Two-Factor Authentication (2FA / TOTP):** Native RFC 6238 TOTP support compatible with Google Authenticator, Microsoft Authenticator, and 1Password. Includes emergency backup reset pins.
- **Emergency Air-Gapped Recovery Key:** A dedicated cryptographic recovery key generated at setup allows administrators to regain access if locked out, without having to edit database files manually.
- **Windows DPAPI Credential Encryption:** Passwords and stored server credentials are encrypted on disk using machine-level Windows Data Protection API keys.
- **Role-Based Access Control (RBAC):** Five built-in role tiers (`SuperAdmin`, `ServerAdmin`, `UserAdmin`, `Auditor`, and standard `User`) with granular permission flags.
- **Full Audit Logging:** Detailed, searchable event logs capturing every login attempt, privilege change, server connection, and configuration update with source IP attribution.
- **Brute-Force & Session Protection:** Configurable grace periods, rate limiting, and sliding session timeouts.
- **Encrypted Automatic Backups:** Set up scheduled AES-256 database and certificate snapshots with automatic retention cleanup.
- **Alert Integrations:** Instant alerts via `ntfy` push notifications, authenticated SMTP email, and native Windows desktop notifications.

---

## Installation

### Option 1: Full Installer EXE (Recommended)
Download and run the installer on the machine that will act as your gateway:
```powershell
.\RDP-Installer.exe
```
The installer checks for the required Microsoft .NET 8 runtime, installs it automatically if missing, sets up firewall rules, and registers the background Windows service.

### Option 2: MSI Package (GPO / SCCM Silent Deployment)
For automated enterprise rollouts across multiple servers:
```powershell
msiexec.exe /i "RDP Installer.msi" /quiet /norestart
```

---

## System Requirements

- **Operating System:** Windows Server 2016, 2019, 2022, 2025 or Windows 10 / 11 (64-bit only).
- **Runtime:** Microsoft .NET 8.0 ASP.NET Core Runtime (checked and installed automatically by the setup wizard).
- **Network:** Default port `8080` (HTTPS, fully configurable to `443` or any custom port in the admin dashboard).

---

## Feedback, Bugs & Improvements

If you find a bug, run into an edge case on your Windows environment, or have suggestions to make RDPanic better align with enterprise best practices:

- **Email:** [jazibali1969@gmail.com](mailto:jazibali1969@gmail.com)
- **GitHub Issues:** Open an issue right here on the repository with steps to reproduce and your Windows version.

Pull requests and constructive feedback are always welcome.

---

## License

Distributed under the MIT License. See [LICENSE](LICENSE) for details.
