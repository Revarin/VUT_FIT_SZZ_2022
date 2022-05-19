# Princip činnosti počítače
- Otázky: řetězené zpracování instrukcí, RISC, CISC
- Předmět: INP
- Zdroje:
    - https://wis.fit.vutbr.cz/FIT/st/cfs.php.cs?file=%2Fcourse%2FINP-IT%2Flectures%2Finp2021_02isreg.pdf (RISC, CISC)
    - https://wis.fit.vutbr.cz/FIT/st/cfs.php.cs?file=%2Fcourse%2FINP-IT%2Flectures%2Finp2021_03risc.pdf (zřetězení)

## Zřetězené zpracování instrukcí
Zpracování instrukce lze rozdělit na několik po sobě jdoucích fází, které jsou obvodově zajištěny různými částmi procesoru. Při sériovém zpracováním instrukce se vždy zpracovává pouze jedna instrukce, a tak části procesoru, v nichž instrukce není nic nedělají. To je neefektivní.

Zřetězené zpracování instrukcí (_pipelining_) je provádění různých částí několika instrukcí v jeden okamžik. V jeden hodinový cyklus není prováděna pouze jedna instrukce, ale více instrukcí, z nichž každá je v jiné fázi provádění. Tímto může procesor pracovat efektivně a současně využívat všechny své části. Zpracování instrukce lze obvykle rozdělit do následujících operací:
- Načtení instrukce z paměti (__F__ - Fetch)
- Dekódování instrukce a získání registrů (__D__ - Decode)
- Vykonání instrukce a cyklus výpočtu efektivní adresy (__E__ - Execute)
- Přístup do paměti a cyklus dokončení skoku (__M__ - Memory access)
- Uložení výsledků (__W__ - Write back)

![Zřetězené zpracování instrukcí](/Images/07/pipelining.png)

![Výukový RISC procesor](/Images/07/vyukovy_procesor.png)

### Rizika zřetězeného zpracování
Zřetězení zpracování instrukcí obsahuje jisté rizika. _Sekvenční_ model zpracování předpokládá, že se každá instrukce dokončí před vykonáváním další instrukce. Toto však v případě zřetězeného zpracování nemusí platit. Problémy nastávají především při po sobě jdoucím instrukcím pro zápis a čtení z paměti a skokovým instrukcím.

Existuje několik druhů __konfliktů__ u řetězeného zpracování instrukcí v procesoru, které mohou vést ke zpomalení linky:
- __Strukturální konfliky__ - Obvodová struktura procesoru neumožňuje současné provedení určitých akcí.
    - Čtení dvou hodnot z paměti, _řešení:_ rozdělení paměti na paměť programu a paměť dat.
    - Současné provedení dvou sčítání (procesor s jedním ALU), _řešení:_ přidání dalších výpočetních jednotek.
- __Datové konfiliky__ - Jsou zapotřebí data z předcházející instrukce, která ale ještě není dokončena. Lze rozdělit na několik podkategorií.
    - _RAW_ (Read After Write) - Přečtení hodnoty v kroku 2 dříve, než je do ní uložena hodnota z předchozího kroku 1.
```bsh
ADD R2, R1, R3      // 1. R2 <- R1 + R3
SUB R4, R2, R3      // 2. R4 <- R2 + R3
```
-   - _WAW_ (Write After Write) - Data jsou do R2 zapsána v kroku 2 dříve, než se do R2 uloží hodnota v kroku 1.
```bsh
ADD R2, R4, R7      // 1. R2 <- R4 + R7
SUB R2, R1, R3      // 2. R2 <- R1 + R3
```
-   - _WAR_ (Write After Read) - Hodnota je přepsána v kroku 2 dříve, než je načtena v kroku 1.
```bsh
ADD R4, R1, R5      // 1. R4 <- R1 + R5
SUB R5, R1, R2      // 2. R5 <- R1 + R2
```
-   - Řešení pomocí takzvaného __Bypassing__ - poskytnutí mezivýsledků dříve, než je zapsán do registru. To je umožněno přidáním speciálních datových cest.
- __Řídicí konflikty__ - Skoková instrukce mění obsah `PC`, nebo jiné. Neví se kam skočit, adresa je známa až na konci zpracování instrukce. To lze řešit několika způsoby:
    - _Zpožděním skoku_ - Za skok se vloží jiné užitečné instrukce (program se musí přeskládat).
    - _Vložení NOP_ - Pokud neexistuje užitečná instrukce, co vložit za skok, tak se vloží instrukce `NOP` (No Operation).
    - _Predikce skoku_ - Rozpracuje se pouze předpokládaný skok na základě __prediktoru skoku__.
    - _Začít rozpracovávat obě možnosti pokračování skoku_ - Z nich se pak provede ta validní

