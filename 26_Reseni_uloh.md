# Řešení úloh
- Otázky: Prohledávání stavového prostoru, rozklad na podúlohy, metoda hraní her
- Předmět: (původně okruh 24)
- Zdroje:
    - https://wis.fit.vutbr.cz/FIT/st/cfs.php.cs?file=%2Fcourse%2FIZU-IT%2Flectures%2F2122izu_02.pdf (prohledávání stavového prostoru)
    - https://wis.fit.vutbr.cz/FIT/st/cfs.php.cs?file=%2Fcourse%2FIZU-IT%2Flectures%2F2122izu_03.pdf (rozklad na podproblémy)
    - https://wis.fit.vutbr.cz/FIT/st/cfs.php.cs?file=%2Fcourse%2FIZU-IT%2Flectures%2F2122IZU_05.pdf (hraní her)

## Stavový prostor
> Stavový prostor je uspořádaná dvojice \((S, O)\), kde:
> - \(S\) je množina stavů úlohy \(S = \{S_i\}\).
> - \(O\) je množina operátorů \(O = \{O_j\}\).

Stavový prostor si můžeme představit jako graf/strom, kde uzly představují jednotlivé stavy úlohy a hrany představují přechody mezi stavy způsobené definovanými operátory. Cesta z počátečního stavu do konečného stavu je pak potenciálním řešením úlohy.

> Úloha je uspořádaná dvojice \((S_0, G)\), kde:
> - \(S_0\) je počáteční stav.
> - \(G\) je množina všech koncových stavů kdy \(G \subseteq S\).

Úloha ve stavovým prostoru vlastně zadává počáteční stav, z něhož se máme dostat do jednoho z koncových stavů. Pro _řešení úlohy_ - nalezení cesty z počátečního stavu do koncového - se používají __prohledávací metody__. Tyto metody jsou hodnoceny určitými kritériemi:
- __Úplnost__ - Metoda je úplná, pokud najde řešení vždy, když daná úloha řešení má.
- __Optimálnost__ - Metoda je optimální, pokud jí nalezené řešení bude vždy nejefektivnější (optimální).
- __Paměťová__ a __časová__ složitost

Existují různé druhy metod prohledávání stavových prostorů:
- __Neinformované__ (slepé) metody - Metody, které nevidí do budoucnosti, nemají žádné informace o cílovém stavu. Pamatují si stavy, které už prošli. Jsou vhodné pro úlohy, o kterých nemáme žádné informace.
    - BFS, DFS, DLS, IDS, BS, UCS, ...
- __Informované__ metody - Metody, které mají k dispozici nějakou informaci o cílovém stavu. Mají prostředky jak aktuální stavy prohledávání zhodnotit z hlediska cílového stavu.
    - BestFS, GS, A*, Hill Climbing
- __Metody lokálního prohledávání__ - Metody, které místo systematického prohledávání stavového prostoru prohledávají pouze okolí aktuálního stavu. Jsou vhodné pro řešení optimalizačních problémů.

### Terminologie
- Uzel \(A\) je __uzel kořenový__ a označuje počáteční stav \(s_0\).
- Uzly \(I,L,M,...,Z\) jsou __uzly listové__.
    - Uzel \(L\) označuje cílový stav \(s_G\).
- Uzly \(A,D,J\) jsou __předchůdci__ uzlu \(V\).
    - Uzel \(C\) je __bezprostředním předchůdcem__ uzlu \(H\).
- Uzly \(H,I,S,T,U\) jsou __následníci__ uzlu \(C\).
    - Uzel \(K\) je __bezprostředním následníkem__ uzlu \(D\).
- Uzel \(A\) má __hloubku__ 0, uzly \(B,C,D\) mají hloubku 1 atd.

- __Expanzí__ uzlu se rozumí určení všech jeho bezprostředních následníků.
- __Generací__ uzlu se nazývá proces vytvoření uzlu.
- __Ohodnocení__ uzlu je dáno součtem cen přechodů z kořenového uzlu do tohoto uzlu.

![Graf stavového prostoru](/Images/26/graf_stavoveho_prostoru.png)

## Neinformované metody prohledávání stavového prostoru
![Neinformované metody](/Images/26/neinformovane_metody.png)

