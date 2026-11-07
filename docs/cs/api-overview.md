# Avemeo REST API – přehled

> 🇬🇧 English version: [../api-overview.md](../api-overview.md) · 🇸🇰 Slovenská verzia: [../sk/api-overview.md](../sk/api-overview.md) · ⬅ Zpět na [README](../../README.cs.md)

**Avemeo REST API** je programové rozhraní cloudové platformy Avemeo pro digital signage, hotelovou TV a audio v prodejnách. Je to **stejné API, které používá webová aplikace Avemeo CMS**, takže vše, co uděláte v CMS – média, obrazovky, playlisty, plánovače, zařízení, dálkové ovládání, statistiky – zvládnete i z vlastního softwaru. Popisuje ho specifikace **OpenAPI 3** zveřejněná na každém cloudu Avemeo.

Typické použití:

- propojení Avemeo s **hotelovým systémem (PMS)**, ERP, rezervační nebo marketingovou platformou,
- automatizace opakovaných změn obsahu (kampaně, sezónní menu, ceníky),
- **monitoring a reporting** nad stavy zařízení a statistikami přehrávání (proof of play),
- základ pro [AI konektor Avemeo (MCP)](mcp-connector.md), který toto API používá na pozadí.

## Kde najdete specifikaci

| | |
|---|---|
| Interaktivní dokumentace (Swagger UI) | `https://<váš-cloud>/backend/openapi/` |
| Soubor specifikace (JSON) | `https://<váš-cloud>/backend/api/openapi/doc` |
| Základní cesta serveru | `/backend` |
| Rozsah | více než 380 operací na více než 350 cestách |

`<váš-cloud>` nahraďte cloudem, na kterém máte účet:

