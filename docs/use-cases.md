# Use cases: Avemeo with an AI assistant

> 🇸🇰 Slovenská verzia: [sk/use-cases.md](sk/use-cases.md) · 🇨🇿 Česká verze: [cs/use-cases.md](cs/use-cases.md) · ⬅ Back to [README](../README.md)

What customers will be able to do with Avemeo and an AI assistant (Claude, ChatGPT, Gemini and other MCP clients) once the [AI connector](mcp-connector.md) is available. Each example shows what you say, what the assistant does in Avemeo and what you approve. The same operations are available to developers through the [REST API](api-overview.md).

**Contents:** [Retail](#retail-stores-and-chains) · [Hotels](#hotels-and-hospitality) · [Offices, venues and events](#offices-venues-and-events) · [Operations and monitoring](#operations-and-monitoring) · [Content production](#content-production) · [Developers](#developers-and-integrators)

## Retail: stores and chains

### Proof of play and offline players

> *"Which store players were offline last week during opening hours? Sort by hours lost."*

The assistant reads per-minute device states for every player, compares them with each store's opening hours and returns a table by store with hours lost and outage times. Typical result: most players play 98–100 % of the time; a few stores show repeated outages that point to the local network rather than the player.

> *"Reboot the audio player in the Main Street store and tell me when it is playing again."*

**You approve:** the reboot of one named device.

### Campaigns across many stores

> *"From Monday, add the new autumn spot to all store audio playlists, every 15 minutes, until the end of November."*

The assistant finds the store playlists, prepares one change with a before/after preview for every playlist and applies it after a single approval.

> *"Replace the summer price list on all menu boards with the new one from the media library."*

**You approve:** the list of playlists or screens that will change.

### Regional and seasonal content

> *"Play the Christmas playlist in all stores from 1 December, but in the Bratislava stores start a week earlier."*

The assistant creates or adjusts schedulers with date ranges per store group.

## Hotels and hospitality

### Interactive hotel TV menu

> *"Create a hotel TV menu from the round template with TV, radio, restaurant, wellness, trips and weather, in Slovak and English."*

The assistant creates the screen from an Avemeo template, fills in texts, images and translations and shows a preview of each menu level.

> *"Change the breakfast time in the menu to 7:00–10:30."*

> *"Add a German version of the menu and a language switch."*

**You approve:** the new or changed screen after reviewing the preview.

### Guest communication

> *"Show me what is playing right now in room 204."*

> *"Put a welcome message for the conference group on all rooms on floor 3 from Friday to Sunday."*

### Events and conferences

> *"For tomorrow's conference, put the programme on the lobby screens from 7:30 and the room names on the door screens."*

## Offices, venues and events

### Reception and lobby screens

> *"Make a reception playlist with the five presentation screens, 8 seconds each, and play it on weekdays 8:00–17:00."*

> *"What is on the lobby screen right now?"*

### Wayfinding and queue systems

> *"Rename the meeting room 'Tatry' to 'Fatra' on all wayfinding screens."*

### Canteens and menu boards

> *"Upload this week's canteen menu to the cafeteria screens and switch to the weekend menu on Saturday."*

## Operations and monitoring

### Daily report

> *"Send me every morning a list of devices that were offline yesterday."* (with scheduled tasks in the AI assistant)

### Power management

> *"Switch off all screens in the Žilina branch tonight at 20:00 and on again at 7:00 on weekdays."*

The assistant edits the scheduler with power control per time slot.

### Fleet overview

> *"Which devices have not reported for more than 24 hours? Group them by location."*

> *"Which players are still on the old firmware?"*

### Undo

> *"Undo the last change to the restaurant playlist."* (planned: change history and restore)

## Content production

> *"Create a screen with today's date, the clock and the weather for Poprad, dark background, our logo top left."*

> *"Translate all texts of the 'Wellness' screen into English and keep the layout."*

> *"Duplicate the 'Summer offer' screen as 'Autumn offer' and swap the background image for `autumn.jpg`."*

**You approve:** every new or changed screen after a preview.

## Developers and integrators

Everything above runs on the Avemeo REST API, which you can also call directly:

| Integration | How |
|---|---|
| **Hotel PMS → TV** | Avemeo's hotel TV integrates with hotel systems for check-in and check-out (guest name, room, messages); ask us about the integration options for your PMS. |
| **ERP → price lists** | Nightly job that updates price texts on menu-board screens. |
| **Monitoring → ticketing** | Poll device states and open a ticket when a device is offline for more than N minutes. |
| **Marketing → campaigns** | Create playlists and schedulers for a campaign from your campaign tool. |

The technical documentation of the API is provided to customers and integrators on request – see the [REST API overview](api-overview.md).

## Related

- [AI connector (MCP)](mcp-connector.md) · [REST API overview](api-overview.md) · [FAQ](faq.md) · [Glossary](glossary.md)
- Interested in the pilot? [avemeo@sortec.sk](mailto:avemeo@sortec.sk)
