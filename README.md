
# API Documentation

## Overview

This API provides various endpoints to interact with Hypixel data, Minecraft Bedwars Quickbuy items, mailbox management and more.

---

## Authentication

**API Key**

- Some endpoints require an API key for authentication.
- Pass as query parameter `api_key` or header `X-API-Key`.
- Example: `?api_key=your_secret_api_key_123`

---

## Endpoints

### 1. `/v2/quickbuy`

**Description:**  
Generates an image of the quickbuy inventory for a Minecraft player (Bedwars).

**Method:** GET  
**Parameters:**  
- `name` (string, required): Minecraft player name.

**Response:**  
- 200: PNG image of the quickbuy inventory layout.  
- 400: Missing `name` parameter.  
- 404: Player not found.

**Example:**  
`GET /v2/quickbuy?name=MinecraftPlayer123`

---


### 3. Hypixel Endpoints

These endpoints fetch data from the official Hypixel API.

#### a) `/hypixel/punishmentstats`

**Description:**  
Returns Hypixel punishment stats.

**Method:** GET  
**Response:** JSON data.

---

#### b) `/hypixel/leaderboards`

**Description:**  
Returns current Hypixel leaderboards.

**Method:** GET  
**Response:** JSON data.

---

#### c) `/hypixel/counts`

**Description:**  
Returns Hypixel player and server counts.

**Method:** GET  
**Response:** JSON data.

---

#### d) `/hypixel/boosters`

**Description:**  
Returns active boosters on Hypixel.

**Method:** GET  
**Response:** JSON list of booster details:

```json
[
  {
    "booster_id": "string",
    "player_name": "string",
    "uuid": "string",
    "game_type": "string",
    "amount": number,
    "length": "HH:MM:SS",
    "date_activated": "YYYY-MM-DD HH:MM:SS UTC"
  },
  ...
]
```

---

### 4. Mailbox Management

#### a) `/create`

**Description:**  
Creates a new mailbox.

**Method:** GET  
**Parameters:**  
- `name` (string, required)  
- `password` (string, required)  

**Response:**  
- 200/201: JSON with mailbox details.  
- 400: Missing parameters.  
- Error details otherwise.

---


#### c) `/delete/<mailbox_id>`

**Description:**  
Deletes the mailbox with the specified ID.

**Method:** DELETE  
**Response:**  
- 200/204: Successfully deleted.  
- Error details on failure.

---

### 5. `/scoreboard`

**Description:**  
Returns scoreboard data from various JSON files.

**Method:** GET  
**Parameters:**  
- `raw` (optional, `true`/`false`): Return raw data.  
- `weekly` (optional, `true`/`false`): Return weekly data.

**Response:**  
- 200: JSON scoreboard data.  
- 404: File not found.  
- 500: Error reading file.

**Example:**  
`GET /scoreboard?raw=true&weekly=false`

---


## Error Codes

| Status Code | Meaning                         |
|-------------|--------------------------------|
| 200         | OK / Success                   |
| 400         | Missing or invalid parameters  |
| 401         | Unauthorized (missing/invalid API key) |
| 404         | Resource not found             |
| 500         | Internal server error          |


