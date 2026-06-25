# Changelog

All notable changes to THERW Panel are documented here.

---

## [1.6.0] – 2026-06-25

### Added
- **Interactive Demo** — Fully navigable demo at `panel.therw.de/demo.php`. Includes a simulated server import flow (SSH key → connect → discover services → import) and a simulated game server creation flow (template picker → configure → Wings install steps). Fake console accepts real commands (`help`, `tps`, `gc`, `list`). Newly created/imported servers appear in the demo sidebar after completion.
- **SSH-Key Node Setup** — Root password is no longer required when connecting a new node. The panel generates a persistent ed25519 key pair; users add the public key to their server with a single copy-paste command. After setup, the key can be revoked at any time. No credentials are transmitted to or stored by the panel.
- **GitHub presence** — Public repository at `github.com/hidekisuzuki157-droid/therw-panel` with README, Changelog, API docs, issue templates and a roadmap issue.

### Changed
- Node setup page redesigned: replaced password field with SSH-key instructions, security explanation box and „Kein Passwort übertragen" badge.
- Landing page (therw.de): updated Import feature card, Setup step description, added Import FAQ entry, added „Warum ist therw.de kostenlos?" FAQ entry, added GitHub links (nav, contact section, footer), added Demo button in hero and CTA sections.

---

## [1.5.0] – 2026-06-25

### Added
- **Modpack Installer** — Search Modrinth directly from the new server dialog. Selecting a Fabric or NeoForge modpack automatically downloads and installs all server-side mods + config overrides after creation.
- **Server Templates** — Six one-click templates in the creation dialog (Vanilla, Paper, Fabric, NeoForge, Purpur, Velocity) that pre-fill egg, version and RAM.

---

## [1.4.0] – 2026-06-24

### Added
- **Task Scheduler** — Schedule recurring server actions (restart, start, stop, custom command) by interval (5–1440 min), daily at a set time, or weekly on selected days. Works for both Wings and imported servers.
- **Public REST API** — `https://panel.therw.de/api/v1/` with Bearer token auth. 11 endpoints covering server status, power actions, console commands, backup management and task management.
- **API Key Management** — Generate, reveal (password-protected) and revoke API tokens in Account Settings.

---

## [1.3.0] – 2026-06-23

### Added
- **Automatic Backup Schedules** — Set up scheduled backups (hourly / daily / weekly) with auto-rotation (delete oldest when limit is reached). Available for both Wings and imported servers.
- **Imported Server Backups** — Full backup support (create, list, download, delete, restore) for systemd-imported services via the node agent.

---

## [1.2.0] – 2026-06-22

### Added
- **Disk Monitoring** — Live disk usage with progress bar (color-coded: normal → orange at 70% → red at 90%) for all Wings servers.
- **Network Monitoring** — Live TX/RX rate display (bytes/sec) for Wings and imported servers.
- **Extended Node Agent** — `/service-metrics` now returns `disk_bytes`, `net_rx`, `net_tx` alongside CPU and RAM.

### Changed
- Resource cards now show a 2×2 grid: CPU, RAM, Disk, Network.

---

## [1.1.0] – 2026-06-20

### Added
- **Plugin & Mod Manager** — Search and install plugins from Modrinth, Hangar (Paper) and SpigotMC directly from the dashboard. No file upload needed.
- **Live Resource Monitoring** — CPU and RAM sparklines updating every 8s for Wings servers and every 10s for imported servers.

---

## [1.0.0] – Initial Release

### Features
- Pterodactyl Wings integration with custom dashboard
- Self-service node setup (SSH + auto Wings install)
- Systemd service import (no Docker required)
- Browser-based file manager
- Server sharing with granular permissions
- Sidebar categories (collapsible, per-user)
- Ticket system with support availability status
- Account center (2FA, sessions, recovery contacts)
- In-panel notifications
- 83 eggs across 11 game/tool categories
