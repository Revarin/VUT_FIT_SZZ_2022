# Principy řízení a připojování periferních zařízení
- Otázky: přerušení, programová obsluha, přímý přístup do paměti, sběrnice
- Předmět: INP
- Zdroje:
    - https://wis.fit.vutbr.cz/FIT/st/cfs.php.cs?file=%2Fcourse%2FINP-IT%2Flectures%2Finp2021_15bus_per.pdf

## Řadič periferních zařízení a autonomní provádění periferní operace
Pro práci se všemi periferiemi zařízení se používá součástka zvaná __řadič__. Tato součástka slouží pro komunikaci zařízení s periferií. Údaje putující z periferie nebo do ní překládá do formátu, kterému rozumí sběrnice a periferie. Řídí činnost periferie pomocí _řídících signálů_ a _přerušení_ nebo _programové obsluhy_.

Procesor komunikuje pouze s _registry řadiče_ periferního zařízení. K tomu používá buď instrukce pro práci s paměti nebo speciální instrukce pro ovládání I/O periferie. Řadič periferie většinou mívá tři druhu registrů: _datový registr_ (přes něj se přenášejí data), _řídící registr_ (určuje operaci periferie a její způsob provedení) a _stavový registr_ (stav řadiče a periferie).

Existují dva způsoby připojení periferních zařízení: __mapovaný vstup/výstup__ a __izolovaný vstup/výstup__.
- __Mapovaný V/V__ - Registry řadiče periferie jsou namapovány na určité adresy hlavní paměti. Periferie a paměť tak sdílí stejný adresový prostor. Operace s periferií se provádí stejně jako operace s paměti (instrukce čtení a zápis).
- __Izolovaný V/V__ - Adresový prostor paměti a periferií je oddělen. Registry periferních zařízení mají svůj vlastní adresový prostor. Operace s periferií s provádí pomocí speciálních instrukcí (`IN` a `OUT`).

Průběr provádění periferních operací je následující: Řadič nejdříve zjistí stav perefiere. Pokud je periferie v pořádku, zahájí na ní danou periferní operaci vložením __parametrů operace do registrů__ řadiče periferie. Po dokončení této operace je potřeba aby periferie oznámila řadiči a ten následně procesoru, že operace byla dokončena. K tomu se používá __přerušení__ nebo __programové obsluhy__. Pro zjištění výsledku operace se musí zkontrolovat stav periferie. Jsou dvě fáze zjištění stavu periferie:
1. Nejprve se zkontroluje __stavová slabika__ (status byte), v ní je bit označující výskyt chyby. Pokud je hlášena chyba tak je operace považována za neplatnou a musí se zopakovat.
2. Analýza stavové slabiky procesorem. Pokud vznikla chyba, tak zde se tato chyba analyzuje.
3. Následně se přenesou __slabiky závad__ (sense byte), v níž každý bit značí jeden typ poruchy.

### Přerušení
O dokončení vykonávání periferení operace je nutné informovat procesor. K tomu se využívají __přerušení__. Přerušení je hardwarový (nebo taky i softwarový) signál, který signalizuje nějakou událost, která nastala v periferii. Přerušení nejsou z řadiče periferie posílané přímo do procesoru, ale na __řadič přerušení__, který sdružuje přerušení ze všech perifierií. Tento řadič zajišťuje první kroky obsluhy přerušení a komunikuje s procesorem. Řadič posílá do procesoru __vektor přerušení__, který obsahuje informace o tom, které přerušení bude obslouženo (je to ukazatel do tabulky přerušovacích vektorů - odkazů na programy obsluhy přerušení). Procesor ho následně obslouží a dále pokračuje v běhu. Přerušení můžeme dělit do několika druhů:
- __Vnější přerušení__ - Přerušení generované vnějšími periferiemi přes systémovou sběrnici (např.: zmáčknutí klávesy)
- __Vnitřní přerušení__ - Přerušení vyvolané procesorem nebo periferiemi na čipu procesoru, které slouží jako signalizace pro operační systém (např.: dělení nulou)
- __Softwarové nebo programové přerušení__ - Přerušení vyvolané v kódu programu (např.: ukončení programu)

![Přenos přerušení](/Images/06/prenos_preruseni.png)

Přerušení jsou rozděleny do různých typů podle _významu_, _zdroje_ nebo _priority_ přerušení. Určité typy přerušení je možné v procesoru zamaskovat, tak aby je procesor neobsluhoval. Tomu se říká __maskování přerušení__. Existují __nemaskovatelná přerušení__, které nelze zamaskovat a procesor je musí vždy obsloužit. Obvykle se jedná o systémové přerušení s vysokou prioritou.

