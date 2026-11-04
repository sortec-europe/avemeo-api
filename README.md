# Avemeo API & AI Connector

**Avemeo** is a cloud platform for digital signage, hotel TV and in-store audio/video. This repository documents the **Avemeo REST API** and the **Avemeo AI connector (MCP)**, which lets customers manage their screens, playlists and devices from the AI assistant they already use – Claude, ChatGPT, Gemini and other MCP-compatible tools.

> 🇸🇰 Slovenská verzia: [README.sk.md](README.sk.md)

| | |
|---|---|
| Platform | Avemeo CMS (web), players on LG, Samsung, Vestel, Android, Raspberry Pi and ARRIS VIP4302 IPTV set-top boxes |
| Clouds | Avemeo (`ds.avemeo.com`) and [Business Stream](https://www.telekom.sk/biznis/stredne-velke-firmy/business-stream) by Slovak Telekom (`cloud.tvstream.sk`) |
| REST API | OpenAPI 3 specification, 380+ operations – [overview](docs/api-overview.md) |
| AI connector (MCP) | **In development – a pilot with selected customers is being prepared.** [Details](docs/mcp-connector.md) |
| AI assistant in the CMS | **In development** – the Avemeo team is also building an AI assistant directly into the Avemeo CMS, for customers who do not use their own AI tool. |

## What you can do with Avemeo and AI

With the Avemeo connector you will be able to ask your AI assistant in plain language, in Slovak, Czech or English:

- *"Add the new autumn offer to the reception playlist from Friday, 10 seconds per slide."*
- *"Which store players were offline yesterday during opening hours?"*
- *"Create an English version of the hotel menu and add a language switch."*
- *"Reboot all screens in the Košice group."*
- *"Show me what is playing right now in room 204."*

The assistant will read and change content only in **your** Avemeo account, with **your** permissions. Every change will be shown for approval first and recorded in the audit log. See [use cases](docs/use-cases.md).

## Features of the Avemeo platform

- **Digital signage** – visual screen editor with widgets (text, images, video, clock, weather, name days, RSS, apps), playlists and time-based schedulers with weekdays, date ranges and public holidays.
- **Interactive screens** – multi-level menus controlled by a remote control or touch, multilingual content with a language switch.
- **Hotel TV** – live TV channels (HLS) with EPG, guest name and room on screen, guest account, messages, check-in/check-out integration with hotel systems, Netflix / YouTube / Chromecast apps.
- **In-store audio and video** – music and spots on shuffle, campaigns per store, proof-of-play statistics per device, screen and media file with CSV export.
- **Device management** – power on/off, reload, reboot, volume, TV channel, screenshots, online/offline monitoring with e-mail and SMS alerts.
- **Self-service kiosks and more** – hotel kiosk, queue system, quizzes, digital menu boards.

## Quick start: REST API

```bash
BASE_URL=https://cloud.tvstream.sk/backend   # or your Avemeo cloud

# 1. Sign in – the response contains the access token (accessKey)
curl -s -X POST "$BASE_URL/api/auth/login" \
  -H "Content-Type: application/json" \
  -d '{"username":"YOUR_USER","password":"YOUR_PASSWORD"}'

# 2. List playlists of your account
curl -s -X POST "$BASE_URL/api/playlist" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Active-Profile-Id: $ACCOUNT_ID" \
  -H "Content-Type: application/json" \
  -d '{"filter":{},"page_number":1,"page_size":100,"sort_field":"id","sort_order":"asc"}'
```

Full specification: `https://<your-cloud>/backend/openapi/`. Details and authentication: [docs/api-overview.md](docs/api-overview.md).

## AI connector (MCP)

The Avemeo connector is a remote [Model Context Protocol](https://modelcontextprotocol.io) server. When it is available for your account, you add it to your AI assistant once:

1. In your AI assistant open the connectors settings (in Claude: **Customize → Connectors → Add custom connector**).
2. Enter the connector URL for your cloud:
   - Avemeo (`ds.avemeo.com`): `https://mcp.avemeo.com`
   - [Business Stream](https://www.telekom.sk/biznis/stredne-velke-firmy/business-stream) (`cloud.tvstream.sk`): `https://mcp.tvstream.sk`
3. Sign in with your Avemeo account and choose what the assistant may access.

Status, tools and security: [docs/mcp-connector.md](docs/mcp-connector.md).

## AI assistant in the CMS

Not everyone uses their own AI tool. The Avemeo team is therefore also developing an AI assistant built directly into the Avemeo CMS. It will use the same tools as the connector, show a preview of every change in the CMS and ask for approval before saving. Status: in development.

## Contact

- Avemeo: [avemeo.sk](https://avemeo.sk), [avemeo@sortec.sk](mailto:avemeo@sortec.sk)
- Sales, deployment and pilot program (Slovakia): **SORTEC EUROPE s.r.o.** – distributor and business & development partner of Avemeo, partner for [Business Stream](https://www.telekom.sk/biznis/stredne-velke-firmy/business-stream) by Slovak Telekom. [avemeo@sortec.sk](mailto:avemeo@sortec.sk)

---

This repository is maintained by **SORTEC EUROPE s.r.o.**, distributor and business & development partner of Avemeo and partner for [Business Stream](https://www.telekom.sk/biznis/stredne-velke-firmy/business-stream) by Slovak Telekom. Avemeo is a product of Avemeo s.r.o. Documentation is licensed under [CC BY 4.0](LICENSE).
