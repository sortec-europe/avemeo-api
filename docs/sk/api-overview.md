# Avemeo REST API – prehľad

> 🇬🇧 English version: [../api-overview.md](../api-overview.md) · ⬅ Späť na [README](../../README.sk.md)

**Avemeo REST API** je programové rozhranie cloudovej platformy Avemeo pre digital signage, hotelovú TV a audio v predajniach. Je to **to isté API, ktoré používa webová aplikácia Avemeo CMS**, takže všetko, čo urobíte v CMS – médiá, obrazovky, playlisty, plánovače, zariadenia, diaľkové ovládanie, štatistiky – viete urobiť aj z vlastného softvéru. Popisuje ho špecifikácia **OpenAPI 3** zverejnená na každom cloude Avemeo.

Typické použitie:

- prepojenie Avemeo s **hotelovým systémom (PMS)**, ERP, rezervačnou alebo marketingovou platformou,
- automatizácia opakovaných zmien obsahu (kampane, sezónne menu, cenníky),
- **monitoring a reporting** nad stavmi zariadení a štatistikami prehrávania (proof of play),
- základ pre [AI konektor Avemeo (MCP)](mcp-connector.md), ktorý toto API používa na pozadí.

## Kde nájdete špecifikáciu

| | |
|---|---|
| Interaktívna dokumentácia (Swagger UI) | `https://<váš-cloud>/backend/openapi/` |
| Súbor špecifikácie (JSON) | `https://<váš-cloud>/backend/api/openapi/doc` |
| Základná cesta servera | `/backend` |
| Rozsah | viac ako 380 operácií na viac ako 350 cestách |

`<váš-cloud>` nahraďte cloudom, na ktorom máte konto:

