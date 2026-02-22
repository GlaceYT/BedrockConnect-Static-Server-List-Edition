<div align="center">
  <img src="https://i.ibb.co/GfTxbJfC/7-edited.png" alt="Banner" width="100%"/>
</div>
# BedrockConnect - Static Server List Edition

A customized version of [BedrockConnect](https://github.com/Pugmatt/BedrockConnect) with a **locked, admin-controlled server list**, **server groups/categories**, **rank-based access control**, and **live server status pinging**.

<img src="https://i.imgur.com/H9zVzGT.png" alt="Bedrock Block" align="right" width="120">

## ✨ Features

✅ Static server list (users can't add/edit/remove)  
✅ **Server groups** — organize servers into categories with icons  
✅ Per-server rank restrictions (whitelist/blacklist)  
✅ Custom colored rank badges  
✅ Live server status with player count (e.g., `● 1/30 online`)  
✅ Custom icons per server & per group  
✅ Optional exit button  
✅ Single config file — no database required  
✅ Based on **BedrockConnect 1.65** (Minecraft 26.0 support)

---

## 📦 What's Included

```
├── BedrockConnect-1.0-SNAPSHOT.jar    ← The server (run this)
└── static_servers.json                ← Your server config (edit this)
```

## 🚀 Quick Start

1. **Install Java 8+** if not already installed
2. Put both files in the same folder
3. Edit `static_servers.json` with your servers
4. Run:
```bash
java -jar BedrockConnect-1.0-SNAPSHOT.jar nodb=true static_server_list=static_servers.json
```
5. Connect your Minecraft Bedrock client to: `YOUR_IP:19132`

### Command Line Options
```bash
java -jar BedrockConnect-1.0-SNAPSHOT.jar                            # Default settings
java -jar BedrockConnect-1.0-SNAPSHOT.jar nodb=true                  # No database (recommended)
java -jar BedrockConnect-1.0-SNAPSHOT.jar port=19133                 # Custom port
java -jar BedrockConnect-1.0-SNAPSHOT.jar nodb=true static_server_list=servers.json  # Custom config path
```

---

## 📝 Configuration Guide (`static_servers.json`)

The config file supports **two formats** — grouped and flat. The format is auto-detected.

### 📂 Grouped Format (Recommended)

Organize servers into **categories/groups**. The main menu shows group buttons, and clicking a group opens a sub-menu with servers inside.

```json
[
  {
    "name": "Public Servers",
    "iconUrl": "https://example.com/public-icon.png",
    "content": [
      {
        "name": "Survival Server",
        "address": "play.example.com",
        "port": 19132,
        "iconUrl": "https://example.com/survival.png"
      },
      {
        "name": "Creative World",
        "address": "play.example.com",
        "port": 19133,
        "iconUrl": "https://example.com/creative.png"
      }
    ]
  },
  {
    "name": "Staff Servers",
    "iconUrl": "https://example.com/staff-icon.png",
    "content": [
      {
        "name": "Admin Server",
        "address": "admin.example.com",
        "port": 19132,
        "rankName": "ADMIN",
        "rankFormat": "§8[§c§lADMIN§8]",
        "allowedPlayers": ["AdminPlayer1", "AdminPlayer2"]
      }
    ]
  }
]
```

**How groups work:**
- Main menu shows **group buttons** with their icons (e.g., Public Servers, Staff Servers)
- Clicking a group opens a **sub-menu** with its servers + a **← Back** button
- Groups **auto-hide** if a player has no access to any server inside
- Each server inside a group supports all the same properties (icons, ranks, allowedPlayers, etc.)

### 📋 Flat Format

A simple list without grouping — all servers show on one page.

```json
{
  "showExitButton": false,
  "showServerStatus": true,
  "servers": [
    {
      "name": "My Server",
      "address": "play.myserver.com",
      "port": 19132,
      "iconUrl": "https://i.imgur.com/3BmFZRE.png"
    }
  ]
}
```

---

## 📑 Property Reference

### Global Options (Flat Format)

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `showExitButton` | boolean | `false` | Show "Exit" button at the top |
| `showServerStatus` | boolean | `true` | Show online/offline status + player count |

### Group Properties (Grouped Format)

| Field | Required | Description |
|-------|----------|-------------|
| `name` | ✅ | Display name of the group/category |
| `iconUrl` | ❌ | Square PNG URL for group icon |
| `content` | ✅ | Array of server objects within this group |

### Server Properties

| Field | Required | Description |
|-------|----------|-------------|
| `name` | ✅ | Display name |
| `address` | ✅ | Server IP/domain |
| `port` | ❌ | Port (default: `19132`) |
| `iconUrl` | ❌ | Square PNG URL for button icon |
| `rankName` | ❌ | Rank badge text (e.g., `"VIP"`, `"STAFF"`) |
| `rankColor` | ❌ | Color code for badge (e.g., `"§6"` for gold). Default: `"§e"` (yellow) |
| `rankFormat` | ❌ | Full custom rank format — overrides rankName/rankColor |
| `allowedPlayers` | ❌ | Whitelist — only these players can see/join (empty = everyone can access) |
| `blockedPlayers` | ❌ | Blacklist — hide from and block these players |

---

## 🎨 Color Codes

### Colors
| Code | Color | Code | Color |
|------|-------|------|-------|
| `§0` | Black | `§8` | Dark Gray |
| `§1` | Dark Blue | `§9` | Blue |
| `§2` | Dark Green | `§a` | Green |
| `§3` | Dark Aqua | `§b` | Aqua |
| `§4` | Dark Red | `§c` | Red |
| `§5` | Dark Purple | `§d` | Light Purple |
| `§6` | Gold | `§e` | Yellow |
| `§7` | Gray | `§f` | White |

### Formatting
| Code | Effect |
|------|--------|
| `§l` | **Bold** |
| `§o` | *Italic* |
| `§r` | Reset |

---

## 🔒 Rank/Permission Examples

### VIP Server (Gold badge)
```json
{
  "name": "VIP Lounge",
  "address": "vip.myserver.com",
  "port": 19132,
  "rankName": "VIP",
  "rankColor": "§6",
  "allowedPlayers": ["VIPPlayer1", "VIPPlayer2"]
}
```
**Result:** `VIP Lounge [VIP]` (gold colored badge) — only VIPPlayer1 and VIPPlayer2 can see it

### Staff Server (Custom format)
```json
{
  "name": "Staff Server",
  "address": "staff.myserver.com",
  "port": 19132,
  "rankName": "Staff",
  "rankFormat": "§8[§c§lADMIN§8]",
  "allowedPlayers": ["AdminName"]
}
```
**Result:** `Staff Server [ADMIN]` (bold red text in gray brackets)

### Blocked Players
```json
{
  "name": "Public Server",
  "address": "play.myserver.com",
  "port": 19132,
  "blockedPlayers": ["BannedPlayer1", "TrollPlayer"]
}
```
**Result:** Everyone can see/join except BannedPlayer1 and TrollPlayer

---

## 📊 Server Status Display

When `showServerStatus` is enabled (default `true`), each server button shows live status:

- 🟢 **Online:** `● 1/30 online` (green dot, yellow text)
- 🔴 **Offline:** `● OFFLINE` (red)

Status is cached for **30 seconds** to avoid excessive pinging.

---

## � Full Grouped Example

Here's a real-world grouped configuration:

```json
[
  {
    "name": "Public Servers",
    "iconUrl": "https://i.postimg.cc/3xhYRLSt/Public-Servers.png",
    "content": [
      {
        "name": "Survival",
        "address": "play.example.com",
        "port": 19132,
        "iconUrl": "https://i.postimg.cc/kgPhL60v/Survival.png"
      },
      {
        "name": "Minigames",
        "address": "play.example.com",
        "port": 19133,
        "iconUrl": "https://i.postimg.cc/gcKCNsZj/Minigames.png"
      }
    ]
  },
  {
    "name": "Event Servers",
    "iconUrl": "https://i.postimg.cc/8Cv9MnBH/Events.png",
    "content": [
      {
        "name": "Tournament Server",
        "address": "play.example.com",
        "port": 19134,
        "iconUrl": "https://i.postimg.cc/PJYVvmwX/Tournament.png",
        "allowedPlayers": ["Player1", "Player2", "Player3"]
      }
    ]
  },
  {
    "name": "Staff Servers",
    "iconUrl": "https://i.postimg.cc/m2rY0zqZ/Staff.png",
    "content": [
      {
        "name": "Training Server",
        "address": "play.example.com",
        "port": 19135,
        "rankName": "TRAINEE",
        "rankFormat": "§8[§9§lTRAINEE§8]",
        "allowedPlayers": ["Staff1", "Staff2"]
      }
    ]
  },
  {
    "name": "Private Servers",
    "iconUrl": "https://i.postimg.cc/FH7xJdgJ/Private.png",
    "content": [
      {
        "name": "My Private Server",
        "address": "play.example.com",
        "port": 19136,
        "allowedPlayers": ["Owner", "Friend1", "Friend2"]
      }
    ]
  }
]
```

---

## 💡 Tips

1. **Icon URLs** must be direct image links (PNG recommended). Use Imgur, postimg.cc, or similar.
2. **Player names** are **case-insensitive** in `allowedPlayers` / `blockedPlayers`.
3. **Restart the server** after editing `static_servers.json` to apply changes.
4. **Status pinging** adds ~1-2 second delay when opening the list. Set `showServerStatus: false` to disable.
5. **Groups auto-hide** — if a player can't access any server in a group, the entire group is hidden from their menu.
6. **No database needed** — use `nodb=true` for a fully file-based setup.

---

## 🔧 Based On

[BedrockConnect](https://github.com/Pugmatt/BedrockConnect) by [Pugmatt](https://github.com/Pugmatt) — v1.65 (Minecraft Bedrock 26.0 support)

[![License: GPL v3](https://img.shields.io/badge/License-GPL%20v3-blue.svg)](http://www.gnu.org/licenses/gpl-3.0)