### Metoda slepého prohledávání do šířky
Metoda slepého prohledávání do šířky (BFS) je metoda prohledávání stavového prostoru. Je-li počet bezprostředních následníků každého uzlu konečný, pak je metoda BFS __úplná__ a __optimální__.
- __Časová náročnost:__ Exponenciální
- __Paměťová náročnost:__ Exponenciální \(O(b^{d+1})\)
    - \(b\) je takzvaný faktor dělení - průměrný počet bezprostředních následníků každého uzlu.
    - \(d\) je hloubka nejlepšího řešení (řešení nacházející se v nejmenší hloubce).

Algoritmus BFS s uvažováním __seznamu__ `CLOSED` je následující:
1. Sestrojí se dva prázdné seznamy, __frontu__ `OPEN` (bude obsahovat všechny uzly určené k expanzi) a `CLOSED` (bude obsahovat seznam expandovaných uzlů). Do fronty `OPEN` se umístí počáteční uzel.
2. Je-li fronta `OPEN` prázdná, pak úloha nemá řešení a prohledávání se tak ukončí jako _neúspěšné_. Jinak se pokračuje.
3. Vybere se z čela fronty `OPEN` první uzel a umístí se do seznamu `CLOSED`.
4. Je-li vybraný uzel uzlem cílovým, prohledávání se ukončí jako _úspěšné_ a vrátí se cesta od kořenového uzlu k cílovému uzlu (posloupnost stavů). Jinak se pokračuje.
5. Vybraný uzel se _expanduje_ a jeho bezprostřední následníci, kteří nejsou ani ve frontě `OPEN` ani v seznamu `CLOSED` se umístí do fronty `OPEN`. Následně se vrací do bodu 2.

### Metoda stejných cen
Metoda stejných cen (UCS) je podobná metodě BFS, uvažuje však skutečné _ceny přechodů_ a skutečné ceny cest (jsou dány součtem cen příslušných přechodů). Pro expanzi se pak vybírá ze seznamu `OPEN` uzel s nejmenším ohodnocením (nejnižší cenou cesty). Je-li počet bezprostředních následníků každého uzlu konečný, pak je metoda UCE __úplná__ a __optimální__.
- __Časová náročnost:__ Exponenciální
- __Paměťová náročnost:__ Eponenciální \(O(b^k)\)
    - \(b\) je faktor dělení
    - \(k\) je koeficient získaný podílem ceny optimálního řešení a nejmenšího přírůstku ceny mezi dvěma uzly.

Algoritmus UCS s _redukcí_ předchůdců a opakujících se uzlů v `OPEN` je následující:
1. Sestrojí se seznam `OPEN` (bude obsahovat všechny uzly určené k expanzi) a umístí se do něj počáteční uzel včetně jeho (nulového) ohodnocení.
2. Je-li seznam `OPEN` prázdný, pak úloha nemá řešení a prohledávání se ukončí jako _neúspěšné_. Jinak se pokračuje.
3. Vybere se ze seznamu `OPEN` uzel s nejnižším ohodnocením.
4. Je-li vybraný uzel cílovým uzelm, ukončí se prohledávání jako _úspěšné_ a vrátí se cesta od kořenového uzlu k cílovému uzlu (posloupnost stavů nebo operátorů). Jinak se pokračuje.
5. Vybraný uzel se expanduje, všechny jeho bezprostřední následníci, kteří nejsou jeho předci, se umístí do seznamu `OPEN` a to včetně jejich ohodnocení. Z uzlů, které se v seznamu `OPEN` vyskytují vícekrát se ponechá pouze uzel s nejlepším ohodnocením, ostatní se ze seznamu vyjmou. Následně se vrací do bodu 2.

Metoda UCS není vhodná pro úlohy, kdy cesta z výchozího do cílového uzlu prochází pouze několika málo jinými uzly s vysokými cenami přechodů, protože pak prohledává zbytečně mnoho cest s nízkými cenami.

### Metoda slepého prohledávání do hloubky
Metoda slepého prohledávání do hloubky (DFS) je další metoda prohledávání stavového prostoru. Je __neúplná__ a __neoptimální__.
- __Časová náročnost:__ Exponenciální \(O(b^m)\)
- __Paměťová náročnost:__ Lineární \(O(bm)\)
    - \(b\) je faktor dělení.
    - \(m\) je maximální prohledávaná hloubka stromu.