![Bypassing](/Images/07/bypassing.png)

### Predikce skoků
Skokové instrukce dynamicky mění pořadí instrukcí, které se mají vykonávat. Protože pipelining vykonává již dopředu následující instrukce, v případě skoku je potřeba tyto instrukce číst z jiné části. V nepodmíněných skocích toto nezpůsobuje zásadní problém, ale v případě podmíněných skocích musí procesor provádět _predikci_ (jednotka predikce skoku), zda bude skok proveden nebo ne. Existuje několik způsobý predikce skoku:
- __Statická predikce__ - Kompilátor nastaví bit predikce.
- __Dynamická predicke__ - Predikce pomocí specializovaného hardwaru.
- __Predikce podle předchozího skoku__ - Historie skoků lze popsat binárním řetězcem několika bitů. V nejjednodušším případě se používá __jednobitový prediktor__, který ukládá pouze jeden bit historie. Tento prediktor předpovídá stejné chování skoku i v příštím průchodu (stav 0 - skok minule neproveden a tak se neskočí, stav 1 - skok minule proveden a tak se skočí). Pokud je předpověď chybná tak se přejde do druhého stavu. Ukončí se špatná rozpracovaná větev programu a aktualizuje se BTB, což stojí několik taktů procesoru.

U všech skoků se používá pro zrychlení zjištění cílové adresy cache s cílovými adresami __BTB__ (Branch Target Buffer).

### Další poznatky k zřetězenému zpracování instrukcí
Čím větší je počet sekcí, tím větší počet úloh může procesor provádět současně. Frekvence výsledku na výstupu tak roste s počtem sekcí. Na každou sekci musí navazovat __registr__ v němž je výsledek sekce zaznamenán. To zvyšuje cenu a spotřebu procesoru a taky může zanést další zpoždění.

### Architektury proudového zpracování
- __Skalární architektura__ - Architektura s jednou frontou
- __Superskalární architektura__ - Front instrukcí je více, což umožňuje zpracovat v jednom taktu více instrukcí. Vyskytují se problémy s koordinací činností v jednotlivých frontách (problém párování instrukcí, párovací pravidla).
- __Hyperskalární architektura__ - Navýšení počtu sekcí v jedné frontě (hranice deseti sekcí, ale existují architektury i s více sekcemi).

## RISC
_Reduced Instruction Set Processors_ (procesory s redukovanou instrukční sadou) jsou procesory, jejichž instrukční sada je __omezená__. Tyto instrukční sady mají mále jednoduchých instrukcí, zato ale mají tyto instrukce __stejnou velikost__ a také stejnou __dobu vykonávání__ (snaha __CPI__ (cycles per instruction) = 1). To je pro procesory velmi výhodné, protože mohou jednoduše využívat zřetězení instrukcí. Procesory tohoto typu mývají více víceúčelových registrů, poněvadž jsou značně omezeny instrukce přístupu do paměti (obvykle pouze instrukce `READ` a `WRITE`).

## CISC
_Complex Instruction Set Processors_ (procesory s komplexní instrukční sadou) jsou procesory, jejichž instrukční sada je __rozšířená__. Obsahují velké množství instrukcí, z nichž jsou mnohé specializované na konkrétní použití. Instrukce mají rozdílnou velikost a také různé doby vykonávání. Oproti procesorům RISC je možné ušetřit některé instrukce použitím jedné složitější specializované instrukce. CISC procesory obsahují relativně málo registrů, na druhou stranu ale umí pracovat přímo s pamětí.

Složitější instrukce se obvykle skládají z několika __mikroinstrukcí__ (jsou to vlastně __mikroprogramy__). Tyto mikroprogramy jsou uloženy v _paměti mikroprogramů_ a při vykonávání instrukce se vyvolají. Řízení procesoru mikroprogramem má několik výhod jako je možnost _aktualizace_ mikroprogramu, možnost _tvorbu instrukcí na míru_ a _extensivní vývoj_. Vyvolání mikroprogramu má ale určitou režii. U moderních PC jsou jednoduché instrukce realizovány obvodově a složité instrukce mikroprogramově.
