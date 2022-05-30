# Numerické metody
- Otázky: přímé a iterační metody pro řešení soustav lineárních rovnic, numerické řešení obyčejných diferenciálních rovnic
- Předmět: IMA (původně okruh 23)

## Příloha: Determinanty
> Nechť \(A\) je matice řádu \(n\). Determinantem matice \(A = (a_{ij})\) nazýváme číslo
>
> \[det A = |A| = \sum (-1)^{\pi(i_1, i_2, ..., i_n)} a_{1i_1} a_{2i_2} ... a_{ni_n}\]
>
> kde se sčítá přes všechny permutace \((i_1, i_2, ..., i_n)\) množiny \(\N_n = {1,2,...,n}\).

- Pro matici \(2 \times 2\) se pro výpočet determinantu používá __křížové pravidlo__:

\[det A = ad - bc\]

- Pro matici \(3 \times 3\) se pro výpočet determinantu používá __Sarrusovo pravidlo__:

![Sarrusovo pravidlo](/Images/24/sarrusovo_pravidlo.png)

- Pro matice \(4 \times 4\) a větší se pro výpočet determinantu musí matice __rozdělit__ na menší matice. Musíme se dostat k maticím \(3 \times 3\), jejichž determinant můžeme vypočítat pomocí Sarrusova pravidla. Tomuto postupu se říka __Laplacův rozvoj__. Postup výpočtu determinantu je následující:
    1. Vybereme si nějaký sloupec/řádek matice a postupně pro všechny prvky tohoto sloupce/řádku rozsekáme matici na několik menších matic.
    2. Rozsekané matice neobsahují vybraný sloupec a řádek, ve kterém se nachází prvek, nímž se násobí matice.

![Laplacův rozvoj](/Images/24/laplacuv_rozvoj.png)

## Příloha: Druhy matic
- Čtvercová matice - Matice se stejným počtem řádků a sloupců.
- Nulová matice - Matice, v níž jsou všechny prvky rovny nule.
- Jednotková matice - Čtvercová matice, která ma na hlavní diagonále (úhlopříčka zleva nahoře napravo dolů) jedničky a všude jinde nuly.
- Schodová matice - Matice, kde každý následující řádek má na začátku více nul než předchozí řádek.
- Transponované matice - Matice, která má zaměněné řádky a sloupce.
    - Symetrická matice - Matice, která po transponování zůstane stejná.
    - Antisymetrická matice - Matice, která po transponování zůstane stejná mimo znaménka čísel.
- Diagonální matice - Matice, která má všude jinde než na hlavní diagonále nuly.
- Regulární matice - Matice, jejíž determinant je nenulový.

## Numerické řešení soustavy lineárních rovnic
Numerické řešení soustavy \(n\) lineárních rovnice se zabývá řešením následujícího druhu soustavu rovnice s neznámými \(x_1, x_2, ..., x_n\):

\[
    a_{11}x_1 + a_{12}x_2 + \dots + a_{1n}x_n = b_1 \\
    a_{21}x_1 + a_{22}x_2 + \dots + a_{2n}x_n = b_2 \\
    \vdots \\
    a_{n1}x_1 + a_{n2}x_2 + \dots + a_{nn}x_n = b_n
\]

Matice \(A = (a_{ij})\), kde \(i,j = 1, ..., n\) se nazývá __matice soustavy__ a sloupcový vektor \(b = (b_1, ..., b_n)^T\) je __vektor pravých stran__. Budeme předpokládat, že matice soustavy je _regulární_, tj. že řešená soustava má právě jedno řešení.

### Přímé metody pro řešení algebraických rovnic
Přímé metody vedou k řešení soustavy rovnic v konečném počtu kroků. Pokud se v průběhu výpočtu nebudeme dopouštět zaokrouhlovacích chyb, tak takto nalezené řešení bude přesné.

#### Cramerovo pravidlo
Pro pouze velmi malé soustavy rovnic je vhodné __Cramerovo pravidlo__. To říká, že je-li matice soustavy regulární, tj. její _determinant je nenulový_, pak řešení soustavy lze vypočítat následovně:

\[
    x_1 = \frac{D_1}{D},\;\; x_2 = \frac{D_2}{D},\;\; x_n = \frac{D_n}{D}
\]

\(D\) je determinant matice soustavy \(A\) a \(D_k\) jsou determinanty matic, které vzniknou z matice \(A\) nahrazením \(k\)-tého sloupce této matice vektorem pravých stran \(b\).

#### Gaussova eliminační metoda
Pro obecné matice se používá __Gaussova eliminační metoda__. Základem této metody je úprava soustavy na trojúhelníhový tvar pomocí elementárních úprav matic:
- Prohození řádků.
- Násobení a dělení nenulovým číslem.
- Přičítání/odečítání násobků jednotlivých řádků k jiným.

