# Slovník pojmov – digital signage, hotelová TV, Avemeo a MCP

> 🇬🇧 English version: [../glossary.md](../glossary.md) · 🇨🇿 Česká verze: [../cs/glossary.md](../cs/glossary.md) · ⬅ Späť na [README](../../README.sk.md)

Krátke definície pojmov, ktoré sa používajú v tejto dokumentácii, v Avemeo CMS a v AI konektore. Abecedne.

**AI asistent (MCP klient)** – AI aplikácia, ktorá vie používať MCP servery: Claude, ChatGPT, Gemini CLI, Cursor, VS Code a ďalšie.

**Audit** – záznam každej akcie vrátane akcií cez AI konektor, s používateľom, klientom a časom.

**Avemeo** – cloudová platforma (CMS) pre digital signage, hotelovú TV a audio a video v predajniach od spoločnosti Avemeo s.r.o. Prevádzkovaná v cloude Avemeo (`ds.avemeo.com`) a ako Business Stream v Slovak Telekome (`cloud.tvstream.sk`).

**Business Stream** – služba Slovak Telekomu pre digital signage a hotelovú TV, ktorá beží na platforme Avemeo.

**CMS (systém na správu obsahu)** – webová aplikácia, v ktorej sa obsah tvorí, plánuje a priraďuje zariadeniam. V Avemeo zdieľajú CMS a REST API ten istý backend.

**Diaľkové ovládanie (remote control API)** – endpointy API (overované API kľúčom) na napájanie, hlasitosť, TV kanál a stlačenia kláves na zariadení.

**Digital signage** – centrálne riadený obsah na obrazovkách vo verejných a komerčných priestoroch: akcie, menu, informácie, navigácia, živá TV. Po slovensky aj „digitálne obrazovky“ alebo „digitálne vývesky“.

**EPG (elektronický programový sprievodca)** – prehľad TV programu v prehrávači hotelovej TV.

**HLS (HTTP Live Streaming)** – formát streamovania, ktorý Avemeo používa pre živé TV kanály.

**Hotelová TV / hotelová IPTV** – TV pre hotelové izby so živými kanálmi, uvítacou obrazovkou s menom hosťa, interaktívnym menu služieb, správami a aplikáciami (Netflix, YouTube, Chromecast). IPTV prenáša kanály cez IP sieť hotela.

**Interaktívne menu** – obrazovka s viacerými úrovňami, v ktorej sa hosť alebo návštevník pohybuje diaľkovým ovládačom alebo dotykom, často vo viacerých jazykoch.

**Konto (profil)** – priestor zákazníka v Avemeo s vlastnými médiami, obrazovkami, playlistmi, plánovačmi, zariadeniami a používateľmi. Jeden používateľ môže mať prístup do viacerých kont; požiadavky API vyberajú konto hlavičkou `Active-Profile-Id`.

**MCP (Model Context Protocol)** – otvorený štandard na pripájanie AI asistentov k externým nástrojom a dátam. *Vzdialený MCP server* beží na internete a asistent ho používa cez HTTPS s prihlásením cez OAuth. AI konektor Avemeo je vzdialený MCP server.

**Naplánovaná úloha** – funkcia niektorých AI asistentov (napríklad Claude), ktorá spúšťa pokyn podľa rozvrhu, napríklad denný report výpadkov cez konektor.

**OAuth** – štandard prihlásenia, ktorý používa AI konektor. Používateľ sa prihlási na stránke Avemeo; asistent dostane obmedzený, odvolateľný token a heslo nikdy nevidí.

**Obrazovka** – rozloženie (štandardne 1920 × 1080) zložené z widgetov; základná jednotka obsahu v Avemeo. Obrazovka môže mať viac úrovní a prekladov.

**Obsah zariadenia** – priradenie toho, čo zariadenie prehráva: obrazovka s úrovňou alebo plánovač.

**OpenAPI** – štandardný strojovo čitateľný popis REST API. Avemeo zverejňuje špecifikáciu OpenAPI 3 na každom cloude na adrese `/backend/openapi/`.

**Plán (dvojkrokový zápis)** – v AI konektore sa každá zmena najprv pripraví ako plán so zhrnutím pred/po a vykoná sa až po schválení používateľom.

**Plánovač** – určuje, čo kedy hrá: časové sloty s dňami v týždni, časmi, obdobiami a sviatkami, voliteľne so zapnutím a vypnutím v každom slote. Zariadeniu možno namiesto jednej obrazovky priradiť plánovač.

**Playlist** – usporiadaná sekvencia položiek (obrazovky, médiá, živé kanály) s trvaním v sekundách pre každú položku, prehrávaná dookola. Položky môžu mať dátumy a časy platnosti.

**PMS (property management system)** – recepčný systém hotela. Hotelová TV Avemeo sa integruje s hotelovými systémami pri check-ine a check-oute.

**Prezentačný widget** – celoobrazovkový widget, ktorý na obrazovke prehráva playlist.

**Proof of play** – štatistiky dokazujúce, čo sa kde a kedy prehralo: stav zariadenia po minútach a obrazovky a médiá prehrané v každý deň. Používa sa na reklamné reporty a analýzu výpadkov.

**Šablóna** – hotová obrazovka alebo menu v Avemeo, ktoré sa zduplikuje a naplní textami, obrázkami a jazykmi zákazníka.

**Úroveň** – jeden stav interaktívnej obrazovky (napríklad hlavné menu, stránka reštaurácie, výber jazyka). Widgety sú viditeľné alebo aktívne na konkrétnych úrovniach; tlačidlá prepínajú medzi úrovňami.

**Widget** – stavebný prvok obrazovky: textový blok, obrázok, video, hodiny, dátum, počasie, meniny, RSS, TV prehrávač, prezentácia (prehrávač playlistu), aplikácie a ďalšie. Každý widget má polohu, veľkosť, poradie (nižšie číslo = vpredu) a parametre.

**Zariadenie (prehrávač)** – hardvér, ktorý prehráva obsah: displej LG, Samsung alebo Vestel so zabudovaným prehrávačom, prehrávač alebo TV s Androidom, Raspberry Pi alebo IPTV set-top box ARRIS. Každému zariadeniu je priradená obrazovka (a úroveň) alebo plánovač.
