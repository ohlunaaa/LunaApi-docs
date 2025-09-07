# API Documentation

This API provides various endpoints for retrieving Minecraft player data, Discord information, and game statistics.

## Base URL
```
join the dc an do /api
```

## Endpoints

### 1. Chat Data
Retrieve chat data for a specific UUID.

**Endpoint:** `GET /chat/{uuid}` or `GET /chat?uuid={uuid}`

**Parameters:**
- `uuid` (string, required): Player UUID

**Response:**
```json
{
  "history": [
    {
      "botId": 1,
      "message": "Hello world",
      "prefix": "§7[22⚫] §b[MVP§f+§b] PlayerName§f",
      "timestamp": 1757245512.401,
      "username": "PlayerName"
    },
    {
      "botId": 1,
      "message": "Another message",
      "prefix": "§7[22⚫] §b[MVP§f+§b] PlayerName§f",
      "timestamp": 1757245515.123,
      "username": "PlayerName"
    }
  ]
}
```

**Response Fields:**
- `history` (array): Array of chat messages
  - `botId` (number): Bot identifier
  - `message` (string): The actual chat message content
  - `prefix` (string): Player's formatted prefix with rank colors and level (contains Minecraft color codes)
  - `timestamp` (number): Unix timestamp with milliseconds
  - `username` (string): Player's username

**Error Response:**
```json
{
  "error": "UUID missing"
}
```

**Example:**
```bash
GET /chat/550e8400-e29b-41d4-a716-446655440000
```

---

### 2. UUID to Username Conversion
Convert a Minecraft UUID to a username using Mojang's API.

**Endpoint:** `GET /uuid/{uuid}` or `GET /uuid?uuid={uuid}`

**Parameters:**
- `uuid` (string, required): Minecraft player UUID

**Response:**
```json
{
  "uuid": "550e8400-e29b-41d4-a716-446655440000",
  "name": "PlayerName"
}
```

**Error Responses:**
```json
{
  "error": "UUID missing"
}
```
```json
{
  "error": "UUID not found"
}
```

**Example:**
```bash
GET /uuid/550e8400-e29b-41d4-a716-446655440000
```

---

### 3. Daily Scoreboard
Retrieve daily scoreboard data.

**Endpoint:** `GET /daily`

**Parameters:** None

**Response:**
```json
{
  "Daily Beds Broken": [
    {
      "name": "PlayerName [GUILD]",
      "placement": 1,
      "raw": "§e1. §6PlayerName§r§3 [GUILD]§7 - §r§e450",
      "timestamp": "2025-09-07T15:37:44.655Z",
      "value": 450
    }
  ],
  "Daily Final Kills": [
    {
      "name": "PlayerName [GUILD]",
      "placement": 1,
      "raw": "§e1. §6PlayerName§r§3 [GUILD]§7 - §r§e700",
      "timestamp": "2025-09-07T15:37:44.648Z",
      "value": 700
    }
  ],
  "Daily Wins": [
    {
      "name": "PlayerName [GUILD]",
      "placement": 1,
      "raw": "§e1. §6PlayerName§r§3 [GUILD]§7 - §r§e145",
      "timestamp": "2025-09-07T15:37:44.658Z",
      "value": 145
    }
  ]
}
```

**Error Response:**
```json
{
  "error": "Error message"
}
```

**Example:**
```bash
GET /daily
```

---

### 4. Discord User Information
Retrieve Discord user information including name and display name history.

**Endpoint:** `GET /discord/info/{user_id}` or `GET /discord/info?id={user_id}`

**Parameters:**
- `user_id` (string, required): Discord user ID

**Response:**
```json
{
  "names": [
    {
      "name": "username",
      "fetched_at": "2024-01-01T00:00:00Z"
    }
  ],
  "displays": [
    {
      "display": "Display Name",
      "fetched_at": "2024-01-01T00:00:00Z"
    }
  ]
}
```

**Error Response:**
```json
{
  "error": "User ID fehlt"
}
```

**Example:**
```bash
GET /discord/info/123456789012345678
```

---

### 5. Ping Data
Retrieve ping/latency data for a player.

**Endpoint:** `GET /ping/{uuid}` or `GET /ping?uuid={uuid}`

**Parameters:**
- `uuid` (string, required): Player UUID

**Response:**
```json
{
  "history": {
    "2025-08-22": {
      "avg": 145.9066985645933,
      "datetime": "2025-08-22T23:28:05+02:00",
      "max": 227,
      "min": 0,
      "unix": 1755898085
    },
    "2025-08-30": {
      "avg": 135,
      "datetime": "2025-08-30T02:19:04+02:00",
      "max": 207,
      "min": 125,
      "unix": 1756513144
    },
    "2025-09-07": {
      "avg": 144,
      "datetime": "2025-09-07T14:09:17+02:00",
      "max": 259,
      "min": 129,
      "unix": 1757246957
    }
  },
  "last_ping": 141,
  "last_updated": 1757246957,
  "uuid": "f000dba1-531c-4589-822e-7249f2704809"
}
```