Těmito úpravami se snažíme v matici soustavy \(A\) získat nuly po hlavní diagonálou matice a tím ji dostat do trojúhleníkového tvaru. Při dosažení tohoto tvaru potom můžeme z poslední rovnice přímo určit hodnotu poslední neznámé v soustavě a následně vypočítat ostatní neznámé.

![Gaussova eliminační metoda](/Images/24/gaussova_eliminacni_metoda.png)

### Iterační metody pro řešení algebraických rovnic
Iterační metody řešení soustavy rovnic na rozdíl od přímých metod nevedou k přesnému řešení po konečném, předem daném počtu kroků. U iteračních metod zvolíme __počáteční aproximaci__ řešení a určitým postupem ji v každém kroku metody zlepšíme (zpřesníme). K řešení se přibližujeme _postupně_ a obecně ho dosáhneme až v limitě. Protože výpočet nelze provádět donekonečna, po jisté době jej ukončíme (počet iterací, splnění určité chyby). Výsledek tak bude přibližné řešení soustavy.

#### Jacobiho metoda
Jacobiho metoda říká, že pokud máme soustavu rovnic:

\[
    a_{11}x_1 + a_{12}x_2 + a_{13}x_3 = a_{14} \\
    a_{21}x_1 + a_{22}x_2 + a_{23}x_3 = a_{24} \\
    a_{31}x_1 + a_{32}x_2 + a_{33}x_3 = a_{34}
\]

Tak můžeme z nich vyjádřit \(x_1\), \(x_2\) až \(x_n\):

\[
    x_1 = \frac{a_{14} - a_{12}x_2 - a_{13}x_3}{a_{11}} \\
    x_2 = \frac{a_{24} - a_{21}x_1 - a_{23}x_3}{a_{22}} \\
    x_3 = \frac{a_{34} - a_{31}x_2 - a_{32}x_2}{a_{33}}
\]

Na začátku výpočtu si zvolíme __počátační aproximaci__ \(x^{(0)} = (x_1^{(0)}, x_2^{(0)}, ... x_n^{(0)})^T\) a tu dosadíme do pravé strany rovnice. Z toho nám vyjde nová aproximace, kterou můžeme opětovně dosazovat do pravé strany, až nedosáhneme dostatečně přesného výsledku. Dostatečnou přenost výsledku můžeme určit podle absolutní hodnoty rozdílu výsledků dvou po sobě jdoucích iterací - __chyba__.

Jacobiho metoda __konverguje__ (neustále se přibližuje k výsledku), pokud je matice soustavy rovnice řádkově nebo sloupcově __diagonálně dominantní__. To znamená, pokud je v každém řádku matice absolutní hodnota prvku na diagonále větší jak součet absolutních hodnot všech ostatních prvků v tomto řádku/sloupci.

#### Gauss-Seidelova metoda
Gauss-Seidelova metoda je velmi podobná Jacobiho metoda, liší se v podmínkách konvergence. Hlavním rozdílem je, že v každém dílčím kroku výpočtu \(x_i\) používáme nejnovější hodnotu \(x_j\) a ne hodnotu z předcházejícího kroku.

Gauss-Seidelova metoda konverguje je-li matice soustavy __pozitivně definitní__. Ověření, zda je daná matice pozitivně definitní, je náročné a pro velké matice prakticky neproveditelné.

> Symetrická matice \(A\) řádu \(n\) se nazývá __pozitivně definitní__, jestliže pro každý nenulový sloupcový vektor \(x = (x_1, ..., x_n)^T\) platí:
>
> \[x^T A x > 0\]

## Numerické metody řešení jedné nelineární rovnice
Při řešení jedné nelineární rovnice hledáme kořen \(x \in R\) v nelineární rovnici \(f(x) = 0\). Při hledání kořenů je třeba nejdříve zjistit, kolik má rovnice kořenů. Poté najdeme intervaly obsahující právě jeden kořen rovnice - __separace kořenů rovnice__. Následně se pomocí nějaké metody aproximuje kořen rovnice.

### Metoda půlení intervalů (metoda bisekce)
Metoda půlení intervalů je nejjednodušší metoda hledání kořene rovnice.

Mějme interval \(\langle a,b \rangle\) takový, že \(f(a) * f(b) < 0\) (nachází se v něm alespoň jeden kořen rovnice \(f(x) = 0\)). V každém kroku tento interval rozpůlíme \(s = \frac{a + b}{2}\) a vybereme tu polovinu intervalu, ve které je zaručena existence kořene. Platí-li \(f(x_k) = 0\) tak jsme nalezli výpočet rovnice. Jinak iteraci pokračujeme, dokud je polovina velikosti intervalu menší než požadovaná přenost (__podmínka ukončení__): \(b_k - a_k < 2 \varepsilon\). Jako výsledek potom zvolíme střed aktuálního intervalu.

