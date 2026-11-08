# Frequently asked questions – Avemeo, REST API and AI connector

> 🇸🇰 Slovenská verzia: [sk/faq.md](sk/faq.md) · 🇨🇿 Česká verze: [cs/faq.md](cs/faq.md) · ⬅ Back to [README](../README.md)

**Contents:** [About Avemeo](#about-avemeo) · [REST API](#rest-api) · [AI connector (MCP)](#ai-connector-mcp) · [Security and data](#security-and-data) · [Pilot, pricing and contact](#pilot-pricing-and-contact)

## About Avemeo

**What is Avemeo?**
Avemeo is a cloud platform (CMS) for digital signage, hotel TV and in-store audio and video, developed by Avemeo s.r.o. From one web application it manages what plays on screens, hotel TVs and audio players: content, playlists, schedules, devices and statistics.

**What is digital signage?**
Digital signage means displaying content – promotions, menus, information, wayfinding, live TV – on screens in public and commercial spaces, managed centrally. Avemeo is the software (CMS) that creates, schedules and distributes that content and monitors the screens.

**What is hotel TV / hospitality IPTV?**
A TV system for hotel rooms that goes beyond live channels: a welcome screen with the guest's name, an interactive menu of hotel services, messages, live TV with EPG, and apps such as Netflix, YouTube and Chromecast. Avemeo delivers this on LG, Samsung and Vestel hospitality displays and on ARRIS IPTV set-top boxes connected to any TV.

**What is the difference between Avemeo and Business Stream?**
Business Stream is a digital signage and hotel TV service of Slovak Telekom. It runs on the Avemeo platform in its own cloud (`cloud.tvstream.sk`). The Avemeo cloud (`ds.avemeo.com`) is operated by Avemeo s.r.o. The REST API and the AI connector work the same way on both; only the URLs differ.

**Which devices are supported?**
LG commercial displays (webOS), Samsung and Vestel commercial displays, Android players and TVs, Raspberry Pi, and ARRIS VIP4302 IPTV set-top boxes.

**Which languages does Avemeo support?**
On-screen content can be multilingual with a language switch (for example Slovak and English on a hotel menu). The AI connector understands prompts in Slovak, Czech and English.

**Who sells and supports Avemeo in Slovakia?**
SORTEC EUROPE s.r.o. – distributor and business & development partner of Avemeo, and partner for Business Stream by Slovak Telekom. Contact: [avemeo@sortec.sk](mailto:avemeo@sortec.sk).

## REST API

**Does Avemeo have an API?**
Yes. Avemeo has a REST API – the same one the CMS uses – covering media, screens, playlists, schedulers, devices, remote control and statistics. The technical documentation is provided to customers and integrators after sign-in and on request; it is not public. See the [API overview](api-overview.md).

**Why is the technical API documentation not public?**
The current API was designed for the Avemeo CMS, not as a public interface. Avemeo provides its documentation to customers and integrators individually, and a new API v2 with its own documentation is in preparation.

**Can I get a test account?**
Write to [avemeo@sortec.sk](mailto:avemeo@sortec.sk); access for integrators and pilot customers is arranged individually.

**What can I build with it?**
Integrations with hotel systems (PMS), ERP and marketing tools; automated content updates; monitoring and reporting; custom dashboards. See [use cases](use-cases.md).

**Where do I get the technical documentation?**
Write to [avemeo@sortec.sk](mailto:avemeo@sortec.sk) with your company, your cloud and what you want to integrate.

## AI connector (MCP)

**What is the Avemeo AI connector?**
A remote Model Context Protocol (MCP) server that lets AI assistants – Claude, ChatGPT, Gemini, Cursor, VS Code and others – read and change an Avemeo account on behalf of a signed-in user, with approval before every change. See the [connector page](mcp-connector.md).

**What is MCP?**
The Model Context Protocol is an open standard for connecting AI assistants to external tools and data. A remote MCP server is hosted on the internet and reached over HTTPS with OAuth sign-in.

**Is the connector available now?**
It is in development; a pilot with selected customers is being prepared. Contact [avemeo@sortec.sk](mailto:avemeo@sortec.sk) to take part.

**Which AI assistants work with it?**
Any assistant that supports remote MCP servers with OAuth: Claude (web, desktop, mobile), ChatGPT (custom connectors), Gemini CLI, Cursor, VS Code and others.

**Do I need my own AI subscription?**
Yes. The connector plugs into the assistant you already use. For customers without their own AI tool, an AI assistant built into the Avemeo CMS is in development.

**What can the assistant do?**
Find and read screens, playlists, schedulers, media and devices; prepare and – after your approval – apply changes to playlists, schedulers and screens; create screens from templates; send device commands (on, off, reload, reboot); produce proof-of-play and outage reports.

**What can it not do?**
Delete content. Act without your approval. Access accounts or areas you did not grant at sign-in.

**Can it run reports automatically?**
Assistants with scheduled tasks (for example Claude) can run a prompt on a schedule, such as a morning list of devices that were offline yesterday.

## Security and data

**How does sign-in work?**
Through OAuth on the Avemeo sign-in page. The assistant receives a scoped token; it never sees your password. You can revoke the token in Avemeo at any time.

**Is every change approved?**
Yes. The connector prepares a plan with a before/after summary; the change is applied only after you approve it. Every call is written to the audit log with the user and the AI client.

**Is my data used to train AI models?**
Data flows to the AI assistant you chose, under your AI provider's terms and plan. Business and enterprise plans of the major providers typically exclude training on customer data. Avemeo receives only the tool calls the assistant makes.

**What about prompt injection?**
Content stored in Avemeo (screen names, texts, media titles) is treated as data, not as instructions to the assistant.

**How do I report a security issue?**
See [SECURITY.md](../SECURITY.md).

## Pilot, pricing and contact

**How do I join the pilot?**
Send a short note with your industry, the number of devices and the AI assistant you use to [avemeo@sortec.sk](mailto:avemeo@sortec.sk).

**What does the connector cost?**
Pricing and availability will be announced with the launch; pilot participants are informed individually.

**Where can I see Avemeo?**
[avemeo.sk](https://avemeo.sk), or ask for a demo at [avemeo@sortec.sk](mailto:avemeo@sortec.sk).

**How do I report an error in this documentation?**
[Open an issue](https://github.com/sortec-europe/avemeo-api/issues/new/choose) or send a pull request – see [CONTRIBUTING.md](../CONTRIBUTING.md).
