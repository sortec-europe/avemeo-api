# Příklady použití: Avemeo s AI asistentem

> 🇬🇧 English version: [../use-cases.md](../use-cases.md) · 🇸🇰 Slovenská verzia: [../sk/use-cases.md](../sk/use-cases.md) · ⬅ Zpět na [README](../../README.cs.md)

Co budou zákazníci moci dělat s Avemeo a AI asistentem (Claude, ChatGPT, Gemini a další MCP klienti), až bude dostupný [AI konektor](mcp-connector.md). Každý příklad ukazuje, co řeknete, co asistent udělá v Avemeo a co schvalujete. Stejné operace mají vývojáři k dispozici přes [REST API](api-overview.md).

**Obsah:** [Retail](#retail-prodejny-a-sítě) · [Hotely](#hotely-a-ubytování) · [Firmy, prostory a akce](#firmy-prostory-a-akce) · [Provoz a monitoring](#provoz-a-monitoring) · [Tvorba obsahu](#tvorba-obsahu) · [Vývojáři](#vývojáři-a-integrátoři)

## Retail: prodejny a sítě

### Proof of play a přehrávače offline

> *„Které přehrávače v prodejnách byly minulý týden během otevírací doby offline? Seřaď podle ztracených hodin.“*

Asistent načte stavy každého přehrávače po minutách, porovná je s otevírací dobou prodejny a vrátí tabulku po prodejnách se ztracenými hodinami a časy výpadků. Typický výsledek: většina přehrávačů hraje 98–100 % času; pár prodejen má opakované výpadky, které ukazují spíš na místní síť než na přehrávač.

> *„Restartuj audio přehrávač v prodejně na Hlavní a dej vědět, až zase hraje.“*

**Schvalujete:** restart jednoho pojmenovaného zařízení.

### Kampaně napříč prodejnami

> *„Dej od pondělí nový podzimní spot do všech audio playlistů prodejen, každých 15 minut, do konce listopadu.“*

Asistent najde playlisty prodejen, připraví jednu změnu s náhledem před/po pro každý playlist a po jednom schválení ji provede.

> *„Nahraď letní ceník na všech digitálních menu novým z knihovny médií.“*

**Schvalujete:** seznam playlistů nebo obrazovek, které se změní.

### Regionální a sezónní obsah

> *„Pouštěj vánoční playlist ve všech prodejnách od 1. prosince, ale v pražských začni o týden dřív.“*

Asistent vytvoří nebo upraví plánovače s obdobími podle skupin prodejen.

## Hotely a ubytování

### Interaktivní hotelové TV menu

> *„Vytvoř hotelové TV menu z kruhové šablony s TV, rádiem, restaurací, wellness, výlety a počasím, česky a anglicky.“*

Asistent vytvoří obrazovku ze šablony Avemeo, doplní texty, obrázky a překlady a ukáže náhled každé úrovně menu.

> *„Změň v menu čas snídaní na 7:00–10:30.“*

> *„Přidej německou verzi menu a přepínač jazyka.“*

**Schvalujete:** novou nebo změněnou obrazovku po kontrole náhledu.

### Komunikace s hosty

> *„Co právě hraje na pokoji 204?“*

> *„Dej uvítací zprávu pro konferenční skupinu na všechny pokoje ve 3. patře od pátku do neděle.“*

### Akce a konference

> *„Na zítřejší konferenci dej od 7:30 program na obrazovky v lobby a názvy sálů na obrazovky u dveří.“*

## Firmy, prostory a akce

### Recepce a lobby

> *„Vytvoř playlist pro recepci z pěti prezentačních obrazovek po 8 sekundách a pouštěj ho v pracovní dny 8:00–17:00.“*

> *„Co je právě na obrazovce v lobby?“*

### Navigace a vyvolávací systém

> *„Přejmenuj zasedačku ‚Tatry‘ na ‚Fatra‘ na všech navigačních obrazovkách.“*

### Jídelny a digitální menu

> *„Nahraj menu jídelny na tento týden na obrazovky v kantýně a v sobotu přepni na víkendové menu.“*

## Provoz a monitoring

### Denní report

> *„Každé ráno mi pošli seznam zařízení, která byla včera offline.“* (přes naplánované úlohy v AI asistentovi)

### Správa napájení

> *„Vypni všechny obrazovky v brněnské pobočce dnes ve 20:00 a v pracovní dny je zapni v 7:00.“*

Asistent upraví plánovač se správou napájení po časových slotech.

### Přehled flotily

> *„Která zařízení se neohlásila déle než 24 hodin? Seskup je podle lokality.“*

> *„Které přehrávače mají ještě starý firmware?“*

### Vrácení změny

> *„Vrať poslední změnu v playlistu restaurace.“* (v plánu: historie změn a obnovení)

## Tvorba obsahu

> *„Vytvoř obrazovku s dnešním datem, hodinami a počasím pro Brno, tmavé pozadí, naše logo vlevo nahoře.“*

> *„Přelož všechny texty obrazovky ‚Wellness‘ do angličtiny a zachovej rozložení.“*

> *„Zduplikuj obrazovku ‚Letní nabídka‘ jako ‚Podzimní nabídka‘ a vyměň obrázek pozadí za `podzim.jpg`.“*

**Schvalujete:** každou novou nebo změněnou obrazovku po náhledu.

## Vývojáři a integrátoři

Vše výše běží na Avemeo REST API, které můžete volat i přímo:

| Integrace | Jak |
|---|---|
| **Hotelový PMS → TV** | Hotelová TV Avemeo se integruje s hotelovými systémy při check-inu a check-outu (jméno hosta, pokoj, zprávy); zeptejte se nás na možnosti integrace s vaším PMS. |
| **ERP → ceníky** | Noční úloha, která aktualizuje texty cen na obrazovkách digitálního menu (`/api/screen/widgets/update`). |
| **Monitoring → ticketing** | Dotazování stavů zařízení (`/api/stats/device`, `/api/device`) a založení tiketu, když je zařízení offline déle než N minut. |
| **Marketing → kampaně** | Vytvoření playlistů a plánovačů pro kampaň z vašeho kampaňového nástroje (`/api/playlist/update`, `/api/scheduler/update`). |

Autentizaci a příklady najdete v [přehledu REST API](api-overview.md).

## Související

- [AI konektor (MCP)](mcp-connector.md) · [Přehled REST API](api-overview.md) · [FAQ](faq.md) · [Slovník pojmů](glossary.md)
- Máte zájem o pilot? [avemeo@sortec.sk](mailto:avemeo@sortec.sk)