Základní verze algoritmu DFS je téměř nepoužitelná - může nastat smyčka v generování uzlů, která vede k nekonečnému zásobníku. Proto se používá modifikovaný algoritmus této metody, který využívá __zásobník LIFO__. Algoritmus této modifikace je následující:
1. Sestrojí se zásobník `OPEN` (bude obsahovat všechny uzly určené k expanzi) a umístí se do něj počáteční uzel.
2. Je-li zásobník `OPEN` prázdný, pak úloha nemá řešení. Prohledávání se ukončí jako _neúspěšné_. Jinak se pokračuje.
3. Vybere se z vrcholu zásobníku `OPEN` první uzel.
4. Je-li vybraný uzel cílovým uzlem, pak se prohledávání ukončí jako _úspěšné_ a vrátí se cesta od kořenového uzlu k cílovému uzlu (posloupnost stavů nebo operátorů). Jinak se pokračuje.
5. Vybraný uzel se expanduje a do zásobníku `OPEN` se umístí všechny jeho bezprostřední následnící, kteří v tomto zásobníku ještě nejsou a kteří nejsou ani předky generovaného uzlu. Následně se vrací do bodu 2.

### Metoda omezeného prohledávání do hloubky
Metoda omezeného prohledávání do hloubky (DLS) je modifikace metody DFS. Je vhodná pro řešení úlohy, u které dokážeme odhadnout hloubku řešení. Tak můžeme problém opakovaného generování stejných stavů vyřešit omezením hloubky prohledávání. Metoda DLS je __neúplná__ a __neoptimální__.
- __Časová náročnost:__ Exponenciální \(O(b^n)\)
- __Paměťová náročnost:__ Lineární \(O(bm)\)

Algoritmus metody DLS je následující:
1. Sestrojí se zásobník `OPEN` a umístí se do něj počáteční uzel s označením hloubky (0).
2. Je-li zásobník `OPEN` prázdný, pak úloha nemá řešení. Prohledávání se ukončí jako _neúspěšné_. Jinak se pokračuje.
3. Vybere se z vrcholu zásobníku `OPEN` první uzel.
4. Je-li vybraný uzel cílovým uzlem, pak se ukončí prohledávání jako _úspěšné_ a vrátí se od kořenovéo uzlu k cílovému uzlu (posloupnost stavů nebo operátorů). Jinak se pokračuje.
5. Pokud je hloubka vybraného uzlu menší než zadaná maximální hloubka, tak se tento uzel expanduje a všechny jeho bezprostřední následníci se umístí do zásobníku `OPEN` s hloubkou o jedna větší než je hloubka expandovaného uzlu. Následně se vrací do bodu 2.

### Metoda postupného zanořování do hloubky
Metoda postupného zanořování do hloubky (IDS) je iterativní využití metody DLS. Používá se tam, kdy bychom mohli použít DLS, ale nedokážeme předem odhadnout hloubku. Metoda IDS je __úplná__ a __optimální__.
- __Časová náročnost:__ Exponenciální \(O(b^m)\)
- __Paměťová náročnost:__ Lineární \(O(bm)\)

Algoritmus metody IDS je následující:
1. Nastaví se hloubka prohledávání na hodnotu 1.
2. Použije se metoda DLS. Skončí-li metoda _úspěchem_ (nalezením cesty), skončí se také _úspěchem_ a vrátí se nalezená cesta. Jinak se pokračuje.
3. Dosáhla-li hloubka prohledávání maximální hodnotu, skončí se _neúspěchem_. Jinak se hloubka prohledávání inkrementuje a vrací se do bodu 2.

### Metoda zpětného navracení
Metoda zpětného navrácení (backtracking) místo expanze vybraného uzlu používá generování. Vygeneruje se jeden následník a v případě neúspěchu se generuje další následník. Metoda je __neúplná__ a __neoptimální__.
- __Časová náročnost:__ Exponenciální
- __Paměťová náročnost:__ Lineární

Algoritmus metody zpětného navrácení je následující:
1. Sestrojí se zásobník `OPEN` (bude obsahovat uzly určené k expanzi) a umístí se do něj počáteční uzel.
2. Je-li zásobník `OPEN` prázdný, pak úloha nemá řešení. Prohledávání se ukončí jako _neúspěšné_. Jinak se pokračuje.
3. Jde-li na uzel na vršku zásobníku aplikovat první/další operátor, tak se tento operátor aplikuje a pokračuje se bodem 4. V opačném případě se testovaný uzel odstraní z vrcholu zásobníku a vrací se do bodu 2.
4. Je-li nový vygenerovaný uzel (uzel vzniklý aplikací operátoru) cílovým uzlem, tak se prohledávání ukončí jako úspěšné a vrací se cesta od kořenového uzlu k cílovému uzlu (posloupnost stavů nebo operátorů). Jinak se nový uzel uloží na vršek zásobníku a vrací se do bodu 2.

