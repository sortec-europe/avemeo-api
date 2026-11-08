# Avemeo REST API

> 🇸🇰 Slovenská verzia: [sk/api-overview.md](sk/api-overview.md) · 🇨🇿 Česká verze: [cs/api-overview.md](cs/api-overview.md) · ⬅ Back to [README](../README.md)

Avemeo, the cloud platform for digital signage, hotel TV and in-store audio, has a **REST API** – the same interface the Avemeo CMS web application uses. It covers media, screens, playlists, schedulers, devices, remote control and statistics, and it is the foundation of the [Avemeo AI connector (MCP)](mcp-connector.md).

## Who can use it

The API is available to **Avemeo customers and their integrators**. The technical documentation (OpenAPI 3 specification, authentication, endpoints, examples) is provided **after sign-in on your Avemeo cloud** and on request – it is not published here, because the current API was designed for the CMS, not as a public interface.

To get access or ask a technical question, write to [avemeo@sortec.sk](mailto:avemeo@sortec.sk) with your company, your cloud (Avemeo or Business Stream) and what you want to integrate.

## What people integrate

| Integration | Typical goal |
|---|---|
| **Hotel system (PMS) → hotel TV** | guest name and room on the TV, check-in/check-out, messages |
| **ERP or price list → menu boards** | automatic price and menu updates |
| **Monitoring → ticketing** | a ticket when a player is offline for too long |
| **Marketing tool → campaigns** | playlists and schedules created for a campaign |
| **Reporting** | proof of play and outage reports across locations |

More scenarios: [Use cases](use-cases.md).

## API v2

The Avemeo team is preparing a **new version of the API (v2)** with its own documentation. Integrations built on the current API will need to migrate to v2 once it is released. If you are planning an integration now, contact us first so that we can advise on the timing.

## No code? Use the AI connector

For customers who do not want to write code, the [AI connector (MCP)](mcp-connector.md) lets an AI assistant – Claude, ChatGPT, Gemini and others – work with your Avemeo account on your behalf, with your permissions and your approval before every change.

## Related

- [AI connector (MCP)](mcp-connector.md) · [Use cases](use-cases.md) · [FAQ](faq.md) · [Glossary](glossary.md)
- [README](../README.md) – platform overview and contact