| Cloud | Host | Príklad základnej adresy |
|---|---|---|
| Avemeo | `ds.avemeo.com` | `https://ds.avemeo.com/backend` |
| [Business Stream](https://www.telekom.sk/biznis/stredne-velke-firmy/business-stream) od Slovak Telekomu | `cloud.tvstream.sk` | `https://cloud.tvstream.sk/backend` |

Na použitie API potrebujete účet Avemeo na danom cloude. Špecifikácia obsahuje schémy priamo v operáciách a zatiaľ bez popisov polí – kontext dopĺňa táto stránka a [slovník pojmov](glossary.md).

## Autentifikácia

| Spôsob | Hlavička | Použitie |
|---|---|---|
| **Bearer token (JWT)** | `Authorization: Bearer <token>` | Správa obsahu a konta. Token získate cez `POST /api/auth/login`. |
| **Výber konta** | `Active-Profile-Id: <id konta>` | Určuje konto (profil) Avemeo, s ktorým požiadavka pracuje. Jeden používateľ môže mať prístup do viacerých kont. |
| **API kľúč** | `api-key: <kľúč>` | Diaľkové ovládanie zariadení (`/api/remote/…`). |

Príklad prihlásenia:

```bash
BASE_URL=https://cloud.tvstream.sk/backend

curl -s -X POST "$BASE_URL/api/auth/login" \
  -H "Content-Type: application/json" \
  -d '{"username":"POUZIVATEL","password":"HESLO"}'
# → {"status":"success","data":{"accessToken":"<JWT>"}}
```

Token potom posielajte v každej ďalšej požiadavke spolu s id konta:

```bash
TOKEN=...        # accessToken z odpovede na prihlásenie
ID_KONTA=...     # id konta (profilu) Avemeo

curl -s -X POST "$BASE_URL/api/playlist" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Active-Profile-Id: $ID_KONTA" \
  -H "Content-Type: application/json" \
  -d '{"filter":{},"page_number":1,"page_size":100,"sort_field":"id","sort_order":"asc"}'
```

**Tokeny a API kľúče držte v tajnosti.** Vytvorte samostatného používateľa pre API s minimálnymi potrebnými oprávneniami, nedávajte tokeny do URL, logov ani dokumentov a pri úniku zmeňte heslo.

## Formát odpovede

Odpovede sú JSON objekty s poľami `status` a `data`:

```json
{ "status": "success", "data": { "...": "..." } }
```

Pri chybe je `status` rovný `"error"`. Zoznamové endpointy vracajú položky spolu s celkovým počtom (napríklad zoznam zariadení vracia `data.entities` a `data.total_count`).

## Hlavné oblasti

| Oblasť | Endpointy (príklady) | Účel |
|---|---|---|
| **Priečinky** | `GET /api/tree/all/{type}/edit`, `POST /api/tree/update` | Stromy priečinkov pre médiá, obrazovky, playlisty a zariadenia (`{type}` = `medium`, `screen`, `playlist`, `device`) |
| **Médiá** | `POST /api/media`, `GET /api/media/fetch/{id}`, `PUT /api/media/update`, `POST /api/media/transfer`, `PUT /api/media/setfolder` | Knižnica médií: obrázky, video, audio; nahrávanie a presun medzi priečinkami |
| **Obrazovky** | `POST /api/screen`, `GET /api/screen/widgets/fetch/{id}`, `PUT /api/screen/widgets/update`, `POST /api/screen/duplicate` | Rozloženia obrazoviek (štandardne 1920 × 1080) s widgetmi, interaktívnymi úrovňami a prekladmi |
| **Playlisty** | `POST /api/playlist`, `GET /api/playlist/fetch/{id}`, `PUT /api/playlist/update`, `POST /api/playlist/duplicate` | Sekvencie obrazoviek, médií a živých kanálov s trvaním a platnosťou |
| **Plánovače** | `POST /api/scheduler`, `GET /api/scheduler/fetch/{id}`, `PUT /api/scheduler/update` | Čo kedy hrá: dni v týždni, časy, obdobia, sviatky, zapínanie a vypínanie |
| **Zariadenia** | `POST /api/device`, `GET /api/device/fetch/{id}`, `GET /api/device/screenshot/{id}`, `POST /api/device/mcontrol/{action}` | Zoznam a stav zariadení; `on`, `off`, `reload`, `reboot` pre jedno alebo viac zariadení |
| **Obsah zariadenia** | `GET /api/sconnection?type=device&id={id}`, `POST /api/sconnection/update` | Ktorú obrazovku (a úroveň) alebo plánovač zariadenie prehráva |
| **Diaľkové ovládanie** | `PUT /api/remote/box/power/{state}/{box_id}`, `…/audio/volume/…`, `…/tvchannel/…`, `…/keycode/…` | Napájanie, hlasitosť, TV kanál a stlačenia kláves (API kľúč) |
| **Štatistiky** | `PUT /api/stats/device`, `PUT /api/stats/screenmedium` | Proof of play: stav zariadenia po minútach, prehrané obrazovky a médiá za deň |
| **Počasie, jazyky, preklady** | `/api/weather`, `/api/language`, `/api/translation` | Miesta počasia, jazyky konta, preklady textov obrazoviek |
| **Monitoring** | `/api/monitor` | Upozornenia na výpadky e-mailom a SMS |

## Príklady

### Stav zariadenia za jeden deň (proof of play)

```bash
curl -s -X PUT "$BASE_URL/api/stats/device" \
  -H "Authorization: Bearer $TOKEN" -H "Active-Profile-Id: $ID_KONTA" \
  -H "Content-Type: application/json" \
  -d '{"id": 2081, "date": "2026-10-31"}'
```

Odpoveď obsahuje `states` (jeden záznam za minútu: `2` = zapnuté a hrá, `1` = výstup vypnutý, `0` = offline) a `screens` a `media` prehrané v daný deň. Z týchto dát vychádzajú otázky typu *„ktoré prehrávače boli včera počas otváracích hodín offline?“*.

### Reštart zariadení

```bash
curl -s -X POST "$BASE_URL/api/device/mcontrol/reboot" \
  -H "Authorization: Bearer $TOKEN" -H "Active-Profile-Id: $ID_KONTA" \
  -H "Content-Type: application/json" \
  -d '{"ids": [2081, 2747]}'
```

Ďalšie akcie: `on`, `off`, `reload`.

### Zoznam zariadení v priečinku

```bash
curl -s -X POST "$BASE_URL/api/device" \
  -H "Authorization: Bearer $TOKEN" -H "Active-Profile-Id: $ID_KONTA" \
  -H "Content-Type: application/json" \
  -d '{"filter":{"tree_id": <id priečinka>},"page_number":1,"page_size":100}'
```

### Načítanie obrazovky s widgetmi

```bash
curl -s "$BASE_URL/api/screen/widgets/fetch/<id obrazovky>" \
  -H "Authorization: Bearer $TOKEN" -H "Active-Profile-Id: $ID_KONTA"
```

Každý widget má typ (`block`, `datetime`, `presentation`, `tv`, `weather_symbol`, …), `widget_order` (nižšie číslo = vpredu) a `params_json` s polohou (`top`, `left`, `width`, `height`) a obsahom.

## Konvencie a tipy

- **Zoznamy používajú `POST` so stránkovaním:** `{"filter":{}, "page_number":1, "page_size":100, "sort_field":"id", "sort_order":"asc"}`. Filter podľa priečinka: `{"filter":{"tree_id": <id priečinka>}}`.
- **ID:** obrazovky, playlisty a médiá majú dlhé číselné ID – v JavaScripte a iných jazykoch s 53-bitovými celými číslami s nimi pracujte ako s reťazcami. ID zariadení sú bežné celé čísla.
- **Priečinky:** pri ukladaní obrazoviek a playlistov vždy posielajte `tree_id` (priečinok).
- **JSON v reťazcoch:** niektoré polia obsahujú JSON zakódovaný ako reťazec (napríklad `params_json`, `datetime_json`, `days_json`). Pred použitím ich rozparsujte a pred uložením znova zakódujte.
- **Položky playlistu** odkazujú na obrazovku a úroveň (`screen_id`, `screen_level`), majú `duration` v sekundách a príznak `active`; trvania aktívnych položiek dávajú dĺžku playlistu.
- **Preklady** textov obrazoviek sú v parametroch s jazykovou príponou, napríklad `_lng_en`.
- **Zmeny na bežiacich zariadeniach:** po úprave obrazovky, ktorá práve hrá, pošlite zariadeniu `reload`, aby si zmenu načítalo.
- **Záloha pred zápisom:** pred každou úpravou si pôvodný objekt načítajte a uložte, aby ste ho vedeli obnoviť.

## Často kladené otázky

**Je Avemeo API verejné?**
Špecifikácia je zverejnená na každom cloude Avemeo a táto dokumentácia je verejná. Na použitie API potrebujete účet Avemeo s príslušnými oprávneniami.

**Existuje testovacie konto?**
Napíšte na [avemeo@sortec.sk](mailto:avemeo@sortec.sk) – prístup pre integrátorov a pilotných zákazníkov sa rieši individuálne.

**Sú nejaké limity počtu požiadaviek?**
Verejné limity nie sú zdokumentované. Automatizované dopytovanie držte v rozumných medziach (napríklad štatistiky raz denne za zariadenie) a pred vysokoobjemovou integráciou sa nám ozvite.

**Mení sa API?**
Vyvíja sa spolu s CMS. Aktuálnou referenciou je vždy špecifikácia na vašom cloude; zmeny v tejto dokumentácii sú v [CHANGELOG.md](../../CHANGELOG.md).

**Dá sa API používať bez programovania?**
Áno – práve na to slúži [AI konektor (MCP)](mcp-connector.md): váš AI asistent volá API za vás, s vašimi oprávneniami a po vašom schválení.

## Súvisiace

- [AI konektor (MCP)](mcp-connector.md) – správa Avemeo z Claude, ChatGPT alebo Gemini
- [Príklady použitia](use-cases.md) – na čo sa API a konektor používajú
- [Slovník pojmov](glossary.md) – obrazovky, widgety, úrovne, playlisty, plánovače, proof of play
- [README](../../README.sk.md) – prehľad platformy a kontakt
