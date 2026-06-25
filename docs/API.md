# THERW Panel – Public REST API

Base URL: `https://panel.therw.de/api/v1`

## Authentication

All requests require a Bearer token in the `Authorization` header:

```
Authorization: Bearer rwp_<your_token>
```

Generate tokens in **Account Settings → API-Schlüssel**.

---

## Server IDs

| Server Type | ID Format | Example |
|---|---|---|
| Wings (Pterodactyl) | 5-char UUID short | `a1b2c` |
| Imported (systemd) | `ext-{number}` | `ext-5` |

---

## Endpoints

### `GET /ping`

Health check and current user info.

```json
{
  "ok": true,
  "user": "Thurindir",
  "username": "thurindir",
  "email": "..."
}
```

---

### `GET /servers`

List all servers belonging to the authenticated user.

```json
{
  "count": 12,
  "servers": [
    {
      "id": "a1b2c",
      "type": "wings",
      "name": "Rosewood Main",
      "status": "running",
      "node": "node1.therw.de"
    },
    {
      "id": "ext-5",
      "type": "external",
      "name": "WaveArena",
      "status": "running",
      "node": "node1.therw.de"
    }
  ]
}
```

---

### `GET /servers/{id}`

Get details and live stats for a single server.

```json
{
  "id": "ext-5",
  "type": "external",
  "name": "WaveArena",
  "status": "running",
  "cpu": 2.4,
  "ram_bytes": 1811939328,
  "disk_bytes": 459535039,
  "node": "node1.therw.de"
}
```

---

### `POST /servers/{id}/power`

Trigger a power action.

**Body:**
```json
{ "action": "restart" }
```

Actions: `start` · `stop` · `restart` · `kill`

**Response:**
```json
{ "ok": true }
```

---

### `POST /servers/{id}/command`

Send a console command to the server.

**Body:**
```json
{ "command": "say Hello World" }
```

---

### `GET /servers/{id}/backups`

List all backups for a server.

```json
{
  "backups": [
    {
      "uuid": "abc123",
      "name": "Backup #1",
      "bytes": 356000000,
      "created_at": "2026-06-25T12:00:00Z",
      "completed_at": "2026-06-25T12:01:30Z"
    }
  ]
}
```

---

### `POST /servers/{id}/backups`

Create a new backup.

```json
{ "ok": true, "uuid": "abc123" }
```

---

### `DELETE /servers/{id}/backups/{uuid}`

Delete a specific backup.

```json
{ "ok": true }
```

---

### `GET /servers/{id}/tasks`

List all scheduled tasks for a server.

```json
{
  "tasks": [
    {
      "id": 1,
      "name": "Nightly Restart",
      "type": "restart",
      "schedule_type": "daily",
      "time_of_day": "04:00",
      "enabled": true,
      "next_run_at": "2026-06-26T04:00:00"
    }
  ]
}
```

---

### `POST /servers/{id}/tasks`

Create a scheduled task.

**Body (interval example):**
```json
{
  "name": "Hourly Restart",
  "type": "restart",
  "schedule_type": "interval",
  "interval_minutes": 60
}
```

**Body (daily example):**
```json
{
  "name": "Nightly Restart",
  "type": "restart",
  "schedule_type": "daily",
  "time_of_day": "04:00"
}
```

**Body (command example):**
```json
{
  "name": "Morning Broadcast",
  "type": "command",
  "command_text": "say Good morning!",
  "schedule_type": "daily",
  "time_of_day": "08:00"
}
```

Task types: `restart` · `start` · `stop` · `command`
Schedule types: `interval` · `daily` · `weekly`

---

### `DELETE /servers/{id}/tasks/{taskId}`

Delete a scheduled task.

```json
{ "ok": true }
```

---

## Rate Limits

The API applies a shared rate limit of 30 requests/burst per IP via nginx.

---

## Use Cases

- **Discord Bots** — Query server status and trigger restarts from Discord commands
- **Custom Dashboards** — Embed live server stats in your own frontend
- **Automation** — Trigger backups or commands from external scripts
- **Monitoring** — Poll server stats and alert on high CPU/RAM usage