Metodu zpětného navrácení lze modifikovat tak, že nový uzel se do zásobníku `OPEN` neukládá, pokud se již v tomto zásobníku nachází, tj. pokud nový uzel je již předchůdcem uzlu na vršku zásobníku.

### Metoda obousměrného prohledávání
Metoda obousměrného prohledávání (BS) je aplikace prohledávání BFS v obou směrech od počátečního stavu a cílového stavu. Časová složitost metody zůstává stejná, ale paměťová složitost klesá. Metoda je __úplná__ a __optimální__.
- __Časová náročnost:__ Exponenciální
- __Paměťová náročnost:__ Exponenciální \(O(b^{d/2})\)

### Forward checking
Prohledávání s dopřednou kontrolou.

![Forward checking](/Images/26/forward_checking_1.png)
![Forward checking](/Images/26/forward_checking_2.png)

### Min-conflict search
Prohledávání s minimalizací konfliktů.

![Min-conflict](/Images/26/min_conflict.png)

## Informované metody
### Metoda Best First Search
Metoda Best First Search (BestFS) je podobná neinformované metodě UCS. Algoritmus metody je prakticky stejný jako u UCS. Rozdíl spočívá pouze v _ohodnocující funkci_: V metodě UCS byla hodnotou této funkce v uzlu \(n\) cena cesty (součet cen přechodů) z počátečního uzlu do uzlu \(n\). V informovaných metodách musí cena cesty obsahovat i _odhad_ ceny z uzlu \(n\) do uzlu cílového.

\[f(n) = g(n) + h(n)\]

- \(g(n)\) je cena cesty z počátečního uzlu do uzlu \(n\).
- \(h(n)\) je odhad ceny cesty z uzlu \(n\) do cílového uzlu (heuristika).

### Metoda Greedy Search
Metoda Greedy Search (GS) ohodnocuje uzly pouze heuristickou funkcí \(h(n)\), tj. odhadovanou cenou z daného uzlu do cílového uzlu. K expanzi vybírá uzel, který má toto ohodnocení nejnižší. Z hlediska úplnosti, optimálnosti a časové a prostorové náročnosti je metoda GS stejná jako DFS. Dobrá heuristika může značně zredukovat časovou náročnost.

### Metoda A*
Metoda A* je nejznámnější a nejpoužívanější metodou pro řešení úloh prohledáváním stavového prostoru. Tato metoda je __úplná__ a __optimální__ (pro přípustné heuristické funkce). K ohodnocení uzlů používá plný vztah \(f(n) = g(n) + h(n)\).

> Heuristická funkce \(h(n)\) musů být tzv. _spodním odhadem_ skutečné ceny cesty od ohodnocovaného uzlu k cíli. Taková heuristika se pak nazývá __přípustnou heuristikou__.

Časovou a prostorovou náročnost výrazně ovlivňuje použitá heuristika. Pokud je použitá heuristika dobrým spodním odhadem skutečné ceny, pak jsou expandovány pouze uzly kolem optimální cesty.

## Metody založené na rozkladu úloh na podproblémy
Metoda založené na rozkladu úloh na podproblémy jsou přirozené metody řešení úloh, které při řešení obtížných problémů používá i člověk. Uzlem v _AO_ grafech značí __podproblém__ (podúlohu). Jsou dva základní typy problémů:
- Problém \(A\) je řešitelný, je-li řešitelný alespoň jeden z podproblémů - __OR problém__.
- Problém \(E\) je řešitelný, jsou-li řešitelné všechny podproblémy - __AND problém__.

![AND a OR problém](/Images/26/and_or_problem.png)

Smíšené problémy můžeme přčvést na čisté AND a OR problémy zavedením pomocných uzlů nebo vynecháním nedůležitých uzlů.

![Převod na čistý problém](/Images/26/prevod_na_cisty_problem.png)

### AO algoritmus
AO algoritmus je neinformovaná metoda řešení úlohy rozkladem na podúlohy. Její algoritmus je následující:
1. Sestrojí se prázdné seznamy `OPEN` a `CLOSED`. Do seznamu `OPEN` se uloží počáteční uzel.
2. Zleva se vyjme uzel ze seznamu `OPEN` a označí se jako uzel `X`.
3. Zkoumá se řešitelnost uzlu `X`:
    - Je-li uzel `X` řešitelný, přenese se informace o jeho řešitelnosti jeho předchůdcům. Je-li řešitelný počáteční problém, tak se řešení ukončí jako _úspěšné_. Vytvoří a vrátí se relevantní část AND/OR grafu.
    - Není-li uzel `X` řešitelný a nelze-li jej rozložit na podproblémy, tak se přenese informace o jeho neřešitelnosti jeho předchůdcům. Není-li řešitelný počáteční problém, řešení se ukončí jako _neúspěšné_.
    - Expanduje se uzel `X` (rozloží se na podproblémy) a všechny jeho následníci se uloží do seznamu `OPEN`.
