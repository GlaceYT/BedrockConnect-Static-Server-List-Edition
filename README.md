<div align="center">

![Logo](https://i.ibb.co/GfTxbJfC/7-edited.png)

# BedrockConnect - Static-Server-List-Edition

![Version](https://img.shields.io/badge/version-0.1-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![Java](https://img.shields.io/badge/Java-8%2B-orange?logo=java)
![Minecraft%20Bedrock](https://img.shields.io/badge/Minecraft-Bedrock-62B47A?logo=minecraft)
![JSON](https://img.shields.io/badge/Config-JSON-black?logo=json)

**A customized version of BedrockConnect with a locked, admin-controlled server list.**

---

### 🔗 Connect With Me

[![YouTube](https://img.shields.io/badge/YouTube-GlaceYT-red?style=for-the-badge&logo=youtube)](https://youtube.com/@GlaceYT)
[![Website](https://img.shields.io/badge/Website-GlaceYT.com-blue?style=for-the-badge&logo=google-chrome)](https://glaceyt.com)
[![Replit](https://img.shields.io/badge/Replit-GlaceYT-orange?style=for-the-badge&logo=replit)](https://replit.com/@GlaceYT)
[![Discord](https://img.shields.io/badge/Discord-Support%20Server-5865F2?style=for-the-badge&logo=discord)](https://discord.gg/xQF9f9yUEM)

---

</div>


## 📦 What's Included

```
Files/
├── BedrockConnect.jar     ← The server (run this)
└── static_servers.json    ← Your server config (edit this)
```

## 🚀 Quick Start

1. **Install Java 8+** if not already installed
2. Put both files in the same folder
3. Edit `static_servers.json` with your servers
4. Run: `java -jar BedrockConnect.jar`
5. Connect your Minecraft Bedrock client to: `YOUR_IP:19132`

### Command Line Options
```bash
java -jar BedrockConnect.jar                    # Default port 19132
java -jar BedrockConnect.jar port=19134         # Custom port
java -jar BedrockConnect.jar nodb=true          # Disable player data storage
```

---

## 📝 Configuration Guide (`static_servers.json`)

### Basic Example
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

### All Options

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `showExitButton` | boolean | `false` | Show "Exit" button |
| `showServerStatus` | boolean | `true` | Show online/offline + player count |

### Server Entry Options

| Field | Required | Description |
|-------|----------|-------------|
| `name` | ✅ | Display name |
| `address` | ✅ | Server IP/domain |
| `port` | ❌ | Port (default: 19132) |
| `iconUrl` | ❌ | Square PNG URL for button icon |
| `rankName` | ❌ | Rank badge text (e.g., "VIP") |
| `rankColor` | ❌ | Color code (e.g., "§6" for gold) |
| `rankFormat` | ❌ | Full custom format (overrides color) |
| `allowedPlayers` | ❌ | Whitelist - only these players see it |
| `blockedPlayers` | ❌ | Blacklist - hide from these players |

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
**Result:** `VIP Lounge [VIP]` (gold colored badge)

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
**Result:** `Staff Server [ADMIN]` (bold red text)

---

## 📊 Server Status Display

When `showServerStatus: true`, each server shows:
- 🟢 **Online:** `●  12/50 online` (green)
- 🔴 **Offline:** `● OFFLINE` (red)

Status is cached for 30 seconds to avoid spam.

---

## 🛡️ Features

✅ Static server list (users can't add/edit/remove)  
✅ Per-server rank restrictions (whitelist/blacklist)  
✅ Custom colored rank badges  
✅ Live server status (player count + online/offline)  
✅ Custom icons per server  
✅ Optional exit button  
✅ Single config file

---

## 💡 Tips

1. **Icon URLs** must be direct image links (ending in `.png`). Use Imgur or similar.
2. **Player names** are case-insensitive in allowedPlayers/blockedPlayers.
3. **Restart the server** after editing `static_servers.json` to apply changes.
4. **Status pinging** adds ~1-2 second delay when opening the list. Set `showServerStatus: false` to disable.
