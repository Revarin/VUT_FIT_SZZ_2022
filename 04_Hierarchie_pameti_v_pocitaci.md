# Hierarchie paměti v počítači
- Otázky: vlastnosti paměti, typy a principy pamětí, principy lokality, organizace rychlé vyrovnávací paměti, virtuální paměť
- Předmět: INP
- Zdroj: http://szz.g6.cz/doku.php?id=temata:04-hierarchie_pameti:main

## Paměti
Paměti slouží pro uchovávání dat. Existují různé druhy pamětí s různými vlastnostmi jako:
- Kapacita
- Rychlost
    - Přístupová doba - doba od zahájení čtení po získání obsahu paměťového místa
    - Doba cyklu - doba od zahájení čtení/zápisu do skončení operace, kdy je možno spustit další operaci
    - Přenosová rychlost - data/čas
- Chybovost a poruchovost
- Stálost obsahu
    - Volatilní - potřebuje k uchování informace napájecí napětí
    - Nevolatilní - nepotřebuje k uchování informací napájecí napětí
- Doba uchování informace
    - Statická (SRAM) - uchovaná informace se udržuje dlouhodobě
    - Dynamická (DRAM) - uchovanou informaci je potřeba neustále obnovovat
- Přístup k datům
    - S libovolným přístupem (RAM - Random Access Memory)
    - Se sériovým přístupem (SAM - Serial Access Memory)
    - Se smíšeným přístupem
- Výběr z paměti
    - Adresový
    - Asociativní (klíče)
- Fyzikální princip pamětí - polovodičové / magnetické / optické / molekulární
- Přístupnost obsahu
    - RWM - Read/Write Memory
    - ROM - Read Only Memory
    - PROM - Programable ROM
    - EPROM - Erasable Programable ROM
    - EEPROM - Electricaly Erasable Programable ROM
- Poměr cena/bit

Obecně platí, že čím větší kapacita, tím menší je cena/bit a přenosová rychlost. A protože větší paměti jsou obvykle mnohem pomalejší než procesor je nutné využívat __paměťovou hierarchii__. Čím blíže je paměť k procesoru, tím menší ale rychlejší je. Obecně můžeme paměť rozdělit na následující úrovně:
- Registry a cache v procesoru
- Cache (SRAM)
- Hlavní pamět (DRAM)
- Sekundární pamět (disk)
- Terciální paměť (magnetické pásky)

![Hierarchie pamětí](./Images/04/hierarche_pameti.png)

### Jednotlivé typy pamětí
TODO

## Principy lokality
Principy lokality jsou základní předpoklady, díky nimž může fungovat paměťová hierarchie. Jsou dva principy lokality: časová lokalita a prostorová lokalita.

__Časová lokalita__ nám říká, že při využití paměťového bloku je velká šance, že ho budeme brzo používat znovu.

__Prostorová lokalita__ nám říká, že při využití paměťového bloku je velká šance, že brzo budeme potřebovat i jeho sousedy v paměťovém prostoru.

## Rychlá vyrovnávací paměť (Static RAM)
RVP je rozdělena do bloků o konstatní velikosti, v hlavní paměti jsou bloky stejné velikosti, ale je jich mnohem více. Proto v RVP mohou být uloženy jen některé bloky. Při nalezení požadovaného bloku nastavá _cache hit_, pokud není nalezen nastává _cache miss_. Poměr _cache hit_ a _cache miss_ se nazývá _hit rate_. V praci se snažíme _hit rate > 95%_

Existuje několik způsobů organizace RVP podle typu mapování dat z vyšších vrstev paměti.

### RVP s přímým mapováním
RVP má rámce popsané adresami, které jsou menší než adresy v hlavní paměti. Adresy polohy bloku se určí podle nejnižších _x_ bitů. Protože, ale v hlavní paměti je více bloků se stejnou RVP adresou je nutné uchovávat informaci, jaký blok je v RVP přítomen - __adresový příznak__ (tag), což jsou zbývající horní bity adresy. Navíc se používá i __příznak platnosti__ dat (valid bit).

![RVP s přímým mapováním](./Images/04/rvp_s_primym_mapovanim.png)

### RVP s plně asociativním mapováním
RVP umožňuje jakýkoliv blok z hlavní paměti uložit na jakoukoliv adresu v RVP. Adresový příznak bloku obsahuje celou adresu paměťového bloku. Při vyhledávání paměťového bloku je ale nutné zkontrolovat všechny bloky v RVP.

### RVP s skupinovým asociativním mapováním
Představuje kompromis mezi přímým mapováním a plně asociativním mapováním. RVP se rozdělí do _skupin_, které mají stejný počet bloků. Takto je možné současně uložit více položek se stejnou RVP adresou. Podle počtu skupin má RVP určitý __stupeň asociativity__. Stejně jako RVP s přímým mapováním se ukládá adresový příznak a příznak platnosti.

![RVP se skupinovým asociativním mapováním](./Images/04/rvp_s_skupinovym_mapovanim.png)

Při skupinovám asociativním mapováním se vyskytuje problém výběru oběti. Používají se různé algoritmy:
- LRU - Least Recently Used
- MFU - Most Frequently Used
- FIFO - First-In, First-Out
- RAND - Random

### Koherence dat
Pokud se změní data v RVP, tak bloky na vyšších úrovní ztratí platnost a nesmí se použít. Vzníká datová nekoherence. Pro udržování koherence dat ve všech kopií bloků se používají různé strategie:
- Přímý zápis (write-through) - Okamžitě se zapisuje i do bloku v hlavní paměti. Snadná realizace, ale pomalé.
- Zápis s mezipamětí (write buffer) - Opravné zápisy se odloží, dokud nedostaneme přístup k hlavní paměti, nedokončí se aktuální disková operace
- Zpětný zápis (write back) - Opravný zápis se provede až když je blok vyjmut z RVP. Je možné využít příznak změny (dirty bit), který označuje zda byly data změněny.

## Virtuální paměť
Diskové jednotky mají podobné problémy jako hlavní paměť. Jsou příliš pomalé na to, aby s nimi pracoval přímo procesor. Proto se jako jejich vyrovnávací paměť využívá __virtuální paměť__. Virtuální paměť používáme protože:
- Chceme udělat efektivní sdílení paměti M pro mnoho programů.
- Chceme odstranit omezení fyzikální velikosti paměti M

Virtuální paměť vychází z poznatku, že pouze malá část program je současně aktivních. Využívá dva adresové prostory: fyzický adresový prostor (HW) a logický adresový prostor (OS).