**Response Fields:**
- `history` (object): Historical ping data organized by date (YYYY-MM-DD)
  - `avg` (number): Average ping for that day
  - `datetime` (string): ISO datetime with timezone
  - `max` (number): Maximum ping recorded that day
  - `min` (number): Minimum ping recorded that day
  - `unix` (number): Unix timestamp
- `last_ping` (number): Most recent ping value in milliseconds
- `last_updated` (number): Unix timestamp of last update
- `uuid` (string): Player's UUID

**Error Response:**
```json
{
  "error": "UUID missing"
}
```

**Example:**
```bash
GET /ping/550e8400-e29b-41d4-a716-446655440000
```

---

### 6. Player Skin Data
Retrieve Minecraft player skin and cape URLs.

**Endpoint:** `GET /skin/{uuid}` or `GET /skin?uuid={uuid}`

**Parameters:**
- `uuid` (string, required): Minecraft player UUID

**Response:**
```json
{
  "uuid": "550e8400-e29b-41d4-a716-446655440000",
  "name": "PlayerName",
  "skin_url": "https://textures.minecraft.net/texture/...",
  "cape_url": "https://textures.minecraft.net/texture/..." // null if no cape
}
```

**Error Responses:**
```json
{
  "error": "UUID fehlt"
}
```
```json
{
  "error": "Textures nicht gefunden"
}
```

**Example:**
```bash
GET /skin/550e8400-e29b-41d4-a716-446655440000
```

---

### 7. Weekly Scoreboard
Retrieve weekly scoreboard data.

**Endpoint:** `GET /weekly`

**Parameters:** None

**Response:**
```json
{
  "Weekly Beds Broken": [
    {
      "name": "PlayerName [GUILD]",
      "placement": 1,
      "raw": "§e1. §6PlayerName§r§3 [GUILD]§7 - §r§e450",
      "timestamp": "2025-09-07T15:37:44.655Z",
      "value": 450
    }
  ],
  "Weekly Final Kills": [
    {
      "name": "PlayerName [GUILD]",
      "placement": 1,
      "raw": "§e1. §6PlayerName§r§3 [GUILD]§7 - §r§e700",
      "timestamp": "2025-09-07T15:37:44.648Z",
      "value": 700
    }
  ],
  "Weekly Wins": [
    {
      "name": "PlayerName [GUILD]",
      "placement": 1,
      "raw": "§e1. §6PlayerName§r§3 [GUILD]§7 - §r§e145",
      "timestamp": "2025-09-07T15:37:44.658Z",
      "value": 145
    }
  ]
}
```

**Response Fields:**
- Each category contains an array of top 10 players
- `name` (string): Player name with guild tag in brackets
- `placement` (number): Player's ranking position (1-10)
- `raw` (string): Raw formatted string with Minecraft color codes
- `timestamp` (string): ISO 8601 timestamp when data was recorded
- `value` (number): The actual statistic value

**Error Response:**
```json
{
  "error": "Error message"
}
```

**Example:**
```bash
GET /weekly
```

---

### 8. Win Streak Data
Retrieve win streak information for a player.

**Endpoint:** `GET /winstreak/{uuid}` or `GET /winstreak?uuid={uuid}`

**Parameters:**
- `uuid` (string, required): Player UUID

**Response:**
```json
{
  "bedwars_duel_winstreak": 9,
  "eight_one_winstreak": 0,
  "eight_two_winstreak": 0,
  "four_four_winstreak": 1,
  "four_three_winstreak": 0,
  "last_updated": 1757259731,
  "overall_winstreak": 0,
  "two_four_winstreak": 0,
  "uuid": "5830c67e-5609-40c9-80d7-d4e3e6e821e4"
}
```

**Response Fields:**
- `bedwars_duel_winstreak` (number): Current win streak in Bedwars Duels
- `eight_one_winstreak` (number): Current win streak in 8v8 Solo mode
- `eight_two_winstreak` (number): Current win streak in 8v8 Doubles mode
- `four_four_winstreak` (number): Current win streak in 4v4 mode
- `four_three_winstreak` (number): Current win streak in 4v4 Teams of 3 mode
- `two_four_winstreak` (number): Current win streak in 4v4 Teams of 2 mode
- `overall_winstreak` (number): Overall current win streak across all modes
- `last_updated` (number): Unix timestamp of last update
- `uuid` (string): Player's UUID

**Error Response:**
```json
{
  "error": "UUID missing"
}
```

**Example:**
```bash
GET /winstreak/550e8400-e29b-41d4-a716-446655440000
```

---

## HTTP Status Codes

| Status Code | Description |
|-------------|-------------|
| 200 | OK - Request successful |
| 400 | Bad Request - Missing required parameters |
| 404 | Not Found - Resource not found (e.g., invalid UUID) |
| 500 | Internal Server Error - Server error or external API failure |

## Rate Limiting

If an external service is unavailable, the endpoint will return a 500 error with details.

## Error Handling

All endpoints return consistent error responses in the following format:
```json
{
  "error": "Error description"
}
```

## Notes

- UUIDs should be provided without dashes for Minecraft-related endpoints
- All responses are in JSON format
- External API dependencies may affect endpoint availability
