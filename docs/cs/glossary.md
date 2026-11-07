# Slovník pojmů – digital signage, hotelová TV, Avemeo a MCP

> 🇬🇧 English version: [../glossary.md](../glossary.md) · 🇸🇰 Slovenská verzia: [../sk/glossary.md](../sk/glossary.md) · ⬅ Zpět na [README](../../README.cs.md)

Krátké definice pojmů, které se používají v této dokumentaci, v Avemeo CMS a v AI konektoru. Abecedně.

**AI asistent (MCP klient)** – AI aplikace, která umí používat MCP servery: Claude, ChatGPT, Gemini CLI, Cursor, VS Code a další.

**Audit** – záznam každé akce včetně akcí přes AI konektor, s uživatelem, klientem a časem.

**Avemeo** – cloudová platforma (CMS) pro digital signage, hotelovou TV a audio a video v prodejnách od společnosti Avemeo s.r.o. Provozovaná v cloudu Avemeo (`ds.avemeo.com`) a jako Business Stream ve Slovak Telekomu (`cloud.tvstream.sk`).

**Business Stream** – služba Slovak Telekomu pro digital signage a hotelovou TV, která běží na platformě Avemeo.

**CMS (systém pro správu obsahu)** – webová aplikace, ve které se obsah tvoří, plánuje a přiřazuje zařízením. V Avemeo sdílejí CMS a REST API stejný backend.

**Dálkové ovládání (remote control API)** – endpointy API (ověřované API klíčem) pro napájení, hlasitost, TV kanál a stisky kláves na zařízení.

**Digital signage** – centrálně řízený obsah na obrazovkách ve veřejných a komerčních prostorech: akce, menu, informace, navigace, živá TV. Česky také „digitální obrazovky“ nebo „digitální vývěsky“.

**EPG (elektronický programový průvodce)** – přehled TV programu v přehrávači hotelové TV.

**HLS (HTTP Live Streaming)** – formát streamování, který Avemeo používá pro živé TV kanály.

**Hotelová TV / hotelová IPTV** – TV pro hotelové pokoje se živými kanály, uvítací obrazovkou se jménem hosta, interaktivním menu služeb, zprávami a aplikacemi (Netflix, YouTube, Chromecast). IPTV přenáší kanály přes IP síť hotelu.

**Interaktivní menu** – obrazovka s více úrovněmi, ve které se host nebo návštěvník pohybuje dálkovým ovladačem nebo dotykem, často ve více jazycích.

**MCP (Model Context Protocol)** – otevřený standard pro připojování AI asistentů k externím nástrojům a datům. *Vzdálený MCP server* běží na internetu a asistent ho používá přes HTTPS s přihlášením přes OAuth. AI konektor Avemeo je vzdálený MCP server.

**Naplánovaná úloha** – funkce některých AI asistentů (například Claude), která spouští pokyn podle rozvrhu, například denní report výpadků přes konektor.

**OAuth** – standard přihlášení, který používá AI konektor. Uživatel se přihlásí na stránce Avemeo; asistent dostane omezený, odvolatelný token a heslo nikdy nevidí.

**Obrazovka** – rozložení (standardně 1920 × 1080) složené z widgetů; základní jednotka obsahu v Avemeo. Obrazovka může mít více úrovní a překladů.

**Obsah zařízení** – přiřazení toho, co zařízení přehrává: obrazovka s úrovní nebo plánovač.

**OpenAPI** – standardní strojově čitelný popis REST API. Avemeo zveřejňuje specifikaci OpenAPI 3 na každém cloudu na adrese `/backend/openapi/`.

**Plán (dvoukrokový zápis)** – v AI konektoru se každá změna nejdřív připraví jako plán se shrnutím před/po a provede se až po schválení uživatelem.

**Plánovač** – určuje, co kdy hraje: časové sloty s dny v týdnu, časy, obdobími a svátky, volitelně se zapnutím a vypnutím v každém slotu. Zařízení lze místo jedné obrazovky přiřadit plánovač.

**Playlist** – uspořádaná sekvence položek (obrazovky, média, živé kanály) s trváním v sekundách pro každou položku, přehrávaná dokola. Položky mohou mít data a časy platnosti.

**PMS (property management system)** – recepční systém hotelu. Hotelová TV Avemeo se integruje s hotelovými systémy při check-inu a check-outu.

**Prezentační widget** – celoobrazovkový widget, který na obrazovce přehrává playlist.

**Proof of play** – statistiky dokazující, co se kde a kdy přehrálo: stav zařízení po minutách a obrazovky a média přehrané v každý den. Používá se pro reklamní reporty a analýzu výpadků.

**Šablona** – hotová obrazovka nebo menu v Avemeo, které se zduplikuje a naplní texty, obrázky a jazyky zákazníka.

**Účet (profil)** – prostor zákazníka v Avemeo s vlastními médii, obrazovkami, playlisty, plánovači, zařízeními a uživateli. Jeden uživatel může mít přístup do více účtů; požadavky API vybírají účet hlavičkou `Active-Profile-Id`.

**Úroveň** – jeden stav interaktivní obrazovky (například hlavní menu, stránka restaurace, výběr jazyka). Widgety jsou viditelné nebo aktivní na konkrétních úrovních; tlačítka přepínají mezi úrovněmi.

**Widget** – stavební prvek obrazovky: textový blok, obrázek, video, hodiny, datum, počasí, svátky, RSS, TV přehrávač, prezentace (přehrávač playlistu), aplikace a další. Každý widget má polohu, velikost, pořadí (nižší číslo = vpředu) a parametry.

**Zařízení (přehrávač)** – hardware, který přehrává obsah: displej LG, Samsung nebo Vestel se zabudovaným přehrávačem, přehrávač nebo TV s Androidem, Raspberry Pi nebo IPTV set-top box ARRIS. Každému zařízení je přiřazena obrazovka (a úroveň) nebo plánovač.
