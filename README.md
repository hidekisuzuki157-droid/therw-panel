<div align="center">

<h1>THERW Panel</h1>

<p><strong>A self-hosted game server management panel built on Pterodactyl — with everything you actually need.</strong></p>

<p>
  <a href="https://therw.de"><img src="https://img.shields.io/badge/Website-therw.de-7c3aed?style=flat-square" alt="Website"></a>
  <a href="https://panel.therw.de"><img src="https://img.shields.io/badge/Live_Panel-panel.therw.de-2ea043?style=flat-square" alt="Panel"></a>
  <img src="https://img.shields.io/badge/PHP-8.2-777bb4?style=flat-square&logo=php" alt="PHP">
  <img src="https://img.shields.io/badge/MySQL-8.0-4479a1?style=flat-square&logo=mysql" alt="MySQL">
  <img src="https://img.shields.io/badge/nginx-1.x-009639?style=flat-square&logo=nginx" alt="nginx">
  <img src="https://img.shields.io/badge/Pterodactyl-1.13-5865f2?style=flat-square" alt="Pterodactyl">
</p>

<p>
  <a href="#-features">Features</a> ·
  <a href="#-tech-stack">Tech Stack</a> ·
  <a href="#-rest-api">API</a> ·
  <a href="#-supported-software">Software</a> ·
  <a href="CHANGELOG.md">Changelog</a> ·
  <a href="docs/API.md">API Docs</a>
</p>

</div>

---

## ✨ Features

THERW Panel extends Pterodactyl with a custom dashboard layer — keeping Wings as the backbone while adding features that Pterodactyl's default interface lacks.

| Feature | Description |
|---|---|
| 🖥️ **Self-Service Node Setup** | Connect your own root server via IP + SSH key. Wings installs automatically in the background. |
| 📥 **Import Existing Services** | Embed already-running systemd services (e.g. a Minecraft server) without Docker migration. |
| 📊 **Live Resource Monitoring** | Real-time CPU, RAM, disk and network sparklines for every server — Wings and imported alike. |
| 💾 **Backups & Schedules** | Create, download and restore backups. Automatic backup schedules (hourly / daily / weekly). |
| 🔁 **Task Scheduler** | Schedule restarts, commands or power actions — by interval, daily or weekly. No cron knowledge needed. |
| 🧩 **Plugin & Modpack Manager** | Install plugins directly from Modrinth, Hangar and SpigotMC. One-click modpack setup for Fabric & NeoForge. |
| 🚀 **Server Templates** | Quick-start templates for Vanilla, Paper, Fabric, NeoForge, Purpur and Velocity — pre-fills type, version and RAM. |
| 🤝 **Server Sharing** | Share servers with granular permissions: console only, files only, or full control. |
| 🌐 **Public REST API** | Full API with Bearer token auth — control servers, trigger power actions, manage backups and tasks. |
| 🗂️ **Sidebar Categories** | Organize servers into custom groups. Collapsible, drag-free, stored per user. |
| 📂 **File Manager** | Full browser-based file access for server files and root services — no FTP needed. |
| 🎫 **Ticket System** | Support tickets directly in the panel with live availability status. |
| ⚙️ **Account Center** | 2FA (TOTP), API keys, session management, recovery contacts and account linking. |
| 🔔 **Notifications** | In-panel notifications for important events. |

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| **Backend** | PHP 8.2, custom routing (no framework) |
| **Database** | MySQL 8.0 |
| **Web Server** | nginx + PHP-FPM |
| **Container Runtime** | Docker + Pterodactyl Wings 1.13 |
| **Node Agent** | Python 3.11 HTTP server (imported services) |
| **Frontend** | Vanilla JS, no bundler, no framework |
| **Auth** | Session-based, bcrypt, TOTP 2FA, AES-256-CBC token encryption |
| **OS** | Debian 12 |

---

## 🌐 REST API

THERW Panel exposes a public REST API at `https://panel.therw.de/api/v1/`.

Authentication via `Authorization: Bearer rwp_<token>` — tokens are managed in Account Settings.

```
GET    /api/v1/ping                          Health check + user info
GET    /api/v1/servers                       List all your servers
GET    /api/v1/servers/{id}                  Server details + live stats
POST   /api/v1/servers/{id}/power            Power action (start/stop/restart/kill)
POST   /api/v1/servers/{id}/command          Send console command
GET    /api/v1/servers/{id}/backups          List backups
POST   /api/v1/servers/{id}/backups          Create backup
DELETE /api/v1/servers/{id}/backups/{uuid}   Delete backup
GET    /api/v1/servers/{id}/tasks            List scheduled tasks
POST   /api/v1/servers/{id}/tasks            Create task
DELETE /api/v1/servers/{id}/tasks/{taskId}   Delete task
```

Server IDs: Wings servers use their 5-char `uuidShort`, imported servers use `ext-{id}`.

→ **[Full API Documentation](docs/API.md)**

---

## 📦 Supported Software

83 eggs across 11 categories — full Pterodactyl egg selection, not just Minecraft.

| Category | Count | Examples |
|---|---|---|
| ⛏️ Minecraft | 19 | Paper, Purpur, Fabric, NeoForge, Quilt, Folia, Velocity |
| 📱 Minecraft Bedrock | 2 | PocketMine-MP, Nukkit |
| 🏕️ Survival & Sandbox | 15 | Valheim, Rust, Palworld, V Rising, Terraria, Factorio, ARK |
| 🔫 Source Engine | 10 | CS2, CS:Source, Garry's Mod, TF2, Left 4 Dead 2 |
| 🗄️ Databases | 5 | MariaDB, Postgres, MongoDB, RethinkDB, Elasticsearch |
| 📊 Monitoring | 3 | Grafana, Uptime Kuma, Loki |
| 🎙️ Voice & Bots | 10 | TeamSpeak, Mumble, Lavalink, JMusicBot, PhantomBot |
| 🌐 Web Tools | 7 | Gitea, Code-Server, Reposilite, Minio S3, RabbitMQ |
| 💻 Runtimes | 11 | Python, Node.js, Go, .NET, Rust, Deno, Bun |

---

## 🗺️ Roadmap

Feature requests and bug reports are tracked via [GitHub Issues](https://github.com/hidekisuzuki157-droid/therw-panel/issues).

Have an idea? **[Open a feature request →](https://github.com/hidekisuzuki157-droid/therw-panel/issues/new?template=feature_request.md)**

---

## 📝 Changelog

See **[CHANGELOG.md](CHANGELOG.md)** for the full version history.

Latest additions include: Modpack Installer, Server Templates, Disk & Network Monitoring, Task Scheduler, Public REST API, Automatic Backup Schedules.

---

## 🔗 Links

| | |
|---|---|
| **Website** | https://therw.de |
| **Panel** | https://panel.therw.de |
| **Modrinth (Plugins)** | https://modrinth.com/user/Thurindir |

---

<div align="center">
  <sub>Built with ❤️ for the self-hosting community · <a href="https://therw.de">therw.de</a></sub>
</div>
