# Technologie FPGA
- Otázky: vnitřní struktura, LUT, kroky návrhu aplikací využívající FPGA a základy syntetizovatelného popisu hardware, strukturní a behaviorální popis obvodů
- Předmět: INC
- Zdroje:
    - https://wis.fit.vutbr.cz/FIT/st/cfs.php.cs?file=%2Fcourse%2FINC-IT%2Flectures%2F08-technologie.pdf
    - https://wis.fit.vutbr.cz/FIT/st/cfs.php.cs?file=%2Fcourse%2FINC-IT%2Flectures%2F05_navrh_obvodu.pdf
    - https://wis.fit.vutbr.cz/FIT/st/cfs.php.cs?file=%2Fcourse%2FINC-IT%2Flectures%2F06-navrh-obvodu-a-jazyk-vhdl.pdf

## Programovatelný logický obvod
Obvodová implementace algoritmů je obvykle výrazně rychlejší než jeho programová alternativa spuštěná v procesoru. Je v ní možné využít vyššího stupně __paralelismu__, aplikačně specifických HW komponent a speciálních způsobů kódování. Díky tomu je výsledná obvodová realizace algoritmu rychlejší, zabírá méně místa na čipu než procesor a má obvykle i menší spotřeba. Takovéto specifické obvody jsou ale náročné na návrh a taky jsou dražší než obecně použitelné procesy. Obvodová realizace bývá méně flexibilní (jednoúčelová) a nelze ji jednoduše modifikovat. Jako kompromis mezi obvodovou implementací a programovou implementací lze využí __programovatelné logické obvody__.

Programovatelný logický obvod (PLD) mají předdefinovanou strukturu, kterou lze různým způsobem programovat pro realizaci logických obvodů. Mohou též obsahovat klopné obvody, třístavové budiče, paměti a další prvky. Existují různé technologie programovatelných logických obvodů, jako například ROM, PLA, PAL, GAL, CPLD, __FPGA__.

Programování těchto obvodů lte provést různými způsoby podle použité technologie PLD. Programování se provádí pomocí programátoru nebo přímo v zařízení pomocí specializovaného rozhraní.
- Přepálením _pojistky_ (PAL, PLA)
- Naprogramováním paměťových buněk PROM (GAL, CPLD)
- Naprogramování paměti SRAM (FPGA)

Programovatelné logické obvody umožňují uživately samostatně realizovat složité logické obvody a dále je modifikovat. Dnešní kapacity PLD obvodů jsou velmi velké (miliony členů NAND).

## Popis obvodů
Existují dva způsoby popisu logických obvodů: __Strukturní popis__ a __behaviorální popis__. V praxi se tyto dva způsoby popisu často kombinují.

### Strukturní popip
Strukturní popisu popisuje požadovanou __strukturu__ logického obvodu. Architektura obvodu je sloužena pouze z instancí komponent a jejich vzájemné propojení vodiči. Komponenty se mohou rovněž skládat z podkomponent (hierarchie komponent). Strukturní popis tak vlastně popisuje __z čeho je__ daný obvod __složen__. Je blízký finální obvodové realizaci a návrhář má do jisté míry pod kontrolou proces syntézy a časování.

### Behaviorální popis
Behaviorální popis popisuje požadované __chování__ logického obvodu. Architektura obvodu je složena z jednoho nebo více __procesů__. Proces je program (algoritmus), který určuje, jak se mají nastavit výstupní signály komponent v závislosti na změnách vstupních signálů. Používáme konstrukce běžné v _programovacích jazycích_. Při tomto popisu neuvažujeme obvodové detaily, tvorbu zapojení obvodu necháváme na proces syntézy. Syntéza však nemusí být úspěšná, protože pro některé programové konstrukce neexistuje obvodový ekvivalent. Z behaviorálního popisu tak nemusí být zřejmá hardwarová realizace.

## Jazyk VHDL
Jazyk VHDL je aplikačně specifický programovací jazyk sloužící pro návrh logických obvodů. VHDL popisuje číslicová zařízení a jednotlivé části zařízení pomocí __komponent__, které se popisují pomocí __entit__ a __architektury__.

![VHDL entita a architektura](/Images/10/vhdl_entita_architektura.png)

### Entita
Entita popisuje rozhraní mezi komponentou a okolím. Rozhraní komponenty se skládá ze _signálů rozhraní_ a _generických parametrů_. Signály rozhraní mohou mít různý směr podle jejich módu (`IN`, `OUT`, `INOUT`).

