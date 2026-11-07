# Často kladené otázky – Avemeo, REST API a AI konektor

> 🇬🇧 English version: [../faq.md](../faq.md) · ⬅ Späť na [README](../../README.sk.md)

**Obsah:** [O Avemeo](#o-avemeo) · [REST API](#rest-api) · [AI konektor (MCP)](#ai-konektor-mcp) · [Bezpečnosť a dáta](#bezpečnosť-a-dáta) · [Pilot, cena a kontakt](#pilot-cena-a-kontakt)

## O Avemeo

**Čo je Avemeo?**
Avemeo je cloudová platforma (CMS) pre digital signage, hotelovú TV a audio a video v predajniach od spoločnosti Avemeo s.r.o. Z jednej webovej aplikácie riadi, čo sa prehráva na obrazovkách, hotelových televízoroch a audio prehrávačoch: obsah, playlisty, rozvrhy, zariadenia a štatistiky.

**Čo je digital signage?**
Digital signage (digitálne obrazovky, digitálne vývesky) znamená centrálne riadené zobrazovanie obsahu – akcií, menu, informácií, navigácie, živej TV – na obrazovkách vo verejných a komerčných priestoroch. Avemeo je softvér (CMS), ktorý tento obsah tvorí, plánuje, distribuuje a obrazovky monitoruje.

**Čo je hotelová TV / hotelová IPTV?**
TV systém pre hotelové izby, ktorý ide nad rámec živých kanálov: uvítacia obrazovka s menom hosťa, interaktívne menu hotelových služieb, správy, živá TV s EPG a aplikácie ako Netflix, YouTube a Chromecast. Avemeo to dodáva na hotelových displejoch LG, Samsung a Vestel a na IPTV set-top boxoch ARRIS pripojených k ľubovoľnému televízoru.

**Aký je rozdiel medzi Avemeo a Business Stream?**
Business Stream je služba Slovak Telekomu pre digital signage a hotelovú TV. Beží na platforme Avemeo vo vlastnom cloude (`cloud.tvstream.sk`). Cloud Avemeo (`ds.avemeo.com`) prevádzkuje Avemeo s.r.o. REST API aj AI konektor fungujú na oboch rovnako; líšia sa len adresy.

**Ktoré zariadenia sú podporované?**
Komerčné displeje LG (webOS), komerčné displeje Samsung a Vestel, prehrávače a TV s Androidom, Raspberry Pi a IPTV set-top boxy ARRIS VIP4302.

**Aké jazyky Avemeo podporuje?**
Obsah na obrazovkách môže byť viacjazyčný s prepínačom jazyka (napríklad slovenčina a angličtina v hotelovom menu). AI konektor rozumie pokynom po slovensky, česky a anglicky.

**Kto predáva a podporuje Avemeo na Slovensku?**
SORTEC EUROPE s.r.o. – distribútor a obchodno-vývojový partner Avemeo a partner pre Business Stream od Slovak Telekomu. Kontakt: [avemeo@sortec.sk](mailto:avemeo@sortec.sk).

## REST API

**Má Avemeo API?**
Áno. Každý cloud Avemeo zverejňuje špecifikáciu OpenAPI 3 na adrese `https://<váš-cloud>/backend/openapi/` s viac ako 380 operáciami. Je to to isté API, ktoré používa CMS. Pozrite [prehľad API](api-overview.md).

**Ako sa autentifikujem?**
Prihláste sa cez `POST /api/auth/login`, získate JWT, a potom s každou požiadavkou posielajte `Authorization: Bearer <token>` a `Active-Profile-Id: <id konta>`. Diaľkové ovládanie zariadení používa namiesto toho hlavičku `api-key`.

**Dostanem testovacie konto?**
Napíšte na [avemeo@sortec.sk](mailto:avemeo@sortec.sk); prístup pre integrátorov a pilotných zákazníkov sa rieši individuálne.

**Čo s tým môžem postaviť?**
Integrácie s hotelovými systémami (PMS), ERP a marketingovými nástrojmi; automatické aktualizácie obsahu; monitoring a reporting; vlastné dashboardy. Pozrite [príklady použitia](use-cases.md).

**Kde je úplný zoznam endpointov?**
V Swagger UI na vašom cloude (`/backend/openapi/`). [Prehľad API](api-overview.md) vysvetľuje hlavné oblasti, konvencie a príklady.

## AI konektor (MCP)

**Čo je AI konektor Avemeo?**
Vzdialený server Model Context Protocol (MCP), cez ktorý AI asistenti – Claude, ChatGPT, Gemini, Cursor, VS Code a ďalší – čítajú a menia konto Avemeo v mene prihláseného používateľa, so schválením pred každou zmenou. Pozrite [stránku konektora](mcp-connector.md).

**Čo je MCP?**
Model Context Protocol je otvorený štandard na pripájanie AI asistentov k externým nástrojom a dátam. Vzdialený MCP server beží na internete a asistent ho používa cez HTTPS s prihlásením cez OAuth.

**Je konektor už dostupný?**
Je vo vývoji; pripravuje sa pilot s vybranými zákazníkmi. Ak sa chcete zapojiť, napíšte na [avemeo@sortec.sk](mailto:avemeo@sortec.sk).

**S ktorými AI asistentmi funguje?**
S každým asistentom, ktorý podporuje vzdialené MCP servery s OAuth: Claude (web, desktop, mobil), ChatGPT (vlastné konektory), Gemini CLI, Cursor, VS Code a ďalšie.

**Potrebujem vlastné predplatné AI?**
Áno. Konektor sa pripája k asistentovi, ktorý už používate. Pre zákazníkov bez vlastného AI nástroja je vo vývoji AI asistent zabudovaný v Avemeo CMS.

**Čo asistent dokáže?**
Nájsť a prečítať obrazovky, playlisty, plánovače, médiá a zariadenia; pripraviť a – po vašom schválení – vykonať zmeny playlistov, plánovačov a obrazoviek; vytvárať obrazovky zo šablón; posielať príkazy zariadeniam (zapnúť, vypnúť, obnoviť, reštartovať); robiť reporty prehrávania a výpadkov.

**Čo nedokáže?**
Mazať obsah. Konať bez vášho schválenia. Pristupovať ku kontám alebo oblastiam, ktoré ste pri prihlásení nepovolili.

**Vie spúšťať reporty automaticky?**
Asistenti s naplánovanými úlohami (napríklad Claude) vedia spúšťať pokyn podľa rozvrhu, napríklad ranný zoznam zariadení, ktoré boli včera offline.

## Bezpečnosť a dáta

**Ako funguje prihlásenie?**
Cez OAuth na prihlasovacej stránke Avemeo. Asistent dostane obmedzený token; vaše heslo nikdy nevidí. Token môžete v Avemeo kedykoľvek odvolať.

**Schvaľuje sa každá zmena?**
Áno. Konektor pripraví plán so zhrnutím pred/po; zmena sa vykoná až po vašom schválení. Každé volanie sa zapisuje do auditu s používateľom a AI klientom.

**Používajú sa moje dáta na trénovanie AI modelov?**
Dáta idú k AI asistentovi, ktorého ste si zvolili, podľa podmienok a plánu vášho poskytovateľa AI. Firemné a podnikové plány hlavných poskytovateľov spravidla trénovanie na zákazníckych dátach vylučujú. Avemeo dostáva len volania nástrojov, ktoré asistent robí.

**Čo s prompt injection?**
Obsah uložený v Avemeo (názvy obrazoviek, texty, názvy médií) sa berie ako dáta, nie ako pokyny pre asistenta.

**Ako nahlásim bezpečnostný problém?**
Pozrite [SECURITY.md](../../SECURITY.md).

## Pilot, cena a kontakt

**Ako sa zapojím do pilotu?**
Pošlite krátku správu s odvetvím, počtom zariadení a AI asistentom, ktorý používate, na [avemeo@sortec.sk](mailto:avemeo@sortec.sk).

**Koľko konektor stojí?**
Cena a dostupnosť budú oznámené pri spustení; účastníci pilotu dostanú informácie individuálne.

**Kde si môžem Avemeo pozrieť?**
[avemeo.sk](https://avemeo.sk), alebo si vyžiadajte ukážku na [avemeo@sortec.sk](mailto:avemeo@sortec.sk).

**Ako nahlásim chybu v tejto dokumentácii?**
[Založte issue](https://github.com/sortec-europe/avemeo-api/issues/new/choose) alebo pošlite pull request – pozrite [CONTRIBUTING.md](../../CONTRIBUTING.md).
