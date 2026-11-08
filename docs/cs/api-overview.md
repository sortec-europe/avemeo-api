# Avemeo REST API

> 🇬🇧 English version: [../api-overview.md](../api-overview.md) · 🇸🇰 Slovenská verzia: [../sk/api-overview.md](../sk/api-overview.md) · ⬅ Zpět na [README](../../README.cs.md)

Avemeo, cloudová platforma pro digital signage, hotelovou TV a audio v prodejnách, má **REST API** – stejné rozhraní, které používá webová aplikace Avemeo CMS. Pokrývá média, obrazovky, playlisty, plánovače, zařízení, dálkové ovládání a statistiky a je základem [AI konektoru Avemeo (MCP)](mcp-connector.md).

## Kdo ho může používat

API je dostupné **zákazníkům Avemeo a jejich integrátorům**. Technická dokumentace (specifikace OpenAPI 3, autentizace, endpointy, příklady) se poskytuje **po přihlášení na vašem cloudu Avemeo** a na vyžádání – zde není zveřejněna, protože současné API bylo navrženo pro CMS, ne jako veřejné rozhraní.

Pokud chcete přístup nebo máte technický dotaz, napište na [avemeo@sortec.sk](mailto:avemeo@sortec.sk) s názvem firmy, vaším cloudem (Avemeo nebo Business Stream) a tím, co chcete integrovat.

## Co se integruje

| Integrace | Typický cíl |
|---|---|
| **Hotelový systém (PMS) → hotelová TV** | jméno hosta a pokoj na TV, check-in/check-out, zprávy |
| **ERP nebo ceník → digitální menu** | automatické aktualizace cen a menu |
| **Monitoring → ticketing** | tiket, když je přehrávač příliš dlouho offline |
| **Marketingový nástroj → kampaně** | playlisty a rozvrhy vytvořené pro kampaň |
| **Reporting** | proof of play a reporty výpadků napříč provozovnami |

Další scénáře: [příklady použití](use-cases.md).

## API v2

Tým Avemeo připravuje **novou verzi API (v2)** s vlastní dokumentací. Integrace postavené na současném API bude po vydání v2 potřeba zmigrovat. Pokud integraci plánujete nyní, nejdřív se nám ozvěte, abychom poradili s načasováním.

## Bez programování? Použijte AI konektor

Zákazníkům, kteří nechtějí psát kód, umožní [AI konektor (MCP)](mcp-connector.md), aby s jejich účtem Avemeo pracoval AI asistent – Claude, ChatGPT, Gemini a další – s jejich oprávněními a se schválením před každou změnou.

## Související

- [AI konektor (MCP)](mcp-connector.md) · [Příklady použití](use-cases.md) · [FAQ](faq.md) · [Slovník pojmů](glossary.md)
- [README](../../README.cs.md) – přehled platformy a kontakt
