# Avemeo REST API – overview

> 🇸🇰 Slovenská verzia: [sk/api-overview.md](sk/api-overview.md) · ⬅ Back to [README](../README.md)

The **Avemeo REST API** is the programming interface of the Avemeo cloud platform for digital signage, hotel TV and in-store audio. It is the **same API the Avemeo CMS web application uses**, so everything you can do in the CMS – media, screens, playlists, schedulers, devices, remote control, statistics – can also be done from your own software. It is described by an **OpenAPI 3** specification published on every Avemeo cloud.

Typical uses:

- integrate Avemeo with a **hotel system (PMS)**, ERP, booking or marketing platform,
- automate recurring content changes (campaigns, seasonal menus, price lists),
- build **monitoring and reporting** on top of device states and proof-of-play statistics,
- power the [Avemeo AI connector (MCP)](mcp-connector.md), which uses this API under the hood.

## Where to find the specification

| | |
|---|---|
| Interactive documentation (Swagger UI) | `https://<your-cloud>/backend/openapi/` |
| Specification file (JSON) | `https://<your-cloud>/backend/api/openapi/doc` |
| Server base path | `/backend` |
| Size | 380+ operations across 350+ paths |

Replace `<your-cloud>` with the cloud your account lives on:

| Cloud | Host | Example base URL |
|---|---|---|
| Avemeo | `ds.avemeo.com` | `https://ds.avemeo.com/backend` |
| [Business Stream](https://www.telekom.sk/biznis/stredne-velke-firmy/business-stream) by Slovak Telekom | `cloud.tvstream.sk` | `https://cloud.tvstream.sk/backend` |

You need an Avemeo account on that cloud to use the API. The specification contains inline schemas and, at the moment, no field descriptions – this page and the [glossary](glossary.md) fill in the context.

## Authentication

| Method | Header | Used for |
|---|---|---|
| **Bearer token (JWT)** | `Authorization: Bearer <token>` | Content and account management. Obtain the token with `POST /api/auth/login`. |
| **Account selection** | `Active-Profile-Id: <account id>` | Selects the Avemeo account (profile) the request works with. One user may have access to several accounts. |
| **API key** | `api-key: <key>` | Remote device control (`/api/remote/…`). |

Sign-in example:

```bash
BASE_URL=https://cloud.tvstream.sk/backend

curl -s -X POST "$BASE_URL/api/auth/login" \
  -H "Content-Type: application/json" \
  -d '{"username":"YOUR_USER","password":"YOUR_PASSWORD"}'
# → {"status":"success","data":{"accessToken":"<JWT>"}}
```

Use the token in every further request together with the account id:

```bash
TOKEN=...        # accessToken from the login response
ACCOUNT_ID=...   # id of the Avemeo account (profile)

curl -s -X POST "$BASE_URL/api/playlist" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Active-Profile-Id: $ACCOUNT_ID" \
  -H "Content-Type: application/json" \
  -d '{"filter":{},"page_number":1,"page_size":100,"sort_field":"id","sort_order":"asc"}'
```

**Keep tokens and API keys secret.** Create a dedicated API user with the minimum permissions needed, do not put tokens in URLs, logs or documents, and rotate the password if a token leaks.

## Response format

Responses are JSON objects with a `status` and a `data` field:

```json
{ "status": "success", "data": { "...": "..." } }
```

On failure `status` is `"error"`. List endpoints return the items together with the total count (for example the device list returns `data.entities` and `data.total_count`).

## Main areas

| Area | Endpoints (examples) | Purpose |
|---|---|---|
| **Folders** | `GET /api/tree/all/{type}/edit`, `POST /api/tree/update` | Folder trees for media, screens, playlists and devices (`{type}` = `medium`, `screen`, `playlist`, `device`) |
| **Media** | `POST /api/media`, `GET /api/media/fetch/{id}`, `PUT /api/media/update`, `POST /api/media/transfer`, `PUT /api/media/setfolder` | Media library: images, video, audio; upload and move between folders |
| **Screens** | `POST /api/screen`, `GET /api/screen/widgets/fetch/{id}`, `PUT /api/screen/widgets/update`, `POST /api/screen/duplicate` | Screen layouts (1920 × 1080 by default) with widgets, interactive levels and translations |
| **Playlists** | `POST /api/playlist`, `GET /api/playlist/fetch/{id}`, `PUT /api/playlist/update`, `POST /api/playlist/duplicate` | Sequences of screens, media and live channels with durations and validity |
| **Schedulers** | `POST /api/scheduler`, `GET /api/scheduler/fetch/{id}`, `PUT /api/scheduler/update` | What plays when: weekdays, times, date ranges, public holidays, power on/off |
| **Devices** | `POST /api/device`, `GET /api/device/fetch/{id}`, `GET /api/device/screenshot/{id}`, `POST /api/device/mcontrol/{action}` | Device list and status; `on`, `off`, `reload`, `reboot` for one or many devices |
| **Device content** | `GET /api/sconnection?type=device&id={id}`, `POST /api/sconnection/update` | Which screen (and level) or scheduler a device plays |
| **Remote control** | `PUT /api/remote/box/power/{state}/{box_id}`, `…/audio/volume/…`, `…/tvchannel/…`, `…/keycode/…` | Power, volume, TV channel and key presses (API key) |
| **Statistics** | `PUT /api/stats/device`, `PUT /api/stats/screenmedium` | Proof of play: per-minute device state, screens and media played per day |
| **Weather, languages, translations** | `/api/weather`, `/api/language`, `/api/translation` | Weather locations, account languages, translations of screen texts |
| **Monitoring** | `/api/monitor` | Offline alerts by e-mail and SMS |

## Examples

### Device state for one day (proof of play)

```bash
curl -s -X PUT "$BASE_URL/api/stats/device" \
  -H "Authorization: Bearer $TOKEN" -H "Active-Profile-Id: $ACCOUNT_ID" \
  -H "Content-Type: application/json" \
  -d '{"id": 2081, "date": "2026-10-31"}'
```

The response contains `states` (one record per minute: `2` = powered on and playing, `1` = output off, `0` = offline), plus the `screens` and `media` played that day. This is the data behind questions such as *"which players were offline yesterday during opening hours?"*.

### Reboot devices

```bash
curl -s -X POST "$BASE_URL/api/device/mcontrol/reboot" \
  -H "Authorization: Bearer $TOKEN" -H "Active-Profile-Id: $ACCOUNT_ID" \
  -H "Content-Type: application/json" \
  -d '{"ids": [2081, 2747]}'
```

Other actions: `on`, `off`, `reload`.

### List devices in a folder

```bash
curl -s -X POST "$BASE_URL/api/device" \
  -H "Authorization: Bearer $TOKEN" -H "Active-Profile-Id: $ACCOUNT_ID" \
  -H "Content-Type: application/json" \
  -d '{"filter":{"tree_id": <folder id>},"page_number":1,"page_size":100}'
```

### Read a screen with its widgets

```bash
curl -s "$BASE_URL/api/screen/widgets/fetch/<screen id>" \
  -H "Authorization: Bearer $TOKEN" -H "Active-Profile-Id: $ACCOUNT_ID"
```

Each widget has a type (`block`, `datetime`, `presentation`, `tv`, `weather_symbol`, …), a `widget_order` (lower = in front) and `params_json` with position (`top`, `left`, `width`, `height`) and content.

## Conventions and tips

- **Lists use `POST` with paging:** `{"filter":{}, "page_number":1, "page_size":100, "sort_field":"id", "sort_order":"asc"}`. Filter by folder with `{"filter":{"tree_id": <folder id>}}`.
- **IDs:** screens, playlists and media have long numeric IDs – treat them as strings in JavaScript and other languages with 53-bit integers. Device IDs are ordinary integers.
- **Folders:** when saving screens and playlists, always send `tree_id` (the folder).
- **JSON in strings:** some fields contain JSON encoded as a string (for example `params_json`, `datetime_json`, `days_json`). Parse them before use and encode them again before saving.
- **Playlist items** reference a screen and a level (`screen_id`, `screen_level`), a `duration` in seconds and an `active` flag; durations of active items add up to the playlist length.
- **Translations** of screen texts live in parameters with a language suffix such as `_lng_en`.
- **Changes on live devices:** after updating a screen that is currently playing, send `reload` to the device so it picks up the change.
- **Back up before writing:** read and store the original object before every update so you can restore it.

## Frequently asked questions

**Is the Avemeo API public?**
The specification is published on every Avemeo cloud and this documentation is public. Using the API requires an Avemeo account with the appropriate permissions.

**Is there a sandbox or test account?**
Write to [avemeo@sortec.sk](mailto:avemeo@sortec.sk) – access for integrators and pilot customers is arranged individually.

**Are there rate limits?**
No public rate limits are documented. Keep automated polling reasonable (for example statistics once per day per device) and contact us before building a high-volume integration.

**Does the API change?**
It evolves together with the CMS. The specification on your cloud is always the current reference; changes to this documentation are tracked in [CHANGELOG.md](../CHANGELOG.md).

**Can I use the API without writing code?**
Yes – that is what the [AI connector (MCP)](mcp-connector.md) is for: your AI assistant calls the API for you, with your permissions and your approval.

## Related

- [AI connector (MCP)](mcp-connector.md) – manage Avemeo from Claude, ChatGPT or Gemini
- [Use cases](use-cases.md) – what the API and the connector are used for
- [Glossary](glossary.md) – screens, widgets, levels, playlists, schedulers, proof of play
- [README](../README.md) – platform overview and contact
