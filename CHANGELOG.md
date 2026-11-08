# Changelog

Notable changes to this documentation repository. Dates are in ISO format (YYYY-MM-DD).

## 2026-11-08

### Removed

- Technical details of the current Avemeo REST API (endpoints, headers, response formats, code examples) from all languages, at the request of the Avemeo team: the API documentation is provided to customers and integrators individually and a new API v2 with its own documentation is in preparation. The API pages now describe who can use the API, typical integrations and the v2 plan.

## 2026-11-07 (2)

### Added

- Czech version of the repository: `README.cs.md`, `docs/cs/` (API overview, AI connector, use cases, FAQ, glossary, index) and `marketing/one-pager-cs.md`; language switches and `llms.txt` updated.

## 2026-11-07

### Added

- Repository banner (`assets/banner.svg`), table of contents, "at a glance" table, "who this is for", architecture diagram, comparison table, supported players, status and roadmap, and an FAQ section in `README.md` and `README.sk.md`.
- `docs/faq.md` and `docs/glossary.md` (English) with full Slovak versions in `docs/sk/`.
- Slovak translations of the API overview, AI connector and use cases (`docs/sk/`), plus documentation indexes (`docs/README.md`, `docs/sk/README.md`).
- `llms.txt` – machine-readable summary of the repository for AI tools and search engines.
- `SECURITY.md`, `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, issue templates and a pull request template.
- English press release template (`marketing/press-release-en.md`) and `marketing/README.md`.

### Changed

- `docs/api-overview.md`: added where to find the specification per cloud, response format, device-content endpoints, more examples, conventions, FAQ and related links.
- `docs/mcp-connector.md`: added an explanation of MCP, a sequence diagram of the approval flow, grouped planned capabilities, an example conversation, FAQ and related links.
- `docs/use-cases.md`: grouped by industry with more scenarios and a section for developers and integrators.
- Marketing one-pagers: added a key-facts table and cross-links; press release template extended with boilerplate sections.
- Repository description, website and topics on GitHub.

### Fixed

- Sign-in example: the login response field is `accessToken` (previously documented as `accessKey`).

## 2026-11-03 – 2026-11-04

### Added

- Initial public version: `README.md`, `README.sk.md`, `docs/api-overview.md`, `docs/mcp-connector.md`, `docs/use-cases.md`, marketing one-pagers and the Slovak press release template, `LICENSE` (CC BY 4.0).