Metoda konverguje, pokud se v počátečním intervalu nachází alespoň jeden kořen. Konverguje ale pomalu.

![Metoda půlení intervalů](/Images/24/puleni_intervalu.png)

### Metoda regula falsi
Metoda regula falsi je velmi podobná metodě půlení intervalů. Jediný rozdíl je v tom, že interval nedělíme v polovině, ale v místě průsečíku úsečky mezi body \([a_k, f(a_k)]\) a \([b_k, f(b_k)]\). Průsečík se tak vypočítá:

\[
    x_k = b_k - \frac{b_k - a_k}{f(b_k) - f(a_l)} * f(b_k)    
\]

Metoda vždy konverguje a je obvykle rychlejší než půlení intervalů. Podmínka ukončení je \(|x_k - x_{k-1}| < \varepsilon\).

![Metoda regula falsi](/Images/24/regula_falsi.png)

### Metoda sečen
Metoda sečen je velmi podobná metodě regula falsi. Vycházíme v ní z intervalu \(\langle a,b \rangle\) obsahujícího kořen rovnice. Označíme \(x_0 = a\) a \(x_1 = b\). Vedeme sečnu body \([x_0, f(x_0)]\) a \([x_1, f(x_1)]\) a najdeme její průsečík s osou \(x\). Tento průsečík označíme \(x_2\) a vedeme další sečnu bodu \([x_1, f(x_1)]\) a \([x_2, f(x_2)]\) a tak dále. V \(k\)-tém kroku metody vypočítáme aproximaci kořene podle vzorce:

\[
    x_{k+1} = x_k - \frac{x_k - x_{k-1}}{f(x_k) - f(x_{k-1})} * f(x_k)
\]

Podmínka ukončení je \(|x_k - x_{k-1}| < \varepsilon\). Metoda sečen je rychlejší než metoda regula falsi, ale nemusí vždy konvergovat. Protože je obtížné zjistit, zda bude metoda pro danou rovnici konvergovat, je vhodné zadat maximální počet kroků výpočtu. Pokud je tento počet kroků překročen, výpočet se ukončí s tím, že metoda diverguje.

![Metoda sečen](/Images/24/metoda_secen.png)

### Newtonova metoda (metoda tečen)
V Newtonově metodě pracujeme s tečnami funkce. Předpokládáme, že funkce \(f\) má derivaci. Zvolíme počáteční aproximaci \(x_0\). Vedeme tečnu v bodě \([x_0, f(x_0)]\) a její průsečík s osou \(x\) označíme \(x_1\). \(x_1\) je nová aproximace a znovu vytvoříme tečnu \([x_1, f(x_1)]\) a najdeme její průsečík s osou \(x\) a tak dále. Pokračuje se dokud není naplněna podmínka ukončení \(|x_k - x_{k-1}| < \varepsilon\). Nová aproximace se vypočítá rovnicí:

