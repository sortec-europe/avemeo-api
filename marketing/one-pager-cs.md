# Avemeo – obrazovky, hotelová TV a audio v prodejnách, ovládané i přes AI

> 🇬🇧 English version: [one-pager-en.md](one-pager-en.md) · 🇸🇰 Slovenská verzia: [one-pager-sk.md](one-pager-sk.md) · Dokumentace: [github.com/sortec-europe/avemeo-api](https://github.com/sortec-europe/avemeo-api)

**Avemeo** je cloudová platforma, která z jednoho místa řídí obrazovky v prodejnách, hotelovou TV, interaktivní menu i hudbu a spoty v obchodech. Připravujeme také připojení z AI asistenta, kterého už používáte – Claude, ChatGPT, Gemini a dalších.

## Základní fakta

| | |
|---|---|
| **Co** | cloudový CMS pro digital signage, hotelovou TV (hotelová IPTV) a audio/video v prodejnách |
| **Kde** | cloud Avemeo (`ds.avemeo.com`) a Business Stream od Slovak Telekomu (`cloud.tvstream.sk`) |
| **Zařízení** | displeje LG (webOS), Samsung a Vestel · Android · Raspberry Pi · IPTV set-top boxy ARRIS |
| **Integrace** | REST API pro zákazníky a integrátory (dokumentace na vyžádání, připravuje se v2) · AI konektor (MCP) pro Claude, ChatGPT, Gemini – ve vývoji |
| **Partner** | SORTEC EUROPE s.r.o. – prodej, nasazení, podpora, pilotní program · [avemeo@sortec.sk](mailto:avemeo@sortec.sk) |

## Pro koho

- **Retailové sítě** – hudba, spoty a video kampaně v desítkách prodejen, s důkazem o přehrání po každém zařízení.
- **Hotely** – TV se živými kanály, jménem hosta, interaktivním menu služeb, Netflixem, YouTube a Chromecastem.
- **Firmy a instituce** – recepce, lobby, kongresové navigace, digitální menu, vyvolávací systémy.

## Co Avemeo umí

| | |
|---|---|
| **Obsah** | vizuální editor obrazovek, šablony, playlisty, časovače podle dnů, hodin a svátků |
| **Interaktivita** | víceúrovňové menu na dálkový ovladač nebo dotyk, více jazyků s přepínačem |
| **Hotelová TV** | živé TV kanály s EPG, napojení na hotelový systém (PMS): host, pokoj, check-in, check-out |
| **Zařízení** | LG, Samsung, Vestel, Android, Raspberry Pi, IPTV boxy ARRIS |
| **Provoz** | vzdálené zapnutí, restart, hlasitost, screenshoty, upozornění na výpadky e-mailem a SMS |
| **Statistiky** | stav zařízení po minutách, co a kdy se přehrálo, export do CSV |

## Připravujeme: Avemeo v AI asistentovi

Konektor Avemeo připojí váš účet do Claude, ChatGPT, Gemini a dalších AI nástrojů přes otevřený standard Model Context Protocol (MCP). Místo klikání stačí napsat:

- *„Dej od pátku do playlistu recepce novou nabídku, 10 sekund na snímek.“*
- *„Které přehrávače byly včera během otevírací doby offline?“*
- *„Udělej anglickou verzi hotelového menu.“*

AI pracuje jen s vaším účtem a s oprávněními, která mu při přihlášení povolíte. Každou změnu nejdřív ukáže ke schválení a dá se vrátit. Mazat přes AI nelze.

Pro zákazníky bez vlastní AI připravuje tým Avemeo také AI asistenta přímo v CMS.

Konektor (adresa `https://mcp.avemeo.com/mcp`, pro Business Stream `https://mcp.tvstream.sk/mcp`) i asistent v CMS jsou ve vývoji, pilot s vybranými zákazníky připravujeme. Zájem o pilot: [avemeo@sortec.sk](mailto:avemeo@sortec.sk).

## Proč Avemeo

- **Jedna platforma** pro signage, hotelovou TV i audio v prodejnách.
- **Partner, který mluví vaším jazykem** – podpora a nasazení v češtině a slovenštině. Dostupné také jako služba [Business Stream](https://www.telekom.sk/biznis/stredne-velke-firmy/business-stream) od Slovak Telekomu.
- **REST API** pro integrace s hotelovými, ERP a marketingovými systémy.
- **AI bez vlastního vývoje** – použijete AI, kterou vaši lidé už mají.

**Kontakt:** SORTEC EUROPE s.r.o. – distributor a obchodně-vývojový partner Avemeo, partner pro [Business Stream](https://www.telekom.sk/biznis/stredne-velke-firmy/business-stream) ve Slovak Telekomu. [avemeo@sortec.sk](mailto:avemeo@sortec.sk) · [avemeo.sk](https://avemeo.sk)
