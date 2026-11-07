# Často kladené otázky – Avemeo, REST API a AI konektor

> 🇬🇧 English version: [../faq.md](../faq.md) · 🇸🇰 Slovenská verzia: [../sk/faq.md](../sk/faq.md) · ⬅ Zpět na [README](../../README.cs.md)

**Obsah:** [O Avemeo](#o-avemeo) · [REST API](#rest-api) · [AI konektor (MCP)](#ai-konektor-mcp) · [Bezpečnost a data](#bezpečnost-a-data) · [Pilot, cena a kontakt](#pilot-cena-a-kontakt)

## O Avemeo

**Co je Avemeo?**
Avemeo je cloudová platforma (CMS) pro digital signage, hotelovou TV a audio a video v prodejnách od společnosti Avemeo s.r.o. Z jedné webové aplikace řídí, co se přehrává na obrazovkách, hotelových televizorech a audio přehrávačích: obsah, playlisty, rozvrhy, zařízení a statistiky.

**Co je digital signage?**
Digital signage (digitální obrazovky, digitální vývěsky) znamená centrálně řízené zobrazování obsahu – akcí, menu, informací, navigace, živé TV – na obrazovkách ve veřejných a komerčních prostorech. Avemeo je software (CMS), který tento obsah tvoří, plánuje, distribuuje a obrazovky monitoruje.

**Co je hotelová TV / hotelová IPTV?**
TV systém pro hotelové pokoje, který jde nad rámec živých kanálů: uvítací obrazovka se jménem hosta, interaktivní menu hotelových služeb, zprávy, živá TV s EPG a aplikace jako Netflix, YouTube a Chromecast. Avemeo to dodává na hotelových displejích LG, Samsung a Vestel a na IPTV set-top boxech ARRIS připojených k libovolnému televizoru.

**Jaký je rozdíl mezi Avemeo a Business Stream?**
Business Stream je služba Slovak Telekomu pro digital signage a hotelovou TV. Běží na platformě Avemeo ve vlastním cloudu (`cloud.tvstream.sk`). Cloud Avemeo (`ds.avemeo.com`) provozuje Avemeo s.r.o. REST API i AI konektor fungují na obou stejně; liší se jen adresy.

**Která zařízení jsou podporována?**
Komerční displeje LG (webOS), komerční displeje Samsung a Vestel, přehrávače a TV s Androidem, Raspberry Pi a IPTV set-top boxy ARRIS VIP4302.

**Jaké jazyky Avemeo podporuje?**
Obsah na obrazovkách může být vícejazyčný s přepínačem jazyka (například čeština a angličtina v hotelovém menu). AI konektor rozumí pokynům česky, slovensky a anglicky.

**Kdo prodává a podporuje Avemeo?**
SORTEC EUROPE s.r.o. – distributor a obchodně-vývojový partner Avemeo na Slovensku a partner pro Business Stream od Slovak Telekomu. Kontakt: [avemeo@sortec.sk](mailto:avemeo@sortec.sk).

## REST API

**Má Avemeo API?**
Ano. Každý cloud Avemeo zveřejňuje specifikaci OpenAPI 3 na adrese `https://<váš-cloud>/backend/openapi/` s více než 380 operacemi. Je to stejné API, které používá CMS. Viz [přehled API](api-overview.md).

**Jak se autentizuji?**
Přihlaste se přes `POST /api/auth/login`, získáte JWT, a pak s každým požadavkem posílejte `Authorization: Bearer <token>` a `Active-Profile-Id: <id účtu>`. Dálkové ovládání zařízení používá místo toho hlavičku `api-key`.

**Dostanu testovací účet?**
Napište na [avemeo@sortec.sk](mailto:avemeo@sortec.sk); přístup pro integrátory a pilotní zákazníky se řeší individuálně.

**Co s tím mohu postavit?**
Integrace s hotelovými systémy (PMS), ERP a marketingovými nástroji; automatické aktualizace obsahu; monitoring a reporting; vlastní dashboardy. Viz [příklady použití](use-cases.md).

**Kde je úplný seznam endpointů?**
Ve Swagger UI na vašem cloudu (`/backend/openapi/`). [Přehled API](api-overview.md) vysvětluje hlavní oblasti, konvence a příklady.

## AI konektor (MCP)

**Co je AI konektor Avemeo?**
Vzdálený server Model Context Protocol (MCP), přes který AI asistenti – Claude, ChatGPT, Gemini, Cursor, VS Code a další – čtou a mění účet Avemeo jménem přihlášeného uživatele, se schválením před každou změnou. Viz [stránku konektoru](mcp-connector.md).

**Co je MCP?**
Model Context Protocol je otevřený standard pro připojování AI asistentů k externím nástrojům a datům. Vzdálený MCP server běží na internetu a asistent ho používá přes HTTPS s přihlášením přes OAuth.

**Je konektor už dostupný?**
Je ve vývoji; připravuje se pilot s vybranými zákazníky. Pokud se chcete zapojit, napište na [avemeo@sortec.sk](mailto:avemeo@sortec.sk).

**Se kterými AI asistenty funguje?**
S každým asistentem, který podporuje vzdálené MCP servery s OAuth: Claude (web, desktop, mobil), ChatGPT (vlastní konektory), Gemini CLI, Cursor, VS Code a další.

**Potřebuji vlastní předplatné AI?**
Ano. Konektor se připojuje k asistentovi, který už používáte. Pro zákazníky bez vlastního AI nástroje je ve vývoji AI asistent zabudovaný v Avemeo CMS.

**Co asistent dokáže?**
Najít a přečíst obrazovky, playlisty, plánovače, média a zařízení; připravit a – po vašem schválení – provést změny playlistů, plánovačů a obrazovek; vytvářet obrazovky ze šablon; posílat příkazy zařízením (zapnout, vypnout, obnovit, restartovat); dělat reporty přehrávání a výpadků.

**Co nedokáže?**
Mazat obsah. Jednat bez vašeho schválení. Přistupovat k účtům nebo oblastem, které jste při přihlášení nepovolili.

**Umí spouštět reporty automaticky?**
Asistenti s naplánovanými úlohami (například Claude) umí spouštět pokyn podle rozvrhu, například ranní seznam zařízení, která byla včera offline.

## Bezpečnost a data

**Jak funguje přihlášení?**
Přes OAuth na přihlašovací stránce Avemeo. Asistent dostane omezený token; vaše heslo nikdy nevidí. Token můžete v Avemeo kdykoli odvolat.

**Schvaluje se každá změna?**
Ano. Konektor připraví plán se shrnutím před/po; změna se provede až po vašem schválení. Každé volání se zapisuje do auditu s uživatelem a AI klientem.

**Používají se má data k trénování AI modelů?**
Data jdou k AI asistentovi, kterého jste si zvolili, podle podmínek a plánu vašeho poskytovatele AI. Firemní a podnikové plány hlavních poskytovatelů zpravidla trénování na zákaznických datech vylučují. Avemeo dostává jen volání nástrojů, která asistent dělá.

**Co s prompt injection?**
Obsah uložený v Avemeo (názvy obrazovek, texty, názvy médií) se bere jako data, ne jako pokyny pro asistenta.

**Jak nahlásím bezpečnostní problém?**
Viz [SECURITY.md](../../SECURITY.md).

## Pilot, cena a kontakt

**Jak se zapojím do pilotu?**
Pošlete krátkou zprávu s odvětvím, počtem zařízení a AI asistentem, který používáte, na [avemeo@sortec.sk](mailto:avemeo@sortec.sk).

**Kolik konektor stojí?**
Cena a dostupnost budou oznámeny při spuštění; účastníci pilotu dostanou informace individuálně.

**Kde si mohu Avemeo prohlédnout?**
[avemeo.sk](https://avemeo.sk), nebo si vyžádejte ukázku na [avemeo@sortec.sk](mailto:avemeo@sortec.sk).

**Jak nahlásím chybu v této dokumentaci?**
[Založte issue](https://github.com/sortec-europe/avemeo-api/issues/new/choose) nebo pošlete pull request – viz [CONTRIBUTING.md](../../CONTRIBUTING.md).