\[x_{k+1} = x_k - \frac{f(x_k)}{f'(x_k)}\]

Newtonova metoda je nejefektivnější metoda pro řešení nelineárních rovnice, ale nemusí konvergovat. Podmínka konvergence pro Newtonovu metodu se nazývá __Fourierova podmínka__:

> Nechť na intervalu \(\langle a,b \rangle\) leží jediný kořen \(f(x) = 0\) a nechť \(f'(x)\) a \(f''(x)\) jsou spojité a nemění znaménka na intervalu \(\langle a,b \rangle\). Pokud zvolíme za počáteční podmínku aproximaci \(x_0 \in \langle a,b \rangle\) tak, aby byla splněna podmína:
>
> \[f(x_0) * f''(x_0) > 0\]
>
> bude Newtonova metoda konvergovat.

![Newtonova metoda](/Images/24/newtonova_metoda.png)

## Numerické řešení obyčejných diferenciáních rovnic
Diferenciální rovnice většinou popisují fyzikální děje, kde jako proměnné vystupují derivace funkcí. U některých je možné určit přesné analytické řešení. U složitějších analytické řešení buď neexistuje nebo je obtížné ho nalézt. Používají se proto __iterační metody__.

Společným znakem numerických řešení je, že řešení nehledáme jako spojitou funkci, definovanou na celém zkoumaném intervalu \(\langle a,b \rangle\). Hodnoty přibližného řešení počítáme pouze v konečném počtu bodů \(a = x_0 < x_1 < \dots < x_n = b\). Těmto bodům říkáme __uzlové body__ (body sítě) a množině \(\{x_0, x_1, ..., x_n\}\) říkáme __síť__. Rozdíl \(h_i = x_{i+1} - x_i\) se nazývá __krok__ sítě v uzlu \(x_i\). Metody mohou být __jednokrokové__ (vycházejí pouze z aktuálního stavu) nebo __vícekrokové__ (používají historii stavů).

Metody řeší diferenciální rovnice prvního řádu se zadanou počáteční podmínkou:

\[y' = f(x, y),\;\; y(x_0) = y_0\]

### Eulerova metoda
Eulerova metoda je metoda prvního stupně. Ve všech bodech s síti platí:

\[y'(x_i) = f(x_i, y(x_i))\]

Derivace funkce \(y'(x_i)\) vlastně vyjadřuje směrnici tečny ke grafu funkce v daném bodě. Vzorec pro výpočet jednoho kroku Eulerovy metody je následující:

\[y_{i+1} = y_i + h * f(x_i, y_i)\]

Přesnost Eulerovy metody závisí na velikosti __integračního kroku__ \(h\). Hodnoty řešení v bodě \(x_0\) poznáme z počáteční podmínky rovnice (např.: \(y(0) = 1;\; x_0 = 0,\; y_0 = 1\)). V reálných případech platí \(y'(x_i) = f(x_i, y_i)\).

> Princip Eulerovy metody vlastně spočítá ve výpočtu derivace (směrnice) v aktuálním bodě. S touto směrnicí se posuneme o krok \(h\), opět spočítáme směrnici a znovu se posuneme a tak dále.

![Eulerova metoda](/Images/24/eulerova_metoda.png)

- __1. modifikace Eulerovy metody__:

\[
    k_1 = f(x_n, y_n) \\
    k_2 = f(x_n + \frac{1}{2}h, y_n + \frac{1}{2}hk_1) \\
    y_{n+1} = y_n + hk_2
\]

- __2. modifikace Eulerovy metody__:

\[
    k_1 = f(x_n, y_n) \\
    k_2 = f(x_n + h, y_n + hk_1) \\
    y_{n+1} = y_n + \frac{1}{2}h(k_1 + k_2)
\]

### Metody Runge-Kutta
Metody Runge-Kutta vylepšují Eulerovu metodu a její modifikace (modifikace Eulerovy metody vlastně patří mezi Runge-Kutta metody). Obecný vzoren pro Runge-Kutta metody je:

\[
    y_{n+1} = y_n + h(w_1 k_1 + \dots + w_s k_s) \\\;\\
    k_1 = f(x_n, y_n) \\
    k_i = f(x_n + \alpha_i h, y_n + h \sum_{j=1}^{i-1} \beta{ij} k_j),\;\; i = 2, ..., s
\]

kde \(w_i\), \(\alpha_i\) a \(\beta_{ij}\) jsou konstanty volené tak, aby metoda měla maximální stupeň.

Nejčastěji se používá Runge-Kutta metoda 2. řádu nebo 4. řádu:

![Runge-Kutta 2. řádu](/Images/24/runge_kutta_2.png)
![Runge-Kutta 4. řádu](/Images/24/runge_kutta_4.png)

### Vícekrokové metody
U vícekrokových metod počítáme přibližné řešení v dalším uzlovém bodě sítě pomocí několika předchozích bodů. Jsou přesnější a rychlejší, jejich hlavní slabina ale spočívá v pomalém _rozjezdu_ (musí se nějak aproximovat prvních \(n\) uzlových bodů, používají se jednokrokové metody). Vícekrokové metody přestávají být efektivní ve chvíli, kdy je funkce nespojitá. Při nespojitostech je třeba opětovného hledání prvních \(n\) bodů, což metodu zpomaluje.

## Chyby numerických metod
Při každé aproximaci v numerických metodách musíme počítat s faktorem chyby. Existují chyby dvojího typu:
- __Lokální chyby__ - Chyby, které vznikají v každém kroku. Může jít buď o chybu _zaokrouhlovací_ (round-off error) nebo o chybu _numerické aproximace_ (truncation error).
- __Akumulované chyby__ - Chyby, které se sbírají po celou počtu výpočtu.

Přenost výpočtu je tak závislá na velikosti _integračního kroku_. Neplatí, že čím menší krok, tím vyšší přesnost. Při zmenšení kroku dojde k nárůstu chyby numerické aproximace a naopak se zmenší zaokrouhlovací chyba. Při zvětšení naopak. Při překročení určité velikosti kroku začne jeden druh chyby neúnosně narůstat. Proto je třeba nalézt ideální délku kroku.
