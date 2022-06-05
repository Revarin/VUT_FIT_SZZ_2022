# Strojové učení 
- Otázky: učení s učitelem, učení bez učitele, posilované učení
- Předmět: IMS (původně okruh 25)
- Zdroje:
    - https://wis.fit.vutbr.cz/FIT/st/cfs.php.cs?file=%2Fcourse%2FIZU-IT%2Flectures%2F2122izu_06.pdf (logika)
    - https://www.fit.vutbr.cz/study/courses/SUR/public/prednasky/01_uvod/SUR_uvod.pdf (strojové učení)

## Strojové učení
Strojové učení (Machine Learning) je schopnost inteligentního systému měnit své znalosti tak, aby příště vykonával stejnou nebo podobnou činnost účinněji a efektivněji. Existují různé druhy strojového učení:
- __Učení s učitele__
- __Učení bez učitele__
- __Posilované učení__

## Učení s učitelem
Učení s učitelem spočívá v tom, že pro každá krok učení je známá _požadovaná odezva_ a systém je tak okamžitě informován o aktuálním hodnocením jeho poslední akce. Učení se provádí na __trénovací množině__ příkladů \(T\), kdy každý příklad je představován množinou __vstupních hodnot__ (vstupním vektorem) a množinou požadovaných __výstupních hodnot__ (výstupním vektorem).