4. `X` se uloží do seznamu `CLOSED`.
5. Je-li seznam `OPEN` prázdný, ukončí se řešení jako _neúspěšné_. Jinak se vrací na bod 2.

### Informovaný AO* algoritmus
AO* algoritmus je informovaná metoda řešení úlohy rozkladem na podproblémy. Algoritmus vybírá k prohledání vždy nejnadějnější podstrom každého OR uzlu počínaje kořenovým uzlem. Pokud lze jednotlivé podproblémy ohodnocovat pomocí nějaké heuristické funkce, můžeme v každém uzlu OR přepínat mezi řešitelnými podproblémy a řešit tak nejnadějnější podstrom. Ohodnocení bývý číselné kde:
- 0 znamená triviální (řešitelný) uzel.
- `FUTILITY` označuje neřešitelný uzel.

## Metoda hraní her
> Princip hraní her je následující: Jsou dva pravidelně se střídající hráči, kteří hrají nějakou hru. Každý z těchto hráčů se snaží __vyhrát__. Problém spočívá v nalezení tahu hráče, který je právě na tahu (hráč A). Pro tohoto hráče bude problém řešitelný, povede-li k jeho výhře alespoň jeden z jeho možných tahů (_problém OR_). V dalším tahu táhne soupeř (hráč B), proto musí být všechny tahy hráče B řešitelné pro hráče A (_problém AND_). Řešení vede tedy na prohledávání __AND/OR grafů__.

Existují různé druhy her:
- __Jednoduché hry__ - U jednoduchých her je možné prozkoumat a vyšetřit všechny možné tahy v reálném čase. Lze zde využít AO algoritmu. Přiklad jednoduché hry je např. Tick-Tack-Toe (piškvorky)
- __Složité hry__ - U složitých her je možné prozkoumat pouze několik následující tahů. Prohledávání jejich AO grafů je nemožné. Příklad složité hry jsou např. šachy.
- __Hry s neurčitostí__ - Hry s neurčitostí používají při hře kostky nebo jiný zdroj __náhody__.

Ve vytvořených AND/OR grafech je počet stavů grafu určen počtem možných tahů a ohodnocení uzlů a listů je dáno na základě výhodnosti daného tahu.

### Jednoduché hry
Příklad hry se zápalkami. Je sedm zápalek a hráči postupně odebírají až tři zápalky doku žádná nezbyde. Hráč, který odebere poslední zápalku vyhrává.

![Hra se zápalkami](/Images/26/hra_se_zapalkami.png)

### Složité hry
U složitých her je úplné prohledávání jejich AND/OR grafu nemožné (příliš velký celkový počet možných stavů). Proto se prohledává pouze do předem dané hloubky. Pokud se v této hloubce nenachází koncové problémy, u kterých lze rozhodnout o _řešitelnosti_/_neřešitelnosti_ problémů je nutné tyto uzly nějakým způsobem hodnotit. K ohodnocení vnitřních uzlů se používají např. celočíselné hodnotící funkce, jejíž kladné hodnoty znamenají příznivé stavy pro hráče A a záporné hodnoty pak příznivé stavy pro hráče B. Vítězství nebo prohra jsou hodnocemi maximálními hodnotami v daném číselném intervalu. Z toho plyne:
- Hráč __A__ si vybírá tahy vedoucí ke stavů s __maximálním ohodnocením__.
- Hráč __B__ si vybírá tahy vedoucí ke stavů s __minimálním ohodnocením__.

### Algoritmus MiniMax
Algoritmus MiniMax je metoda řešení složitých her. Základem jeho algoritmu je rekurzivní procedura `MiniMax`, která se zavolá pro aktuální stav hry a hráče A. Tat procedura vrací ohodnocení uzlu pro hráče A a tah k uzlu s maximálním ohodnocením (v daném stavu hry nejvýhodnější tah). Procedura předpokládá, že je zadána maximální hloubka prohledávání. V této proceduře dochází ka zbytečnému vyšetřování některých uzlů.

