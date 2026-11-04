# Avemeo REST API – overview

The Avemeo REST API is the same API that the Avemeo CMS web application uses. It is described by an OpenAPI 3 specification available on every Avemeo cloud:

- Interactive documentation: `https://<your-cloud>/backend/openapi/`
- Specification file: `https://<your-cloud>/backend/api/openapi/doc`
- Server base path: `/backend`

## Authentication

| Method | Header | Used for |
|---|---|---|
| Bearer token (JWT) | `Authorization: Bearer <token>` | Content and account management. Obtain the token with `POST /api/auth/login`. |
| Account selection | `Active-Profile-Id: <account id>` | Selects the Avemeo account (profile) the request works with. |
| API key | `api-key: <key>` | Remote device control (`/api/remote/…`). |

Keep tokens and API keys secret. Use a dedicated user with the minimum permissions needed.

## Main areas

| Area | Endpoints (examples) | Purpose |
|---|---|---|
| Folders | `GET /api/tree/all/{type}/edit`, `POST /api/tree/update` | Folder trees for media, screens, playlists and devices |
| Media | `POST /api/media`, `GET /api/media/fetch/{id}`, `PUT /api/media/update`, `POST /api/media/transfer` | Media library: images, video, audio |
| Screens | `POST /api/screen`, `GET /api/screen/widgets/fetch/{id}`, `PUT /api/screen/widgets/update`, `POST /api/screen/duplicate` | Screen layouts with widgets and interactive levels |
| Playlists | `POST /api/playlist`, `GET /api/playlist/fetch/{id}`, `PUT /api/playlist/update`, `POST /api/playlist/duplicate` | Sequences of screens, media and live channels with durations |
| Schedulers | `POST /api/scheduler`, `GET /api/scheduler/fetch/{id}`, `PUT /api/scheduler/update` | What plays when: weekdays, times, date ranges, public holidays |
| Devices | `POST /api/device`, `GET /api/device/fetch/{id}`, `GET /api/device/screenshot/{id}`, `POST /api/device/mcontrol/{action}` | Device list and status; `on`, `off`, `reload`, `reboot` for one or many devices |
| Remote control | `PUT /api/remote/box/power/{state}/{box_id}`, `…/audio/volume/…`, `…/tvchannel/…`, `…/keycode/…` | Power, volume, TV channel and key presses (API key) |
| Statistics | `PUT /api/stats/device`, `PUT /api/stats/screenmedium` | Proof of play: per-minute device state, screens and media played per day |
| Weather, languages, translations | `/api/weather`, `/api/language`, `/api/translation` | Weather locations, account languages, translations |
| Monitoring | `/api/monitor` | Offline alerts by e-mail and SMS |

## Examples

**Device state for one day (proof of play)**

```bash
curl -s -X PUT "$BASE_URL/api/stats/device" \
  -H "Authorization: Bearer $TOKEN" -H "Active-Profile-Id: $ACCOUNT_ID" \
  -H "Content-Type: application/json" \
  -d '{"id": 2081, "date": "2026-10-31"}'
```

The response contains `states` (one record per minute: `2` = powered on, `1` = output off, `0` = offline), `screens` and `media` played that day.

**Reboot devices**

```bash
curl -s -X POST "$BASE_URL/api/device/mcontrol/reboot" \
  -H "Authorization: Bearer $TOKEN" -H "Active-Profile-Id: $ACCOUNT_ID" \
  -H "Content-Type: application/json" \
  -d '{"ids": [2081, 2747]}'
```

## Notes

- Lists use `POST` with paging: `{"filter":{}, "page_number":1, "page_size":100, "sort_field":"id", "sort_order":"asc"}`. Filter by folder with `{"filter":{"tree_id": <folder id>}}`.
- When saving screens and playlists, send `tree_id` (the folder).
- Some fields contain JSON as a string (for example `params_json`, `datetime_json`).