__Porty entity__ jsou speciální signály, se kterými lze provádět omezené operace čtení a zápisu. Kromě své funkce rozhraní entity mohou být používány jako lokální signály v rámci příslušné architektury:
- `In` - vstupní port
- `Out` - výstupní port
- `Inout` - vstupně výstupní port (používá se například pro realizaci sběrnice)
- `Buffer` - výstupní port, jehož obsah je možné číst
- `Linkage` - směr toku dat neznámy

![Příklad VHDL entity](/Images/10/vhdl_entita.png)

### Architektura
Architektura definuje chování nebo strukturu komponenty. Architektura je vždy svázána s nějakou entitou, která definuje rozhraní komponenty s okolím. Každá komponenta může být popsána na úrovni __struktury__, __chování__ nebo __dataflow__. Různé způsoby popisu je možné kombinovat.

![Příklad VHDL architektury](/Images/10/vhdl_architektura.png)

Součástí sekce paralelních příkazů mohou být instance komponent nebo procesy vzájemně propojené signály podle způsobu popisu obvodu:
- __Behaviorální popis__ - Architektura je složena z jednoho nebo více procesů.
- __Strukturální popis__ - Architektura obsahuje pouze instance komponent.

## FPGA
FPGA (Field Programmable Gate Array) je matice __konfigurovatelných logických obvodů__ (CLB). Konfigurace této matice je uložena v paměti __SRAM__, po každém připojení napájecího napětí je třeba konfigurační informaci zkopírovat do FPGA z externí paměti. FPGA představuje kompromis mezi výkonností HW a flexibilitou SW. Využívá s v automobilovým průmyslu, počítačových sítích, letectví...

### Konfigurovatelné logické bloky
Konfigurovatelný logický blok (CLB) je malá SRAM sloužící pro implementaci logických funkcí, multiplexorů, registrů, atd. Obsahuje obvody pro řízení hodinového signálu (DMC, PLL, apod,) a vestavěné komponenty jako jsou blokové paměti, násobičky a další. Hlavní část CLB tvoří __funkční generátory__ (FG) umožňující využít dané hradlo jako _vyhledávací tabulku_, _paměť_ nebo _posuvný regist_.

__Vyhledávací tabulka__ (LUT, Look-Up Table) je základní logické hradlo s N-bitovým vstupem a 1-bitovým výstupem. Realizuje libovolnou binární funkci N proměnných.

__Paměťový prvek__ (RAM) je paměť o velikosti \(2^N\) bitů. Umožňuje _asynchronní čtení_ (není  potřeba čekat na hodinový signál) a _synchronní zápis_ (data jsou zapsána při vzestupné hraně hodinového signálu). Je vhodná pro konstrukci menších pamětí. Další alternativy paměťového provku _RAM_ jsou _RAM16_ pro tvorbu větších paměťových celků a RAMD pro dvou-portovou paměť.

__Posuvný registr__ (SRL) je malá paměť umožňující synchronní zápis a asynchronní čtení ze zadané pozice. Při zápisu se veškerá data v registru posunou o jednu pozici. Je vhodný pro konstrukci zpožďovacích obvodů, generátorů náhodných čísel a čítačů libovolných sekvencí.

Pro konstrukci složitejších funkcí jsou jednotlivé funkční generátory spojovány skrze pomocné multiplexory MUXFx. Tyto propojení definuje __carry logika__ (konstrukce sčítaček, čítačů, komparátorů, atd.).

### Vestavěné bloky
Vestavěné bloky realizují v FPGA často používané funkce a šetří tak množství spotřebovaných zdrojů. Mohou to být: paměti, procesory, násobičky, DSP bloky (obsahuje násobičku, sčítačku, multiplexor a interní sběrnice) nebo ethernet bloky (zpracování ethernetu).

### Zpracování hodinového signálu
Hodinový signál je do FPGA přiváděn skrze __GCLK piny__ a rozváděn rovnoměrně po celém čipu pomocí speciálních hodinových rozvodů. Kromě _globálních rozvodů_ jsou v čipech umístěny i _regionální rozvody_ pro komunikaci s externími komponentami. Obvody pro úpravu hodinového signálu (redukce zpoždění, frekvenční syntéza, fázový posun...) jsou odděleny od běžných vodiců pro přenos dat.

### Input/Output block (IOB)
Každý pin FPGA může být konfigurován jako vstup, výstup nebo obojí. Jsou podporovány jednotlivé vodiče i deferenciální páry (pouze u sousedních pinů). Je podporováno velké množství standardů, aby bylo možné k FPGA připojit různé externí součástky.

