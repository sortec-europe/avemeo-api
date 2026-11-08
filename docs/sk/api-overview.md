# Avemeo REST API

> 🇬🇧 English version: [../api-overview.md](../api-overview.md) · 🇨🇿 Česká verze: [../cs/api-overview.md](../cs/api-overview.md) · ⬅ Späť na [README](../../README.sk.md)

Avemeo, cloudová platforma pre digital signage, hotelovú TV a audio v predajniach, má **REST API** – to isté rozhranie, ktoré používa webová aplikácia Avemeo CMS. Pokrýva médiá, obrazovky, playlisty, plánovače, zariadenia, diaľkové ovládanie a štatistiky a je základom [AI konektora Avemeo (MCP)](mcp-connector.md).

## Kto ho môže používať

API je dostupné **zákazníkom Avemeo a ich integrátorom**. Technická dokumentácia (špecifikácia OpenAPI 3, autentifikácia, endpointy, príklady) sa poskytuje **po prihlásení na vašom cloude Avemeo** a na požiadanie – tu nie je zverejnená, pretože súčasné API bolo navrhnuté pre CMS, nie ako verejné rozhranie.

Ak chcete prístup alebo máte technickú otázku, napíšte na [avemeo@sortec.sk](mailto:avemeo@sortec.sk) s názvom firmy, vaším cloudom (Avemeo alebo Business Stream) a tým, čo chcete integrovať.

## Čo sa integruje

| Integrácia | Typický cieľ |
|---|---|
| **Hotelový systém (PMS) → hotelová TV** | meno hosťa a izba na TV, check-in/check-out, správy |
| **ERP alebo cenník → digitálne menu** | automatické aktualizácie cien a menu |
| **Monitoring → ticketing** | tiket, keď je prehrávač príliš dlho offline |
| **Marketingový nástroj → kampane** | playlisty a rozvrhy vytvorené pre kampaň |
| **Reporting** | proof of play a reporty výpadkov naprieč prevádzkami |

Ďalšie scenáre: [príklady použitia](use-cases.md).

## API v2

Tím Avemeo pripravuje **novú verziu API (v2)** s vlastnou dokumentáciou. Integrácie postavené na súčasnom API bude po vydaní v2 potrebné zmigrovať. Ak integráciu plánujete teraz, najprv sa nám ozvite, aby sme poradili s načasovaním.

## Bez programovania? Použite AI konektor

Zákazníkom, ktorí nechcú písať kód, umožní [AI konektor (MCP)](mcp-connector.md), aby s ich kontom Avemeo pracoval AI asistent – Claude, ChatGPT, Gemini a ďalší – s ich oprávneniami a so schválením pred každou zmenou.

## Súvisiace

- [AI konektor (MCP)](mcp-connector.md) · [Príklady použitia](use-cases.md) · [FAQ](faq.md) · [Slovník pojmov](glossary.md)
- [README](../../README.sk.md) – prehľad platformy a kontakt
