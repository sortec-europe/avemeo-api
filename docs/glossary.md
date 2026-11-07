# Glossary – digital signage, hotel TV, Avemeo and MCP terms

> 🇸🇰 Slovenská verzia: [sk/glossary.md](sk/glossary.md) · 🇨🇿 Česká verze: [cs/glossary.md](cs/glossary.md) · ⬅ Back to [README](../README.md)

Short definitions of the terms used in this documentation, in the Avemeo CMS and in the AI connector. Alphabetical.

**Account (profile)** – a customer space in Avemeo with its own media, screens, playlists, schedulers, devices and users. One user may have access to several accounts; API requests select the account with the `Active-Profile-Id` header.

**Audit log** – a record of every action, including those made through the AI connector, with the user, the client and the time.

**Avemeo** – a cloud platform (CMS) for digital signage, hotel TV and in-store audio and video, developed by Avemeo s.r.o. Operated in the Avemeo cloud (`ds.avemeo.com`) and, as Business Stream, by Slovak Telekom (`cloud.tvstream.sk`).

**Business Stream** – a digital signage and hotel TV service of Slovak Telekom that runs on the Avemeo platform.

**CMS (content management system)** – the web application in which content is created, scheduled and assigned to devices. In Avemeo the CMS and the REST API share the same backend.

**Device (player)** – the hardware that plays content: an LG, Samsung or Vestel display with a built-in player, an Android player or TV, a Raspberry Pi or an ARRIS IPTV set-top box. Each device is assigned a screen (and level) or a scheduler.

**Device content** – the assignment of what a device plays: a screen with a level, or a scheduler.

**Digital signage** – centrally managed content on screens in public and commercial spaces: promotions, menus, information, wayfinding, live TV.

**EPG (electronic programme guide)** – the TV programme listing shown in the hotel TV player.

**HLS (HTTP Live Streaming)** – the streaming format used for live TV channels in Avemeo.

**Hotel TV / hospitality IPTV** – TV for hotel rooms with live channels, a welcome screen with the guest's name, an interactive services menu, messages and apps (Netflix, YouTube, Chromecast). IPTV delivers channels over the hotel's IP network.

**Interactive menu** – a screen with several levels that the guest or visitor navigates with a remote control or by touch, often in several languages.

**Level** – one state of an interactive screen (for example the main menu, the restaurant page, the language selection). Widgets are visible or active on specific levels; buttons switch between levels.

**MCP (Model Context Protocol)** – an open standard for connecting AI assistants to external tools and data. A *remote MCP server* is hosted on the internet and used by the assistant over HTTPS with OAuth sign-in. The Avemeo AI connector is a remote MCP server.

**MCP client** – an AI application that can use MCP servers: Claude, ChatGPT, Gemini CLI, Cursor, VS Code and others.

**OAuth** – the sign-in standard used by the AI connector. The user signs in on the Avemeo page; the assistant receives a limited, revocable token and never sees the password.

**OpenAPI** – a standard, machine-readable description of a REST API. Avemeo publishes an OpenAPI 3 specification on every cloud at `/backend/openapi/`.

**Plan (two-step write)** – in the AI connector, every change is first prepared as a plan with a before/after summary and applied only after the user approves it.

**Playlist** – an ordered sequence of items (screens, media, live channels) with a duration in seconds for each item, played in a loop. Items can have validity dates and times.

**PMS (property management system)** – the hotel's front-office system. Avemeo's hotel TV integrates with hotel systems for check-in and check-out.

**Presentation widget** – a full-screen widget that plays a playlist on a screen.

**Proof of play** – statistics proving what played where and when: per-minute device state and the screens and media played each day. Used for advertising reports and outage analysis.

**Remote control API** – API endpoints (authenticated with an API key) for power, volume, TV channel and key presses on a device.

**Scheduler** – defines what plays when: time slots with weekdays, times, date ranges and public holidays, optionally with power on/off per slot. A device can be assigned a scheduler instead of a single screen.

**Screen** – a layout (1920 × 1080 by default) composed of widgets; the basic unit of content in Avemeo. A screen can have several levels and translations.

**Scheduled task** – a feature of some AI assistants (for example Claude) that runs a prompt on a schedule, for example a daily outage report through the connector.

**Template** – a ready-made screen or menu in Avemeo that is duplicated and filled with the customer's texts, images and languages.

**Widget** – a building block of a screen: text block, image, video, clock, date, weather, name days, RSS, TV player, presentation (playlist player), apps and more. Each widget has a position, size, order (lower = in front) and parameters.