Algoritmus MiniMax je následující:
1. Předaný vstupní uzel se nazve uzlem `X`.
2. Je-li uzel `X` listem (konečný stav hry, nebo uzel v maximální hloubce) vrátí se ohodnocení tohoto uzlu. Jinak se pokračuje.
3. Je-li na tahu hráč __A__, tak se postupně pro všechny jeho možné tahy (bezprostřední následníky uzlu `X` a hráče B) volá procedura `MiniMax`. Z vrácených hodnoty se vrací ta _maximální_. Je-li `X` kořenovým uzlem vratí se i tah, který vede k nejlépe ohodnocenému bezprostřednímu následníku.
4. Je-li na tahu hráč __B__, tak se postupně pro všechny jeho možné tahy (bezprostřední následníky uzlu `X` a hráče A) volá procedura `MiniMax`. Z vrácených hodnot se vrací ta _minimální_.

![Algoritmus MiniMax](/Images/26/mini_max.png)

### Alfa a Beta řezy
Algoritmus Alfa a Beta řezy je další metoda řešení složitých her. Zabraňuje zbytečnému vyšetřování uzlů a to zavedením tzv. _alfa_ a _beta_ řezů (zastavení).
- __Alfa řezy__ zabrání zbytečnému vyšetřování tahů hráče __A__.
- __Beta řezy__ zabrání zbytečnému vyšetřování tahů hráče __B__.

Vyšetřování možných tahů se v daném uzlu zastaví vždy, když platí \(\alpha \geq \beta\). Algoritmus MiniMax se zavedením alfa a beta řezů se často nazývá přímo __AlfaBeta  algoritmus__. Procedura AlfaBeta je následující:
1. Předaný vstupní uzel se nazve uzlem `X`.
2. Je-li `X` počátečním/kořenovým uzlem, tak se nastaví \(\alpha = -\infty\), \(\beta = \infty\) (v praxi max. a min. hodnotu).
3. Je-li uzel `X` listem (konečný stav hry, nebo uzel v maximální hloubce) tak se procedura ukončí a vrátí se ohodnocení tohoto listu.
4. Je-li uzel typu OR (na tahu je hráč A):
    1. Dokud je \(\alpha < \beta\), tak se postupně pro první/další tah (bezprostředního následníka uzlu `X` a hráče B) volá procedura `AlfaBeta` s aktuálními hodnotami \(\alpha\) a \(\beta\). Po každém vyšetřeném tahu se nastaví hodnota proměnné \(\alpha\) na __maximum__ z aktuální a navrácené hodnoty.
    2. Procedura se ukončí a vrací se aktuální odnota proměnné \(\alpha\). Pro kořenový uzel se vrací i tah, který vede k nejlépe ohodnocenému bezprostřednímu následníku.
5. Je-li uzel typu AND (na tahu je hráč B):
    1. Doku je \(\alpha < \beta\), tak se postupně pro první/další tah (bezprostředního následníka uzlu `X` a hráče A) volá procedura `AlfaBeta` s aktuálními hodnota \(\alpha\) a \(\beta\). Po každém vyšetřením tahu se nastaví hodnota proměnné \(\beta\) na __minimum__ z aktuální a navrácené hodnoty.
    2. Procedura se ukončí a vrátí se aktuální hodnota proměnné \(\beta\).

![Algoritmus Alfa Beta](/Images/26/alfa_beta.png)

### Hry s neurčitostí
Pro hry s neurčitostí se používá modifikace algoritmu MiniMax zvaná __ExpertMiniMax__. Tato procedura je následující:
1. Předaný vstupní uzel se nazve uzlem `X`.
2. Je-li uzel `X` listem (konečný stav hry nebo uzel v maximální hloubce) vrátí se ohodnocení tohoto uzlu. Jinak se pokračuje.
3. Je-li na tahu hráč A, tak se postupně pro všechny jeho možné tahy (bezprostřední následníky uzlu `X` a hráče B) volá procedura `ExpertMiniMax`. Následně se vrátí maximální hodnotu z hodnot `expectimax`. Je-li `X` kořenovým uzlem vrací se i tah, který vede k nejlépe ohodnocenému bezprostřednímu následníku.
4. Je-li na tahu hráč B, tak se postupně pro všechny jeho možné tahy (bezprostřední násleníky uzlu `X` a hráče A) volá procedura `ExpectMiniMax` a vrací se minimální hodnota z hodnot `expectimin`.

![Expectimax](/Images/26/expectimax.png)
![Expectimin](/Images/26/expectimin.png)
