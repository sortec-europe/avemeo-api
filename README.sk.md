# Avemeo API a AI konektor

**Avemeo** je cloudová platforma pre digital signage, hotelovú TV a audio a video v predajniach. Tento repozitár popisuje **Avemeo REST API** a **AI konektor Avemeo (MCP)**, cez ktorý zákazník spravuje svoje obrazovky, playlisty a zariadenia z AI asistenta, ktorého už používa – Claude, ChatGPT, Gemini a ďalších nástrojov s podporou MCP.

> 🇬🇧 English version: [README.md](README.md)

| | |
|---|---|
| Platforma | Avemeo CMS (web), prehrávače na LG, Samsung, Vestel, Android, Raspberry Pi a IPTV boxoch ARRIS VIP4302 |
| Cloudy | Avemeo (`ds.avemeo.com`) a [Business Stream](https://www.telekom.sk/biznis/stredne-velke-firmy/business-stream) od Slovak Telekomu (`cloud.tvstream.sk`) |
| REST API | špecifikácia OpenAPI 3, viac ako 380 operácií – [prehľad](docs/api-overview.md) |
| AI konektor (MCP) | **Vo vývoji – pripravujeme pilot s vybranými zákazníkmi.** [Podrobnosti](docs/mcp-connector.md) |
| AI asistent v CMS | **Vo vývoji** – tím Avemeo pripravuje aj AI asistenta priamo v Avemeo CMS pre zákazníkov, ktorí nepoužívajú vlastný AI nástroj. |

## Čo urobíte s Avemeo a AI

S konektorom Avemeo budete môcť napísať AI asistentovi bežnou rečou, po slovensky, česky alebo anglicky:

- *„Daj od piatku do playlistu recepcie novú jesennú ponuku, 10 sekúnd na snímku.“*
- *„Ktoré prehrávače v predajniach boli včera počas otváracích hodín offline?“*
- *„Sprav anglickú verziu hotelového menu a pridaj prepínač jazyka.“*
- *„Reštartuj všetky obrazovky v skupine Košice.“*
- *„Čo práve hrá v izbe 204?“*

Asistent bude čítať a meniť obsah len vo **vašom** konte Avemeo, s **vašimi** oprávneniami. Každú zmenu najprv ukáže na schválenie a zapíše do auditu. Pozrite [príklady použitia](docs/use-cases.md).

## Čo platforma Avemeo vie

- **Digital signage** – vizuálny editor obrazoviek s widgetmi (text, obrázky, video, hodiny, počasie, meniny, RSS, aplikácie), playlisty a časovače s dňami v týždni, obdobiami a sviatkami.
- **Interaktívne obrazovky** – viacúrovňové menu ovládané diaľkovým ovládačom alebo dotykom, viacjazyčný obsah s prepínačom jazyka.
- **Hotelová TV** – živé TV kanály (HLS) s EPG, meno hosťa a číslo izby na obrazovke, účet hosťa, správy, napojenie check-in/check-out na hotelový systém, aplikácie Netflix, YouTube a Chromecast.
- **Audio a video v predajniach** – hudba a spoty v náhodnom poradí, kampane podľa predajní, štatistiky prehrávania po zariadeniach, obrazovkách a súboroch s exportom do CSV.
- **Správa zariadení** – zapnutie a vypnutie, obnovenie, reštart, hlasitosť, TV kanál, screenshoty, sledovanie online/offline s upozornením e-mailom a SMS.
- **Kiosky a ďalšie** – hotelový kiosk, vyvolávací systém, kvízy, digitálne menu.

## Rýchly štart: REST API

```bash
BASE_URL=https://cloud.tvstream.sk/backend   # alebo váš cloud Avemeo

# 1. Prihlásenie – odpoveď obsahuje prístupový token (accessKey)
curl -s -X POST "$BASE_URL/api/auth/login" \
  -H "Content-Type: application/json" \
  -d '{"username":"POUZIVATEL","password":"HESLO"}'

# 2. Zoznam playlistov konta
curl -s -X POST "$BASE_URL/api/playlist" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Active-Profile-Id: $ID_KONTA" \
  -H "Content-Type: application/json" \
  -d '{"filter":{},"page_number":1,"page_size":100,"sort_field":"id","sort_order":"asc"}'
```

Celá špecifikácia: `https://<váš-cloud>/backend/openapi/`. Podrobnosti a autentifikácia: [docs/api-overview.md](docs/api-overview.md).

## AI konektor (MCP)

Konektor Avemeo je vzdialený server [Model Context Protocol](https://modelcontextprotocol.io). Keď bude pre vaše konto dostupný, pridáte ho do AI asistenta raz:

1. V AI asistentovi otvorte nastavenia konektorov (v Claude: **Customize → Connectors → Add custom connector**).
2. Zadajte adresu konektora podľa vášho cloudu:
   - Avemeo (`ds.avemeo.com`): `https://mcp.avemeo.com/mcp`
   - [Business Stream](https://www.telekom.sk/biznis/stredne-velke-firmy/business-stream) (`cloud.tvstream.sk`): `https://mcp.tvstream.sk/mcp`
3. Prihláste sa svojím účtom Avemeo a zvoľte, k čomu má asistent prístup.

Stav, nástroje a bezpečnosť: [docs/mcp-connector.md](docs/mcp-connector.md).

## AI asistent v CMS

Nie každý používa vlastný AI nástroj. Tím Avemeo preto pripravuje aj AI asistenta priamo v Avemeo CMS. Bude používať rovnaké nástroje ako konektor, každú zmenu ukáže v CMS na náhľad a uloží ju až po schválení. Stav: vo vývoji.

## Kontakt

- Avemeo: [avemeo.sk](https://avemeo.sk), [avemeo@sortec.sk](mailto:avemeo@sortec.sk)
- Predaj, nasadenie a pilotný program (Slovensko): **SORTEC EUROPE s.r.o.** – distribútor a obchodno-vývojový partner Avemeo, partner pre [Business Stream](https://www.telekom.sk/biznis/stredne-velke-firmy/business-stream) v Slovak Telekom. [avemeo@sortec.sk](mailto:avemeo@sortec.sk)

---

Repozitár spravuje **SORTEC EUROPE s.r.o.**, distribútor a obchodno-vývojový partner Avemeo a partner pre [Business Stream](https://www.telekom.sk/biznis/stredne-velke-firmy/business-stream) v Slovak Telekom. Avemeo je produkt spoločnosti Avemeo s.r.o. Dokumentácia je poskytovaná pod licenciou [CC BY 4.0](LICENSE).
