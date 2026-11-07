# Príklady použitia: Avemeo s AI asistentom

> 🇬🇧 English version: [../use-cases.md](../use-cases.md) · 🇨🇿 Česká verze: [../cs/use-cases.md](../cs/use-cases.md) · ⬅ Späť na [README](../../README.sk.md)

Čo budú zákazníci môcť robiť s Avemeo a AI asistentom (Claude, ChatGPT, Gemini a ďalší MCP klienti), keď bude dostupný [AI konektor](mcp-connector.md). Každý príklad ukazuje, čo poviete, čo asistent urobí v Avemeo a čo schvaľujete. Rovnaké operácie majú vývojári k dispozícii cez [REST API](api-overview.md).

**Obsah:** [Retail](#retail-predajne-a-siete) · [Hotely](#hotely-a-ubytovanie) · [Firmy, priestory a podujatia](#firmy-priestory-a-podujatia) · [Prevádzka a monitoring](#prevádzka-a-monitoring) · [Tvorba obsahu](#tvorba-obsahu) · [Vývojári](#vývojári-a-integrátori)

## Retail: predajne a siete

### Proof of play a prehrávače offline

> *„Ktoré prehrávače v predajniach boli minulý týždeň počas otváracích hodín offline? Zoraď podľa stratených hodín.“*

Asistent načíta stavy každého prehrávača po minútach, porovná ich s otváracími hodinami predajne a vráti tabuľku po predajniach so stratenými hodinami a časmi výpadkov. Typický výsledok: väčšina prehrávačov hrá 98 – 100 % času; pár predajní má opakované výpadky, ktoré ukazujú skôr na miestnu sieť než na prehrávač.

> *„Reštartuj audio prehrávač v predajni na Hlavnej a daj vedieť, keď zase hrá.“*

**Schvaľujete:** reštart jedného pomenovaného zariadenia.

### Kampane naprieč predajňami

> *„Daj od pondelka nový jesenný spot do všetkých audio playlistov predajní, každých 15 minút, do konca novembra.“*

Asistent nájde playlisty predajní, pripraví jednu zmenu s náhľadom pred/po pre každý playlist a po jednom schválení ju vykoná.

> *„Nahraď letný cenník na všetkých digitálnych menu novým z knižnice médií.“*

**Schvaľujete:** zoznam playlistov alebo obrazoviek, ktoré sa zmenia.

### Regionálny a sezónny obsah

> *„Púšťaj vianočný playlist vo všetkých predajniach od 1. decembra, ale v bratislavských začni o týždeň skôr.“*

Asistent vytvorí alebo upraví plánovače s obdobiami podľa skupín predajní.

## Hotely a ubytovanie

### Interaktívne hotelové TV menu

> *„Vytvor hotelové TV menu z kruhovej šablóny s TV, rádiom, reštauráciou, wellness, výletmi a počasím, po slovensky a anglicky.“*

Asistent vytvorí obrazovku zo šablóny Avemeo, doplní texty, obrázky a preklady a ukáže náhľad každej úrovne menu.

> *„Zmeň v menu čas raňajok na 7:00 – 10:30.“*

> *„Pridaj nemeckú verziu menu a prepínač jazyka.“*

**Schvaľujete:** novú alebo zmenenú obrazovku po kontrole náhľadu.

### Komunikácia s hosťami

> *„Čo práve hrá v izbe 204?“*

> *„Daj uvítaciu správu pre konferenčnú skupinu na všetky izby na 3. poschodí od piatka do nedele.“*

### Podujatia a konferencie

> *„Na zajtrajšiu konferenciu daj od 7:30 program na obrazovky v lobby a názvy sál na obrazovky pri dverách.“*

## Firmy, priestory a podujatia

### Recepcia a lobby

> *„Vytvor playlist pre recepciu z piatich prezentačných obrazoviek po 8 sekúnd a púšťaj ho v pracovné dni 8:00 – 17:00.“*

> *„Čo je práve na obrazovke v lobby?“*

### Navigácia a vyvolávací systém

> *„Premenuj zasadačku ‚Tatry‘ na ‚Fatra‘ na všetkých navigačných obrazovkách.“*

### Jedálne a digitálne menu

> *„Nahraj menu jedálne na tento týždeň na obrazovky v kantíne a v sobotu prepni na víkendové menu.“*

## Prevádzka a monitoring

### Denný report

> *„Každé ráno mi pošli zoznam zariadení, ktoré boli včera offline.“* (cez naplánované úlohy v AI asistentovi)

### Správa napájania

> *„Vypni všetky obrazovky v žilinskej pobočke dnes o 20:00 a v pracovné dni ich zapni o 7:00.“*

Asistent upraví plánovač so správou napájania po časových slotoch.

### Prehľad flotily

> *„Ktoré zariadenia sa neohlásili viac ako 24 hodín? Zoskup ich podľa lokality.“*

> *„Ktoré prehrávače majú ešte starý firmvér?“*

### Vrátenie zmeny

> *„Vráť poslednú zmenu v playlisti reštaurácie.“* (v pláne: história zmien a obnovenie)

## Tvorba obsahu

> *„Vytvor obrazovku s dnešným dátumom, hodinami a počasím pre Poprad, tmavé pozadie, naše logo vľavo hore.“*

> *„Prelož všetky texty obrazovky ‚Wellness‘ do angličtiny a zachovaj rozloženie.“*

> *„Zduplikuj obrazovku ‚Letná ponuka‘ ako ‚Jesenná ponuka‘ a vymeň obrázok pozadia za `jesen.jpg`.“*

**Schvaľujete:** každú novú alebo zmenenú obrazovku po náhľade.

## Vývojári a integrátori

Všetko vyššie beží na Avemeo REST API, ktoré môžete volať aj priamo:

| Integrácia | Ako |
|---|---|
| **Hotelový PMS → TV** | Hotelová TV Avemeo sa integruje s hotelovými systémami pri check-ine a check-oute (meno hosťa, izba, správy); opýtajte sa nás na možnosti integrácie s vaším PMS. |
| **ERP → cenníky** | Nočná úloha, ktorá aktualizuje texty cien na obrazovkách digitálneho menu (`/api/screen/widgets/update`). |
| **Monitoring → ticketing** | Dopytovanie stavov zariadení (`/api/stats/device`, `/api/device`) a založenie tiketu, keď je zariadenie offline dlhšie než N minút. |
| **Marketing → kampane** | Vytvorenie playlistov a plánovačov pre kampaň z vášho kampaňového nástroja (`/api/playlist/update`, `/api/scheduler/update`). |

Autentifikáciu a príklady nájdete v [prehľade REST API](api-overview.md).

## Súvisiace

- [AI konektor (MCP)](mcp-connector.md) · [Prehľad REST API](api-overview.md) · [FAQ](faq.md) · [Slovník pojmov](glossary.md)
- Máte záujem o pilot? [avemeo@sortec.sk](mailto:avemeo@sortec.sk)