Protože v jednom momentě může nastat více různých přerušení je ke každému typu přerušení přiřazena __priorita__. Tyto priority určují, které přerušení bude v daném momentě zpracováno dojde-li k vyvolání více přerušení v jeden okamžik, a zda je možné zpracování tohoto přerušení přerušit jiným, více prioritním přerušením.

### Programová obsluha
Alternativní způsob práce s periferiemi je takzvaná __programová obsluha__ periferií. Procesor musí neustále testovat bit řadiče periferie označující _konec operace_ aby zjistil, zda daná operace proběhla úspěšně. Tento přístup obsluhy periferií je nenáročný ale poměrně neefektivní.

## Přímý přístup do paměti
Přestože je paměť taky periferie, jsou data přenášeny z datového registru řadiče určité periferie do operační paměti přímo (__přes sběrnici__) a ne přes procesor. To je využíváno pro přenos dat mezi diskovou a operační pamětí. Existují dva přístupy:
- __DMA__ (Direct Memory Access) - Řadič DMA řídí přenos dat a umí generovat signály sběrnice, data se ale přez něj __nepřenášejí__.
- __PIO__ (Specializované I/O procesory) - Data jsou přenášena z datového registru periferie přes registr procesoru do registru řadiče paměti a do vyrovnávací paměti

![Přenos dat pomocí DMA](/Images/06/pamet_prenos_dma.png)

## Sběrnice
Sběrnice je hardwarová součástka, která má za účel zajistit přenos dat a řídících povelů mezi dvěma a více elektronickými zařízeními (např.: mezi PCI, ISA, IIC, USB, ...). Sběrnice může být _sériová_ nebo _paralelní_ (okruh __[05]__) a _interní_ nebo _externí_. Sběrnice mají obvykle tři komunikační kanály: __adresa__ (registru nebo paměti), __data__ a __řízení__. Zajišťuje komunikaci mezi procesorem a řadiči periferních zařízení.

Dále můžeme periferie rozlišovat na dva druhy podle jejich fyzické konstrukce:
- __Nesdílená sběrnice__ (dedikovaná sběrnice) - Pro každý signál je samostatný vodič. Slouží pro připojení pouze jednoho zařízení.
- __Sdílená sběrnice__ - Všechny informace se posílají po společné sadě vodičů. Pro rozlišení o jaký typ informace se jedná se používají __identifikační signály__.

![Základní struktura sběrnice](/Images/06/sbernice_struktura.png)

### Synchronní sběrnice
Synchronní sběrnice je sběrnice, jejíž přenost je řízen hodinovým signálem. Obvykle musí mít dodatečný vodič pro přenos hodinového signálu. Operace jsou realizovány od jedné z hran hodinového pulsu. V okamžiku výskytu hrany se vyhodnocuje, jestli se daná operace může provést (zkontroluje se připravenost obou zařízeních). Stav na sběrnici vyhodnocují __všechna__ zařízení.

![Funkce synchronní sběrnice](/Images/06/synchronni_sbernice.png)

### Asynchronní sběrnice
Asynchronní sběrnice je sběrnice, která nepoužívá k řízení synchronizační hodinový signál. Pro synchronizaci zpracování dat mezi vysílačem a příjmačem se musí využívat jiné mechanismy. Generování signálů je pak vázáno na výskyt události předcházející.

![Funkce asynchronní sběrnice](/Images/06/asynchronni_sbernice.png)

### Decentralizované přidělování sběrnice
Na sběrnici neexistuje __arbitr__, který by řídil přidělování sběrnice mezi zařízeními. Rozhodnutí o přidělení sběrnice provedou zařízení _mezi sebou_. Vygenerování žádosti dojde k nastavení signálu __sběrnice obsazena__ a ten je postupně vyhodnocován jednotlivými zařízeními. Jakmile se signál __sběrnice obsazena__ dostane na vstup zařízení, které vygenerovalo tuto žádost, je jeho přenos do následujícího zařízení zablokován a může začít přenos dat.

![Decentralizované přidelování sběrnice](/Images/06/decentralizovana_sbernice.png)

### Centralizované přidělování sběrnice
V počítači existuje __rozhodovací jednotka__ (arbitr) , který přijímá požadavky od všech __adeptů__ (řadiče periferií). Adept generuje žádost o přidělení sběrnice, a arbitr na ni odpovídá. Na základě priorit se centrálně rozhodne o konkrétním zařízení, kterému bude přidělena sběrnice. Před samotným přenosem dat musí být zařízení přidělena sběrnice.

![Centralizované přidělování sběrnice](/Images/06/centalizovana_sbernice.png)
