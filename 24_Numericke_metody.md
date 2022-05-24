# Numerické metody
- Otázky: přímé a iterační metody pro řešení soustav lineárních rovnic, numerické řešení obyčejných diferenciálních rovnic
- Předmět:

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

- Pro matice \(4 \times 4\) a větší se pro vápočet determinantu musí matice __rozdělit__ na menší matice. Musíme se dostat k maticím \(3 \times 3\), jejichž determinant můžeme vypočítat pomocí Sarrusova pravidla. Tomuto postupu se říka __Laplacův rozvoj__. Postup výpočtu determinantu je následující:
    1. Vybereme si nějaký sloupec/řádek matice a postupně pro všechny prvky tohoto sloupce/řádku rozsekáme matici na několik menších matic.
    2. Rozsekané matice neobsahují vybraný sloupec a řádek, ve kterém se nachází prvek, nímž se násobíí matice.

![Laplacův rozvoj](/Images/24/laplacuv_rozvoj.png)

## Numerické řešení soustavy lineárních rovnic
Numerické řešení soustavy \(n\) lineárních rovnice se zabývá řešením následujícího druhu soustavu rovnice s neznýmými \(x_1, x_2, ..., x_n\):

\[
    a_{11}x_1 + a_{12}x_2 + \dots + a_{1n}x_n = b_1 \\
    a_{21}x_1 + a_{22}x_2 + \dots + a_{2n}x_n = b_2 \\
    \vdots \\
    a_{n1}x_1 + a_{n2}x_2 + \dots + a_{nn}x_n = b_n
\]

Matice \(A = (a_{ij})\), kde \(i,j = 1, ..., n\) se nazývá __matice soustavy__ a sloupcový vektor \(b = (b_1, ..., b_n)^T\) je __vektor pravých stra__. Budeme předpokládat, že matice soustavy je _regulární_, tj. že řešená soustava má právě jedno řešení.

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
- Přičítání/odečítání násobnků jednotlivých řádků k jiným.

Těmito úpravami se snažíme v matici soustavy \(A\) získat nuly po hlavní diagonálou matice a tím ji dostat do trojúhleníkového tvaru. Při dosažení tohoto tvaru potom můžeme z poslední rovnice přímo určit hodnotu poslední neznámé v soustavě a následně vypočítat ostatní neznámé.

![Gaussova eliminační metoda](/Images/24/gaussova_eliminacni_metoda.png)

### Iterační metody pro řešení algebraických rovnic
Iterační metody řešení soustavy rovnic na rozdíl od přímých metod nevedou k přesnému řešení po konečném, předem daném počtu kroků. U iteračních metod zvolíme __počáteční aproximaxi__ řešení a určitým postupem ji v každém kroku metody zlepšíme (zpřesníme). K řešení se přibližujeme _postupně_ a obecně ho dosáhneme až v limitě. Protože výpočet nelže provádět donekonečna, po jisté době jej ukončíme (počet iterací, splnění určité chyby). Výsledek tak bude přibližné řešení soustavy.

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

Na začátku výpočtu si zvolíme __počátační aproximaci__ \(x^{(0)} = (x_1^{(0)}, x_2^{(0), ... x_n^{(0)}})^T\) a tu dosadíme do pravé strany rovnice. Z toho nám vyjde nová aproximace, kterou můžeme opětovně dosazovat do pravé strany, až nedosáhneme dostatečně přesného výsledku. Dostatečnou přenost výsledku můžeme určit podle absolutní hodnoty rozdílu výsledků dvou po sobě jdoucích iterací - __chyba__.

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
Metoda půlení intervalů je nejjednodusšší metoda hledání kořene rovnice.

Mějme interval \(\langle a,b \rangle\) takový, že \(f(a) * f(b) < 0\) (nachází se v něm alespoň jeden kořen rovnice \(f(x) = 0\)). V každém kroku tento interval rozpůlíme \(s = \frac{a + b}{2}\) a vybereme tu polovinu intervalu, ve které je zaručena existence kořene. Platí-li \(f(x_k) = 0\) tak jsme nalezli výpočet rovnice. Jinak iteraci pokračujeme, dokud je polovina velikosti intervalu menší než požadovaná přenost (__podmínka ukončení__): \(b_k - a_k < 2 \varepsilon\). Jako výsledek potom zvolíme střed aktuálního intervalu.

Metoda konverguje, pokud se v počátečním intervalu nachází alespoň jeden kořen. Konverguje ale pomalu.

### Metoda regula falsi