### Propojovací síť
Jednotlivé elementy FPGA čipu jsou propojeny skrze rozsáhlou konfigurovatelnou __propojovací síť__. Síť je tvořena horizontálními a vertikálními vodiči. CLB bloky jsou na tuto síť připojeny skrze _C-boxy_ (Connection). V místě průsečíku horizontálních a vertikálních vodiců je umístěn _S-box_ (Switch).

![Propojovací síť](/Images/10/propojovaci_sit.png)

- __C-boxy__ připojují vstupy a výstupy CLB k horizontální a vertikálním vodičům.
- __S-boxy__ vodiče jsou rozděleny na segmenty. Parametrs FS udává počet segmentů, do kterých lze vodič vstupující do S-boxu propojit.

### Konfigurace
Konfigurace je obvykle na FPGA čipu uložena v paměti SRAM a po vypnutí napájení se ztrácí. Některé typy konfigurovatelných obvodů (CPLD) používají paměť typu FLASH s omezeným počtem programování. Konfigurace FPGA specifikuje nastavení výše zmíněných komponent FPGA. Existují různé způsoby konfigurace:
- Režim __master__ - FPGA čip si po zapnutí sám nahraje konfiguraci z externí paměti.
- Režim __slavel__ - FPGA čip po zapnutí čeka než mu někdo nahraje konfiguraci z externí paměti.
- Skrze sériové rozhraní (SPI)
- Skrze paralelní rozhraní (BPI)

FPGA také podporuje _částečnou rekonfiguraci_ za běhu. Rozsáhlou aplikaci lze rozdělit na několik částí, které se postupně za běhu nahrávají do FPGA. K tomu slouží komponenta ICAP. Díky tomu je možné uspořit nějaké zdroje.

## Návrh aplikací FPGA
Při návrhu aplikací využívajících FPGA se nejčastěji používá přístup návrhu systému __shora dolů__ (top-down). Začíná se z celkového popisu problému a končí návrhem s úplnou mírou detailů. Na každé úrovni je potřeba specifikovat správnou funkci navrhovaného systému. Je to vlastně __dekompozice__.

> __Dekompozice__ - rozklad složitého problému na snadno řešitelné části.

Různé druhy obvodů mají různé metodologie jejich návrhu:
- __Kombinační obvody__ mají své chování popsáno pomocí pravdivostní tabulky nebo logických výrazů. Obvodová realizace je na úrovni zapojení logických prvků.
- __Sekvenční obvody__ mají své chování popsáno pomocí Mealyho/Moorova automatu. Obvodová realizace využívá klopných obvodů pro uložení aktuálního stavu v paměti a kombinační logickou síť (logické prvky) pro výpočet následujícího stavu a výstupní funkce.
- __Návrh obvodu na úrovni RT__ má své chování popsáno na úrovni stavového zpracování dat. Obvodová realizace využívá kombinační a sekvenční obvody nebo moduly.

Návrh je obvykle rozdělen do několika kroků:
1. Popis obvodu na úrovni základního stavového automatu - Automat popisuje základní stavy obvodu, ale neřeší konkrétní nastavení řídicích, vstupních nebo výstupních signálů.
2. Vytvoření datové cesty (datapath) - Datová cesta provádí manipulaci s daty a to na základě řízení z obecného automatu.
3. Identifikace signálů pro řízení datové cesty - Definice signálů, které jsou potřeba pro napojení datové cesty na řídící blok.
4. Návrh řídícího automatu - Převedení obecného automatu na Mealyho nebo Moorův automat, který řídí datovou cestu.

## Logická syntéza
Logická syntéza je proces automatické transformace mezi různými úrovněmi popisu. Je to transformace na jemnější popis s cílem vylepšit parametry zadané uživatelem (rychlost, spotřeba, rozměry). Vstup automatické syntézy je popis obvodu v HDL, knihovna prvků cílové technologie a _constraints_ (např.: spotřeba, velikost...). Výstupem je optimalizovaný _NetList_ na úrovni prvků cílové technologie. Skládá se ze dvou kroků:
1. __Behaviorální syntéza__ - Z behaviorálního popisu algoritmu je vytvořena reprezentace na úrovni struktur logických obvodů.
2. __Logická syntéza__ - Z HDL popisu na úrovni RT (meziregistrových přenosů) je vytvořen _NetList_ prvků cílové technologie. Tento proces je závislý na cílové technologii.

Při logické syntéze se rozpoznávají prvky cílové technologie a mapují se do FPGA. Výsledkem procesu je konfigurační soubor pro FPGS.

![Logická syntéza](/Images/10/logicka_synteza.png)
