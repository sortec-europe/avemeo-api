# Avemeo AI connector (MCP)

> **Status: in development.** The connector is being tested with selected pilot customers. This page describes the planned functionality and will be updated at launch. <!-- TODO: update status, date and URL at launch -->

The Avemeo connector is a remote [Model Context Protocol (MCP)](https://modelcontextprotocol.io) server. It lets an AI assistant work with an Avemeo account on behalf of a signed-in user. The customer uses their own AI assistant and subscription; Avemeo provides the connector.

## Supported AI assistants

Any assistant that supports remote MCP servers with OAuth, for example:

| Assistant | How to connect |
|---|---|
| Claude (web, desktop, mobile) | Customize → Connectors → Add custom connector → enter the connector URL → sign in. On Team and Enterprise plans, an organization owner adds the connector once and members sign in individually. |
| ChatGPT | Custom connector (developer mode), OAuth sign-in |
| Gemini CLI, Cursor, VS Code and others | Add a remote MCP server with the connector URL |

Connector URL: `https://<connector-url>` <!-- TODO -->

## Sign-in and permissions

- Sign-in uses **OAuth** on the Avemeo sign-in page. The AI assistant never sees your password.
- You choose the **account** and the **access level**, for example: read only, media, playlists and schedulers, screens, publishing, devices.
- **Deleting** content through AI is not available.
- You can revoke access at any time in Avemeo.

## Tools (planned)

| Tool | What it does |
|---|---|
| `list_folders`, `search` | Find screens, playlists, media, schedulers and devices by name |
| `list_media`, `upload_media` | Browse and upload media |
| `get_playlist`, `plan_playlist_change`, `apply_change` | Show a playlist, propose a change (before/after) and apply it after approval |
| `get_scheduler`, `plan_scheduler_change` | What plays when, with a preview of the change |
| `create_from_template` | New screen or menu from an Avemeo template, with your texts, images and languages |
| `preview_screen` | Image of a screen as it looks on the display |
| `list_devices`, `device_status`, `device_command` | Device status, what is playing now, reload and reboot |
| `playback_report` | Proof of play and offline time per device and day |
| `list_versions`, `restore_version` | Change history and undo |

## Security

- Every change is shown to the user for approval before it is saved (two-step write).
- Every call is recorded in the audit log with the user and the AI client.
- The connector only works with the account and permissions chosen at sign-in.
- Content from Avemeo (names, texts) is treated as data, not as instructions.

## Pilot program

Interested in testing the connector? Contact <!-- TODO: contact -->.
