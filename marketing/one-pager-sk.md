# Avemeo – obrazovky, hotelová TV a audio v predajniach, ovládané aj cez AI

> 🇬🇧 English version: [one-pager-en.md](one-pager-en.md) · 🇨🇿 Česká verze: [one-pager-cs.md](one-pager-cs.md) · Dokumentácia: [github.com/sortec-europe/avemeo-api](https://github.com/sortec-europe/avemeo-api)

**Avemeo** je cloudová platforma, ktorá z jedného miesta riadi obrazovky v predajniach, hotelovú TV, interaktívne menu aj hudbu a spoty v obchodoch. Pripravujeme aj pripojenie z AI asistenta, ktorého už používate – Claude, ChatGPT, Gemini a ďalších.

## Základné fakty

| | |
|---|---|
| **Čo** | cloudový CMS pre digital signage, hotelovú TV (hotelová IPTV) a audio/video v predajniach |
| **Kde** | cloud Avemeo (`ds.avemeo.com`) a Business Stream od Slovak Telekomu (`cloud.tvstream.sk`) |
| **Zariadenia** | displeje LG (webOS), Samsung a Vestel · Android · Raspberry Pi · IPTV set-top boxy ARRIS |
| **Integrácia** | otvorené REST API (OpenAPI 3, viac ako 380 operácií) · AI konektor (MCP) pre Claude, ChatGPT, Gemini – vo vývoji |
| **Partner na Slovensku** | SORTEC EUROPE s.r.o. – predaj, nasadenie, podpora, pilotný program · [avemeo@sortec.sk](mailto:avemeo@sortec.sk) |

## Pre koho

- **Retailové siete** – hudba, spoty a video kampane v desiatkach predajní, s dôkazom o prehratí po každom zariadení.
- **Hotely** – TV so živými kanálmi, menom hosťa, interaktívnym menu služieb, Netflixom, YouTube a Chromecastom.
- **Firmy a inštitúcie** – recepcie, lobby, kongresové navigácie, digitálne menu, vyvolávacie systémy.

## Čo Avemeo vie

| | |
|---|---|
| **Obsah** | vizuálny editor obrazoviek, šablóny, playlisty, časovače podľa dní, hodín a sviatkov |
| **Interaktivita** | viacúrovňové menu na diaľkový ovládač alebo dotyk, viac jazykov s prepínačom |
| **Hotelová TV** | živé TV kanály s EPG, napojenie na hotelový systém (PMS): hosť, izba, check-in, check-out |
| **Zariadenia** | LG, Samsung, Vestel, Android, Raspberry Pi, IPTV boxy ARRIS |
| **Prevádzka** | vzdialené zapnutie, reštart, hlasitosť, screenshoty, upozornenia na výpadky e-mailom a SMS |
| **Štatistiky** | stav zariadení po minútach, čo a kedy sa prehralo, export do CSV |

## Pripravujeme: Avemeo v AI asistentovi

Konektor Avemeo pripojí vaše konto do Claude, ChatGPT, Gemini a ďalších AI nástrojov cez otvorený štandard Model Context Protocol (MCP). Namiesto klikania stačí napísať:

- *„Daj od piatku do playlistu recepcie novú ponuku, 10 sekúnd na snímku.“*
- *„Ktoré prehrávače boli včera počas otváracích hodín offline?“*
- *„Sprav anglickú verziu hotelového menu.“*

AI pracuje len s vaším kontom a s oprávneniami, ktoré mu pri prihlásení povolíte. Každú zmenu najprv ukáže na schválenie a dá sa vrátiť. Mazať cez AI nemožno.

Pre zákazníkov bez vlastnej AI pripravuje tím Avemeo aj AI asistenta priamo v CMS.

Konektor (adresa `https://mcp.avemeo.com/mcp`, pre Business Stream `https://mcp.tvstream.sk/mcp`) aj asistent v CMS sú vo vývoji, pilot s vybranými zákazníkmi pripravujeme. Záujem o pilot: [avemeo@sortec.sk](mailto:avemeo@sortec.sk).

## Prečo Avemeo

- **Jedna platforma** pre signage, hotelovú TV aj audio v predajniach.
- **Lokálny partner** – podpora a nasadenie na Slovensku, v slovenčine. Dostupné aj ako služba [Business Stream](https://www.telekom.sk/biznis/stredne-velke-firmy/business-stream) od Slovak Telekomu.
- **Otvorené API** so zdokumentovanou špecifikáciou OpenAPI.
- **AI bez vlastného vývoja** – použijete AI, ktorú vaši ľudia už majú.

**Kontakt:** SORTEC EUROPE s.r.o. – distribútor a obchodno-vývojový partner Avemeo, partner pre [Business Stream](https://www.telekom.sk/biznis/stredne-velke-firmy/business-stream) v Slovak Telekom. [avemeo@sortec.sk](mailto:avemeo@sortec.sk) · [avemeo.sk](https://avemeo.sk)