| Cloud | Host | Příklad základní adresy |
|---|---|---|
| Avemeo | `ds.avemeo.com` | `https://ds.avemeo.com/backend` |
| [Business Stream](https://www.telekom.sk/biznis/stredne-velke-firmy/business-stream) od Slovak Telekomu | `cloud.tvstream.sk` | `https://cloud.tvstream.sk/backend` |

K použití API potřebujete účet Avemeo na daném cloudu. Specifikace obsahuje schémata přímo v operacích a zatím bez popisů polí – kontext doplňuje tato stránka a [slovník pojmů](glossary.md).

## Autentizace

| Způsob | Hlavička | Použití |
|---|---|---|
| **Bearer token (JWT)** | `Authorization: Bearer <token>` | Správa obsahu a účtu. Token získáte přes `POST /api/auth/login`. |
| **Výběr účtu** | `Active-Profile-Id: <id účtu>` | Určuje účet (profil) Avemeo, se kterým požadavek pracuje. Jeden uživatel může mít přístup do více účtů. |
| **API klíč** | `api-key: <klíč>` | Dálkové ovládání zařízení (`/api/remote/…`). |

Příklad přihlášení:

```bash
BASE_URL=https://cloud.tvstream.sk/backend

curl -s -X POST "$BASE_URL/api/auth/login" \
  -H "Content-Type: application/json" \
  -d '{"username":"UZIVATEL","password":"HESLO"}'
# → {"status":"success","data":{"accessToken":"<JWT>"}}
```

Token pak posílejte v každém dalším požadavku spolu s id účtu:

```bash
TOKEN=...        # accessToken z odpovědi na přihlášení
ID_UCTU=...      # id účtu (profilu) Avemeo

curl -s -X POST "$BASE_URL/api/playlist" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Active-Profile-Id: $ID_UCTU" \
  -H "Content-Type: application/json" \
  -d '{"filter":{},"page_number":1,"page_size":100,"sort_field":"id","sort_order":"asc"}'
```

**Tokeny a API klíče držte v tajnosti.** Vytvořte samostatného uživatele pro API s minimálními potřebnými oprávněními, nedávejte tokeny do URL, logů ani dokumentů a při úniku změňte heslo.

## Formát odpovědi

Odpovědi jsou JSON objekty s poli `status` a `data`:

```json
{ "status": "success", "data": { "...": "..." } }
```

Při chybě je `status` roven `"error"`. Seznamové endpointy vracejí položky spolu s celkovým počtem (například seznam zařízení vrací `data.entities` a `data.total_count`).

## Hlavní oblasti

| Oblast | Endpointy (příklady) | Účel |
|---|---|---|
| **Složky** | `GET /api/tree/all/{type}/edit`, `POST /api/tree/update` | Stromy složek pro média, obrazovky, playlisty a zařízení (`{type}` = `medium`, `screen`, `playlist`, `device`) |
| **Média** | `POST /api/media`, `GET /api/media/fetch/{id}`, `PUT /api/media/update`, `POST /api/media/transfer`, `PUT /api/media/setfolder` | Knihovna médií: obrázky, video, audio; nahrávání a přesun mezi složkami |
| **Obrazovky** | `POST /api/screen`, `GET /api/screen/widgets/fetch/{id}`, `PUT /api/screen/widgets/update`, `POST /api/screen/duplicate` | Rozložení obrazovek (standardně 1920 × 1080) s widgety, interaktivními úrovněmi a překlady |
| **Playlisty** | `POST /api/playlist`, `GET /api/playlist/fetch/{id}`, `PUT /api/playlist/update`, `POST /api/playlist/duplicate` | Sekvence obrazovek, médií a živých kanálů s trváním a platností |
| **Plánovače** | `POST /api/scheduler`, `GET /api/scheduler/fetch/{id}`, `PUT /api/scheduler/update` | Co kdy hraje: dny v týdnu, časy, období, svátky, zapínání a vypínání |
| **Zařízení** | `POST /api/device`, `GET /api/device/fetch/{id}`, `GET /api/device/screenshot/{id}`, `POST /api/device/mcontrol/{action}` | Seznam a stav zařízení; `on`, `off`, `reload`, `reboot` pro jedno nebo více zařízení |
| **Obsah zařízení** | `GET /api/sconnection?type=device&id={id}`, `POST /api/sconnection/update` | Kterou obrazovku (a úroveň) nebo plánovač zařízení přehrává |
| **Dálkové ovládání** | `PUT /api/remote/box/power/{state}/{box_id}`, `…/audio/volume/…`, `…/tvchannel/…`, `…/keycode/…` | Napájení, hlasitost, TV kanál a stisky kláves (API klíč) |
| **Statistiky** | `PUT /api/stats/device`, `PUT /api/stats/screenmedium` | Proof of play: stav zařízení po minutách, přehrané obrazovky a média za den |
| **Počasí, jazyky, překlady** | `/api/weather`, `/api/language`, `/api/translation` | Místa počasí, jazyky účtu, překlady textů obrazovek |
| **Monitoring** | `/api/monitor` | Upozornění na výpadky e-mailem a SMS |

## Příklady

### Stav zařízení za jeden den (proof of play)

```bash
curl -s -X PUT "$BASE_URL/api/stats/device" \
  -H "Authorization: Bearer $TOKEN" -H "Active-Profile-Id: $ID_UCTU" \
  -H "Content-Type: application/json" \
  -d '{"id": 2081, "date": "2026-10-31"}'
```

Odpověď obsahuje `states` (jeden záznam za minutu: `2` = zapnuto a hraje, `1` = výstup vypnutý, `0` = offline) a `screens` a `media` přehrané v daný den. Z těchto dat vycházejí otázky typu *„které přehrávače byly včera během otevírací doby offline?“*.

### Restart zařízení

```bash
curl -s -X POST "$BASE_URL/api/device/mcontrol/reboot" \
  -H "Authorization: Bearer $TOKEN" -H "Active-Profile-Id: $ID_UCTU" \
  -H "Content-Type: application/json" \
  -d '{"ids": [2081, 2747]}'
```

Další akce: `on`, `off`, `reload`.

### Seznam zařízení ve složce

```bash
curl -s -X POST "$BASE_URL/api/device" \
  -H "Authorization: Bearer $TOKEN" -H "Active-Profile-Id: $ID_UCTU" \
  -H "Content-Type: application/json" \
  -d '{"filter":{"tree_id": <id složky>},"page_number":1,"page_size":100}'
```

### Načtení obrazovky s widgety

```bash
curl -s "$BASE_URL/api/screen/widgets/fetch/<id obrazovky>" \
  -H "Authorization: Bearer $TOKEN" -H "Active-Profile-Id: $ID_UCTU"
```

Každý widget má typ (`block`, `datetime`, `presentation`, `tv`, `weather_symbol`, …), `widget_order` (nižší číslo = vpředu) a `params_json` s polohou (`top`, `left`, `width`, `height`) a obsahem.

## Konvence a tipy

- **Seznamy používají `POST` se stránkováním:** `{"filter":{}, "page_number":1, "page_size":100, "sort_field":"id", "sort_order":"asc"}`. Filtr podle složky: `{"filter":{"tree_id": <id složky>}}`.
- **ID:** obrazovky, playlisty a média mají dlouhá číselná ID – v JavaScriptu a jiných jazycích s 53bitovými celými čísly s nimi pracujte jako s řetězci. ID zařízení jsou běžná celá čísla.
- **Složky:** při ukládání obrazovek a playlistů vždy posílejte `tree_id` (složku).
- **JSON v řetězcích:** některá pole obsahují JSON zakódovaný jako řetězec (například `params_json`, `datetime_json`, `days_json`). Před použitím je rozparsujte a před uložením znovu zakódujte.
- **Položky playlistu** odkazují na obrazovku a úroveň (`screen_id`, `screen_level`), mají `duration` v sekundách a příznak `active`; trvání aktivních položek dává délku playlistu.
- **Překlady** textů obrazovek jsou v parametrech s jazykovou příponou, například `_lng_en`.
- **Změny na běžících zařízeních:** po úpravě obrazovky, která právě hraje, pošlete zařízení `reload`, aby si změnu načetlo.
- **Záloha před zápisem:** před každou úpravou si původní objekt načtěte a uložte, abyste ho uměli obnovit.

## Často kladené otázky

**Je Avemeo API veřejné?**
Specifikace je zveřejněna na každém cloudu Avemeo a tato dokumentace je veřejná. K použití API potřebujete účet Avemeo s příslušnými oprávněními.

**Existuje testovací účet?**
Napište na [avemeo@sortec.sk](mailto:avemeo@sortec.sk) – přístup pro integrátory a pilotní zákazníky se řeší individuálně.

**Jsou nějaké limity počtu požadavků?**
Veřejné limity nejsou zdokumentovány. Automatizované dotazování držte v rozumných mezích (například statistiky jednou denně za zařízení) a před vysokoobjemovou integrací se nám ozvěte.

**Mění se API?**
Vyvíjí se spolu s CMS. Aktuální referencí je vždy specifikace na vašem cloudu; změny v této dokumentaci jsou v [CHANGELOG.md](../../CHANGELOG.md).

**Dá se API používat bez programování?**
Ano – právě k tomu slouží [AI konektor (MCP)](mcp-connector.md): váš AI asistent volá API za vás, s vašimi oprávněními a po vašem schválení.

## Související

- [AI konektor (MCP)](mcp-connector.md) – správa Avemeo z Claude, ChatGPT nebo Gemini
- [Příklady použití](use-cases.md) – k čemu se API a konektor používají
- [Slovník pojmů](glossary.md) – obrazovky, widgety, úrovně, playlisty, plánovače, proof of play
- [README](../../README.cs.md) – přehled platformy a kontakt