\[T= \{(i_1, d_1), (i_2, d_2), ..., (i_n, d_n\}\]

Často se množina dostupných dat nepoužívá k trénování celá, ale rozdělí se na dvě nebo tři podmnožiny:
- První množina je množina __trénovací__ (cca 80% dat). Použije se k trénování systému.
- Druhá množina je množina __testovací__ (cca 10% až 20% dat). Použije se pro testování naučených znalostí.
- Třetí množina (cca 10% dat) se někdy používá k doladění parametrů systému.

Metody učení s učitelem pracují s vektory, které nabývají symbolických hodnot. Jsou založené na předpokladu, že každá hypotéza, která vyhovuje dostatečně velké množině trénovacích příkladů, bude vyhovovat i dalším, dosud neznámým příkladům.

### Tvorba rozhodovacích stromů
Tvorba rozhodovacích stromů (Decision Tree Building) vytváří _rozhodovací strom_. Rozhodovací stromy slouží ke klasifikaci objektů na základě hodnot jejich atributů. Jsou vytvářeny ze známé množiny příkladů. Používají se při dolování dat z databází.

![Tabulka pro rozhodovací strom](/Images/27/tabulka_rozhodovaci_strom.png)

#### Algoritmus Decision Tree
Pro základní budování rozhodovacích stromů slouží algoritmus __Decision Tree__. Tento algoritmus má dva vstupní parametry:
- Množiny __příkladu__ \(MP\) (např.: řádky tabulky)
- Množinu __podmínkových atributů__ \(MA\)

Algoritmus funguje následovně:
1. Patří-li všechny prvky množiny příkladů \(MP\) do stejné třídy, vrátí se _listový uzel_ označený touto třídou. Jinak se pokračuje.
2. Je-li množina atributů \(MA\) prázdná , vrátí se _listový uzel_ označený _disjunkcí_ všech tříd, do kterých patří prvky v množině příkladů \(MP\). Jinak se pokračuje.
3. Vybere se atribut \(A_i\), který se odstraní z množiny atributů \(MA\) a učiní se kořenem aktuálního stromu. Nechť \(MA_{-i}\) je množina atributů \(MA\) bez atributu \(A_i\).
4. Pro každou hodnotu \(H_{ji}\) vybraného atributu \(A_i\):
    1. Vytvoří se nová větev stromu označená hodnotou \(H_{ji}\).
    2. Rekurzivně se volá algoritmus s parametry \(MP_{ji}\) a \(MA_{-i}\), kde množina \(MP_{ji}\) je podmnožina všech prvků množiny příkladů \(MP\), které mají hodnotu \(H_{ji}\) atributu \(A_i\).
    3. Vrácený podstrom/uzel se připojí k této větvi.

Jinak řečeno, vytváří se strom na základě _rozhodovacích parametrů_. Hloubka stromu závisí na tom, jestli je možné nějaký rozhodovací atribut ignorovat, protože nehledě na jeho hodnotu jsou výsledky z trénovací množiny stejné.

![Rozhodovací strom](/Images/27/rozhodovaci_strom.png)

Algoritmus je jednoduchý, ale obsahuje zásadní problém, a to jest výběr atributu \(A_i\) v bodě 3. Nevhodné výběry vedou k hlubokým a neefektivním vyhledávacím stromům, přestože optimální strom může být jednoduchý.

#### Algoritmus ID3
Algoritmus __ID3__ (Induction of Decision Tree) je modifikace algoritmu Decision Tree, který řeší problém při výběru rozhodovacího atributu \(A_i\). Výběr atributu není náhodný, ale je prováděn tak, aby byl maximalizován __informační zisk__ - aby byl vybrán atribut, který co nejvíce ovlivní výsledné rozhodnutí. Z jiného pohledu, množiny, které vzniknou rozdělení dle nějakého atributu mají __nejmenší míru entropie__, tj. je v nich co nejvíce prvků spadajících pod stejný výsledek. Vybíráme tedy takový atribut, který rozdělí množinu na podmnožiny s nejmenší entropií a přinese tak největší informační zisk.

Např. při vytvoření podmnožin \(MP_1 = \{A, A, A, A\}\), \(MP_2 = \{A, B, B, A\}\), \(MP_3 = \{C, C, B, C, C, C\}\) budě mít množina \(MP_1\) nulovou entropii a \(MP_2\) bude mít z trojice nejvyšší entropii. Jednotlivé míry entropie lze vypočítat následovně.

![Výpočet entropie](/Images/27/vypocet_entropie.png)

__Celková entropie__ rozdělení podle daného atributu je pak spočítána jako __vážený průměr__ (váha je dána počtem prvků v množině) entropií podmnožin.

\[E(MP, Att) = \sum_{i=1}^{3} \frac{|MP_i|}{|MP|} E(MP_i)\]

Výsledný prohledávací strom vytvořený pomocí algoritmu ID3 bude vypadat následovně:

![Rozhodovací strom ID3](/Images/27/rozhodovaci_strom_id3.png)

### Prohledávání prostoru verzí
Prohledávání prostoru verzí (Version Space Search) představuje soubor metod učení významných pojmů/hypotéz na základě _pozitivních_ a _negativních_ příkladů. Při učení se hledá takový popis daného pojmu/objektu/hypotézy, který zahrnuje všechny pozitivní příklady a vylučuje všechny negativní příklady z trénovací množiny příkladů. Trénovací množina musí obsahovat oba typy příkladů.

![Trénovací množina pro prohledávání prostoru verzí](/Images/27/prohledavani_prostoru_verzi.png)

#### Algoritmus Specific to General Search
Algoritmus Specific to General Search je metoda učení prohledáváním prostoru, která pracuje od specifického k obecnějšímu. Její algoritmus je následující:
1. Vytvoří se dvě prázdné množiny `S` (Specific) a `N` (Negative).
2. Do množina `S` se uloží první __kladný__ příklad. Pro každý další příklad `p` z testovací množiny:
    - Je-li `p` __kladným příkladem__, pak pro každý pojem \(s \in S\):
        1. Pokud pojem `s` nelze unifikovat s příkladem `p` (`s` je obecnější než `p` a `p` spadá do množiny prvků, které lze pomocí `s` sestavit), pak se nahradí jeho _nejvíce specifickým zobecněním_, které lze unifikovat s příkladem `p`.
        2. Z `S` se odstraní všechny pojmy `s`, které jsou více _obecné_ než jiné pojmy v `S`.
        3. Z `S` se odstraní všechny pojmy `s`, které lze unifikovat s některým pojmem v `N`.
    - Je-li `p` __záporným příkladem__, pak:
        1. Z `S` se odstraní všechny pojmy `s`, které lze unifikovat s příkladem `p` (lze pomocí nich vyjádřit záporný prvek `p`).
        2. Příklad `p` se přidá do `N`.

Jinak řečeno: s pozitivními příklady se výsledné řešení stává obecnější (přidávají se možnosti správných řešení) a s negativními příklady se řešení stává specifičtější (odstraňují se ta řešení, která by správně identifikovala i špatný objekt).

![Průběh algoritmu Specific to General Search](/Images/27/specific_to_general_search.png)

#### Algoritmus General to Specific Search
Algoritmus General to Specific search je metoda učení prohledávání prostoru, která rpacuje od obecného ke specifickému. Její algoritmus je následující:
1. Vytvoří se dvě prázdné množiny `G` (General) a `P` (positive) a do `G` se uloží __nejobecnější__ pojem (všechny jeho parametry jsou vyjádřené proměnnou).
2. Pro každá další příklad `p` z trénovací množiny:
    - Je-li `p` __záporným příkladem__, pak pro každá pojem \(g \in G\):
        1. Jestliže pojem `g` lze unifikovat s příkladem `p`, pak se nahradí jeho _nejobecnější specializací_, kterou nelze unifikovat s příkladem `p`.
        2. Z `G` se odstraní všechny pojmy `g`, které jsou více _specializované_ než jiné pojmy v `G`.
        3. Z `G` se odstraní všechny pojmy `g`, které nelze unifikovat s některém pojmem v `P`.
    - Je-li `p` __kladným příkladem__, pak:
        1. Z `G` se odstraní všechny pojmy `g`, které nelze unifikovat s příkladem `p`.
        2. Příklad `p` se přidá do `P`.

Jinak řečeno: se zápornými příklady se z obecného řešení stává konkrétnější (je konkretizováno), aby nevyhovovalo záporným řešením. Kladné příklady pak odstraňují ta řešení, pomocí kterých je není možné vyjádřit,

![Průběh algoritmu General to Specific Search](/Images/27/general_to_specific_search.png)

#### Algoritmus Candidate Eliminations
Algoritmus Candidate Elimination spojuje postupy obou předchozích algoritmů. Každý pojem, který by byl obecnější než nějaký pojem v množině `G` (General), by zahrnoval některé negativní příklady. Každý pojem, který by byl specifičtější něž nějaký pojem v množině `S` (Specific), by vylučoval některé požitivní příklady. Význam vztahu množin `G` a `S` je na obrázku níže:

![Význam algoritmu Candidate Eliminations](/Images/27/graf_candidate_eliminations.png)

## Rozpoznávání a klasifikace obrazů
Pro rozpoznávání obrazů existují různé algoritmy, které pracují s jedním z následujících popisů obrazu:
- __Příznakový popis__ - Popisuje vektory číselných příznaků. Využívá statických informací o příznacích obrazů obsažených v množině trénovacích dat. Jde o __statické příznakové rozpoznávání__.
- __Strukturální/syntaktický popis__ - Popisuje strukturálními prvky (primitivy). Využívá vztahy mezi příznaky obrazů rozpoznávaných objektů.

![Popis obrazu](/Images/27/popis_obrazu.png)

Zásadním předpokladem úspěšného rozpoznávání je výběr relevantních příznaků nebo primitiv.

### Příznakové rozpoznávání
U příznakového rozpoznávání pracujeme s:
- n-rozměrnými číselnými __vektory příznaků__, které popisují rozpoznávané objekty.
- __Množinou tříd__, do kterých rozpoznávané objekty chceme zařadit.
- __Trénovací množinou__, která je tvořena dvojicemi n-rozměrného číselného vektoru a k němu přiřazení třídy, do které spadá.

Cílem příznakového rozpoznávání je zařadit libovolný vektor příznaků do jedné z tříd - __klasifikovat jej__. Metody příznakového rozpoznávání vycházejí z předpokladu, že obrazy objektů nebo jevů stejných tříd tvoří v n-rozměrném obrazovém prostoru __shluky__. Tyto shluky mohou od seby být zřetelně oddělitelné (__separable__), nebo se mohou prolínat a pak jsou neoddělitelné (__inseparable__). Systémy, které se na trénovací množině naučí obrazy rozpoznávat a poté klasifikují nové obrazy, se nazývají __klasifikátory__.

#### Dichotomie
Dichotomie je klasifikace shluků obrazů do dvou tříd. K tomu se používají __diskriminační funkce__ (funkce, která zastupuje jednu třídu). Obraz je umístěn do třídy, jejíž diskriminační funkce má pro něj největší hodnotu.

#### Etalony
Etalony jsou těžište shluků obrazů jednotlivých tříd. Obraz je klasifikován do tříd, k jejímuž etalonu má nejblíže. Tato klasifikace pracuje na principu klasifikace podle diskriminačních funkcí.

### Strukturální rozpoznávání
Jedná se o rozpoznávání obrazů na základě jaho popisu pomocí __primitiv__. Existují dva základní přístupy ke strukturálnímu rozpoznávání obrazů:
- Rozpoznávání obrazu pomocí __gramatik__ - __syntaktické rozpoznávání__
- Rozpoznávání obrazu __porovnáním se vzory__ uloženými v databázi - __template matching__

Syntaktické rozpoznávání klasifikuje obrazy do \(R\) tříd pomocí syntaktické analýzy. Obraz (__řetězcový popis objektu__) je chápan jako __slova__ a množina __primitiv__ jako množina __terminálních symbolů__. Pokud pak gramatika generuje všechna slova, které reprezentují obrazy třídy \(r\), a negeneruje žádné slovo, které reprezentuje obraz jiné třídy, lze klasifikaci převést na problém určení gramatiky, která jako jediná ze všech \(R\) gramatik generuje rozpoznávaný obraz (slovo). Na úspěšnost strukturálního (syntaktického) rozpoznávání má velký vliv výběr primitv.

#### Freemanův řetezcový kód
Používá se ke strukturálnímu popisu obrysu objektu. Za primitiva popisující obrys objektu považujem __směry sousedů__. Problém je změna popisu objektu při natočení objektu (řešení pomocí rozdílu ve směru sousedů - __diferenční kód__) a změně startovací pozice popisu (řešení binárním posuvem diferenčního kódu dokud nevznikne největší číslo).

![Freemanův řetězcový kód](/Images/27/freemanuv_kod.png)
![Freemanův diferenční řetězcový kód](/Images/27/diferencni_kod.png)

## Učení bez učitele
Učení bez učitele spočívá v __hledání podobnosti__ mezi příklady trénovací množiny a v zařazování příkladů s podobnými charakteristikami do skupin. Umělý systém přitom nemá žádnou informaci o správnosti klasifikace. Jedinou informaci, kterou má je __počet skupin__, do kterých má příklady zařadit.

Příklady trénovací množiny jsou většinou představované __číselnými vektory__ příznaků klasifikovaných objektů či dějů. Metody učení bez učitele jsou pak založeny na předpokladu, že tyto vektory (body), které specifikují v příslušném `n`-rozměrném obrazovém prostoru příklady, tvoří __shluky__. Tyto shluky mohou představovat rozmanité `n`-rozměrné útvary.

### k-means clustering
Algoritmus k-means clustering klasifikuje příklady (číselné vektory) z trénovací množiny do předem daného počtu \(k\) shluků. Algoritmus zařazuje vstupní vektor do toho shluku, k jehož __středu__ (těžišti) má nejkratší vzdálenost. Vstupem algoritmu je počet shluků \(k\) (musí být menší než počet vektorů). Průběh algoritmu je následující:
1. Náhodně určí \(k\) rozdílných vektorů (často je vybere z trénovací množiny), které se považují za středy shluků.
2. Zařadí se všechny vektory trénovací množiny do příslušných shluků dle použité __metriky__ (nejčastěji se používá Euklidovská vzdálenost).
3. Přepočítají se středy všech shluků (například jako průměr ze všech testovacích vektorů přiřazených do tohoto shluku).
4. Pokud se pozice ani jednoho středu nezměnila tak algoritmus končí. Jinak se pokračuje bodem 2.

![k-means clustering](/Images/27/k_means_clustering.png)

## Posilované učení
Posilované učení se od učení s učitelem odlišuje tím, že systém ohodnocuje své akce na základě __penalizací__ a __odměn__ získaných v koncových stavech a na základě svých hodnocení stavů/akcí získaných vlastními předchozími zkušenostmi.

### Policy-only learning
Princip algoritmu Policy-only learning je založený na tom, že v každém uzlu grafu vedou maximálně dvě cesty. Každý uzel obsahuje schránku s kameny dvojí barvy - __bílé__ a __černé__ (analogie pravděpodobnosti, počet bílých kamenů označují pravděpodobnost cesty vlevo, počet černých kamenů označují pravděpodobnost cesty vpravo).

\[
    P_l = \frac{N_w}{N_w + N_b} \\
    P_r = \frac{N_b}{N_w + N_b}
\]

Na začátku učení obsahuje schránka každého rozcestí __stejný__ a dostatečný počet černých a bílých kamenů. Učení pak probíhá tak, že se provádí náhodné procházky. Pokud výsledná cesta procházky:
- Skončí v __cílovém stavu__, je do schránek na této cestě přidán kámen odpovídající barvy podle výběru směru - __odměna__. Pravděpodobnost výběru této cesty se zvyšuje.
- Skončí mimo cílový stav, je ze schránek odebrán kámen odpovídající barvy podle výběru směru - __penalizace__. Pravděpodobnost výběru této cesty se snižuje.

![Policy-only learning](/Images/27/policy_only_learning.png)

Po ukončení učení vybírá systém cestu pouze porovnáním počtu kamenů (už bez náhody). Počet cest z uzlu lze jednoduše rozšířit přidáním více kamenů různých barev. Metoda může mít dva zásadní problémy:
- V případě obecného grafu se může vracet do již dříve vyšetřovaných uzlů. Může se pak teoreticky při učení zacyklit.
- Všechny akce provedené na jedné cestě se hodnotí szejnými váhami, přestože správná ohodnocení mohou být značně rozdílná (některé cesty mohou být zbytečně dlouhé).

### Metoda TD learning
Metoda TD learning (On-Policy) je metoda založená na náhodných procházkách, během kterých ohodnocuje jednotlivé stavy \(s\). Stav \(s\) je vždy bezprostředním předchůdcem stavu \(s'\). Dochází tedy k _šíření hodnot_ ze stavů s odměnou/penalizací. Šíření ohodnocení je dáno vzorcem:

\[o(s) = o(s) + \alpha*(r(s') + \gamma*o(s') * o(s))\]

kde:
- \(o(s)\) je funkce ohodnocení stavu \(s\) při použití dané strategie pohybu.
- \(\alpha\) je koeficient učení
- \(\gamma\) je koeficient určující vliv ohodnocení stavu \(s'\) na ohodnocení předcházejícího stavu \(s\).
- \(r(s')\) je odměna za dosažení stavu \(s'\)

Pro přecházení mezi stavy lze použít různé strategie:
- __Random policy__ - Pravděpodobnosti přechodů mezi sousedními stavy jsou stejné a do sousedních stavů přechází zcela _náhodně_.
- __? policy__ - Pravděpodobnosti jsou různé (mohou být dány např. aktuálními hodnotami sousedních stavů).
- __Greedy policy__ - Pravděpodobnost jednoho přechodu je jedničková a pravděpodobnost ostatních nulové. Extrémní případ předchozího stavu.
- __\(\epsilon\)-greedy policy__ - Kombinace předchozích případů, kdy s pravděpodobností danou parametrem \(\epsilon\) se použije random policy a nebo greedy policy.

Princip učení tohoto algoritmu je následující:
1. Zvolí se hodnoty koeficientů \(\alpha\), \(\gamma\) a vynuluje se ohodnocení všech stavů. Vynuluje se počítadlo procházek \(p\) a nastaví se jeho maximální počet na \(p_{max}\). Nastaví se \(start \to s\).
2. Generuje se nový stav \(s'\) s použítím nějaké strategie.
3. Přepočítá se nová hodnota stavu \(s\) pomocí vztahu výše.
4. Je-li stav \(s'\) cílovým stavem, pak se inkrementuje počet procházek a \(start \to s\). Jinak se pokračuje \(s \to s'\).
5. Je-li \(p < p_{max}\) tak se pokračuje bodem 2.

![Metoda TD learning](/Images/27/td_learning.png)

Po naučení se již přechází z libovolného necílového stavu do sousedního stavu, který má nejvyšší hodnotu. Tato hodnota ale musí být stejná nebo lepší než hodnota aktuálního stavu. To může způsobit problém __uváznustí__ v nějakém stavu (lze řešit snížením koeficientu učení \(\alpha\)).

### Q learning
Q learning (Off policy) je metoda podobná metodě TD learning. Teto metoda místo hodnocení stavů hodnotí akce v těchto stavech. K hodnocení akcí používa vztah:

\[Q(s,a) = Q(s,a) + \alpha*(r(s') + \gamma*maxQ(s',a') - Q(s,a))\]

kde:
- \(\alpha\) je koeficient učení.
- \(\gamma\) je koeficient určující vliv hodnocení stavu \(s'\) na ohodnocení předcházejícího stavu \(s\).
- \(r(s')\) je odměna za dosažení stavu \(s\).
- \(Q(s,a)\) je hodnocení akce \(a\) provedené ze stavu \(s\).
- \(maxQ(s',a')\) označuje maximální hodnotu z ohodnocení všech akcí \(a'\), které je možné provést ve stavu \(s'\).

Metoda je aktivní metodou bez předem dané strategie výběru stavu \(s'\). Princip učení je následující:
1. Zvolí se hodnoty koeficientů \(\alpha\), \(\gamma\) a vynuluje se ohodnocení \(Q(s,a)\) všech akcí \(a\) ve všech stavech \(s\). Vynuluje se počítadlo procházek \(p\) a nastaví se jeho maximální počet na \(p_{max}\). Nastaví se \(start \to s\).
2. Vybere se akce \(a\), která povede k přechodu ze stavu \(s\) do stavu \(s'\).
3. Vypočítá se nová hodnota vybrané akce \(a\) ve stavu \(s\) pomocí vztahu výše.
4. Je-li stav \(s'\) cílovým stavem, pak se inkrementuje počítadlo procházek a nastaví se \(start \to s\). Jinak se pokračuje \(s \to s'\).
5. Je-li \(p < p_{max}\) tak se pokračuje bodem 2.

![Metoda Q learning](/Images/27/q_learning.png)

### SARSA
Metoda SARSA (On-Policy) je přístup, který také ohodnocuje akce, ale k jejich výběru používá nějako __strategii__ \(\Pi\) (místo hledání maxima z možných následujících akcí se používá přímo akce \(Q(s',a')\) vybraná touto strategií). Hlavní funkce pro aktualizaci Q-hodnoty závisí tedy na:
- Aktuálním stavu \(s\)
- Akci \(a\), kterou agent zvolí
- Odměně \(r\), kterou agent dostane za volbu této akce \(a\)
- Stavu \(s'\), do kterého agent vstoupí po provedení akce \(a\)
- Akci \(a'\), kterou agent zvolí ve svém novém stavu \(s'\)
