# 2D vektorová grafika
- Otázky: metody rasterizace úseček a polygonů, reprezentace objektů pomocí Bézierovy křivky
- Předmět: IZG
- Zdroje:
    - https://www.fit.vutbr.cz/study/courses/IZG/private/lecture/izg_slide_rasterizace_rev2021_169.pdf (úsečky a kružnice)
    - https://www.fit.vutbr.cz/study/courses/IZG/private/lecture/izg_slide_vyplnovani_rev2021_169.pdf (vyplňování)
    - https://www.fit.vutbr.cz/study/courses/IZG/private/lecture/izg_slide_krivky_print.pdf (křivky)

## Rasterizace
Základní grafické objekty jsou v paměti uloženy vektorově. Vektorová reprezentace objektů zabírá méně paměti a také s ní lze jednoduše provádět různé operace jako je posun, zvětšení a rotace. Oproti tomu zobrazovací zařízení se skládají z matice pixelů a tudíž zobrazují grafické objekty rastrově. Je tedy nutné umět převést vektorové objekty na jejich rastrovou reprezentaci. K tomu se využívá proces __rasterizace__.

> __Rasterizace__ je proces převodu vektorové reprezentace dat na jejich rastrovou formu s cílem dosáhnout maximální možné kvality a zároveň rychlosti výsledného zobrazení.

## Rasterizace úsečky
Úsečka je geometrická vektorová entita definovaná:
- Souřadnicemi dvou koncových bodů.
- Rovnicí přímky popisující geometrii:
    - _Obecná rovnice_: \(A_x + B_y + C = 0; \; A = (y_2 - y_1), \; B = (x_2 - x_1)\)
    - _Parametrická rovnice_: \(x = x_1 + t \times (x_2 - x_1); \; y = y_1 + t \times (y_2 - y_1), \; t \in \langle 0, 1 \rangle\)
    - _Směrnicový tvar_: \(y = k \times x + q; \; k = \Delta y / \Delta x = (y_2 - y_1) / (x_2 - x_1)\)

Algoritmy pro vykreslování úsečky jsou odvozeny pro případ, kdy úsečka leží v 1. kvadrantu, je rostoucí od počátečního bodu \(P_1\) ke koncovému bodu \(P_2\) a roste nejrychleji ve směru osy \(x\). Ostatní případ je nutné převést na tento například výměnnou souřadných os.

### Digital Differential Analyser
Digital Differential Analyser (DDA) je algoritmus rasterizace úsečky využívající _floating-point_ aritmetiku. Je to jeden z prvních a nejjednodušších algoritmů. Kvůli floating-point aritmetice není příliš efektivní a snadno implementovatelný v HW.

Vykresluje pixel po pixelu od \(P_1\) do \(P_2\). V ose \(x\) je přírůstek \(dx\) vždy 1 a v ose \(y\) je přírůstek dán velikostí směrnice \(k\) úsečky. Souřadnice \(y\) se zaokrouhluje na celé číslo.

\[
    x_{n+1} = x_n + dx, \; dx = 1 \\
    y_{n+1} = y_n + dy, \; dy = k = \frac{(y_2 - y_1)}{x_2 - x_1}    
\]

```cpp
LineDDA(int x1, int y1, int x2, int y2) {
    double k = (y2 - y1)/(x2 - x1);
    double y = y1;

    for (int x = x1; x <= x2; x++) {
        drawPixel(x, round(y));
        y += k;
    }
}
```

### Vykreslování úsečky s hlídáním chyby
Algoritmus vykreslování úsečky s hlídáním chyby je modifikovaný DDA algoritmus. Jeho rozdíl je pouze v tom, že se neprovádí výpočet skutečné souřadnice na ose \(y\). Místo toho se pracuje s hodnotou __relativní odchylky__ (chyby) aktuální celočíselné souřadnice od skutečné souřadnice v ose \(y\). Jestliže tato chyba překročí hodnotu \(0,5\), přesuneme se na další řádek, další celočíselnou souřadnici v ose \(y\). Po každém posunu na nový řádek je hodnota chyby snížena o hodnota \(1,0\).

### Bresenhamův (midpoint) algoritmus
Bresenhamův algoritmus je nejpoužívanější a nejefektivnější algoritmus vykreslování úsečky. Používá pouze celočíselnou aritmetiku (sčítání a porovnávání) a tak je rychlý a snadno implementovatelný v HW.

Bresenhamův algoritmus vykresluje úsečku pixel po pixel od \(P_1\) k \(P_2\). V ose \(x\) je přírůstek \(dx\) vždy roven jedné a v ose \(y\) záleží přírůstek na znaménku __prediktoru__. Při odvození prediktoru vycházíme ze _směrnicového tvaru_ rovnice úsečky. 

![Graf Bresenhamova algoritmu](/Images/11/bresenham_graf.png)

Vykreslování musíme rozhodovat, zda v ose \(y\) provedeme krok a vypočítávat chybu vykreslování \(E\). K předchozí hodnotě \(E\) přičteme v každém kroku poměrný krok. Pokud dojde k posunutí v ose \(y\), tak se hodnota následujícího \(E\) sníží o jedna.

\[
    E_i + \frac{\Delta y}{ \Delta x} < 0,5 \;\; krok(x_i + 1, y_i) \; E_{i+1} = E_i + \frac{\Delta y}{ \Delta x} \\
    E_i + \frac{\Delta y}{ \Delta x} \geq 0,5 \;\; krok(x_i + 1, y_i + 1) \; E_{i+1} = E_i + \frac{\Delta y}{ \Delta x} - 1
\]

Pro vylepšení výkonosti algoritmus se tento vztah převede z porovnání \(0,5\) na test znaménka. To provedem vynásobení rovnice \(2 \Delta x\). Výsledný vztah nazveme prediktorem \(P_i\).

\[
    P_i = 2 \Delta x E_i + 2 \Delta y - \Delta x \\\;\\
    P_i < 0 \;\; P_{i+1} = P_i + 2 \Delta y \\
    P_i \geq 0 \;\; P_{i+1} = P_i + 2 \Delta y - 2 \Delta x \\\;\\
    P_0 = 2 \Delta y - \Delta x
\]

```cpp
LineBresenham(int x1, int y1, int x2, int y2) {
    int dx = x2 - x1;
    int dy = y2 - y1;
    int P = 2*dy - dx;

    for (int x = x1; x <= x2; x++) {
        drawPixel(x, y);
        if (P >= 0) {
            P += 2*dy - 2*dx;
            y++;
        } else {
            P += 2*dy;
        }
    }
}
```

![Bresenhamův algoritmus na jiné kvadranty](/Images/11/usecka_jine_kvadranty.png)

### DDA s fixed point aritmetikou
Modifikace DDA algoritmus využívající fixed point aritmetiku. Algoritmus má vždy stejnou přesnost (využívá bitový posun o 8). Je rychlejší než obyčejný DDA (nepoužívá float hodnoty, ale obsahuje pořád pomalé dělení).

## Rasterizace kružnice
Kružnice je geometrická vektorová entita definovaná:
- Souřadnicemi středu a hodnotou poloměru
- Rovnicí kružnice popisující geometrii: \((x - s_1)^2 + (y - s_2)^2 = R^2\)

Kružnice je _osminásobně symetrická_. Stečí tedy vypočítat pouze jednu osminu jejích bodu umístěných v prvním kvadrantu. Zbývající body lze získat záměnnou souřadnice. Výpočty je výhodnější provádět pro kružnici se středem v počátku (\([0, 0]\)). Algoritmy rasterizace kružnice jsou tedy popsané pro tento případ.

![Body v kružnici](/Images/11/body_kruznice.png)

### Vykreslení kružnice po bodech
Vykreslení kružnice po bodech je nejjednodušší rasterizační algoritmus. Pracuje s floating-point aritmetikou a je tudíž výpočetně náročný. Vykresluje kružnici _ve směru hodinových ručiček_ po jednom pixelu od hodnoty 0 až do bodu \(x = y\) (do té doby je přírůstek na ose \(x\) jedna). Pozice v ose \(y\) se vypočte ze vztahu pro rovnici kružnice \(y = \sqrt{R^2 - x^2}\).

```cpp
CircleByPoints(int s1, int s2, int R) {
    int x = 0;
    int y = R;

    while (x <= y) {
        drawPixel(x, y);
        x += 1
        y = sqrt(R*R - x*x);
    }
}
```
![Vykreslení kružnice po bodech](/Images/11/vykresleni_kruznice_po_bodech.png)

### Vykreslení kružnice jako n-úhelník
Vykreslení kružnice jako n-úhelník je alternativa rasterizačního algoritmus DDA pro kružnici. Algoritmus rozdělí _kružnici na úsečky_ a ty postupně vykreslí. Pracuje s desetinnými čísly a tudíž je pomalý a navíc v HW těžko implementovatelný. Využívá rekurentní vztah pro výpočet souřadnic, využívají konstatní úhel \(\alpha\), jehož hodnota bude záviset na počtu úseček do nichž je kružnice rozdělena.

\[
    x_{n+1} = x_n \cos \alpha - y_n \sin \alpha \\
    y_{n+1} = x_n \sin \alpha + y_n \cos \alpha
\]

Algoritmus je citlivý na kumulované numerické chyby výpočtu funkcí \(\sin\) a \(\cos\). Pro odstranění této chyby je možné spočítat pouze osminu kružnice a zbytek vykreslit s využitím symetrie, nebo použít _High precision_ variantu algoritmu.

```cpp
CircleDDA(int R, int N) {
    double cosa = cos(2*PI / N);
    double sina = sin(2*PI / N);
    int x1 = R, y1 = 0;
    int x2, y2;

    for (int i = 0; i < N; i++) {
        x2 = x1*cosa - y1*sina;
        y2 = x1*sina + y1*cosa;
        drawLine(x1, y1, x2, y2);
        x1 = x2;
        y1 = y2;
    }
}
```
![Vykreslování kružnice jako n-úhelník](/Images/11/vykresleni_kruznice_n_uhelnik.png)

### Midpoint algoritmus pro kružnici
Midpoint algoritmus je algoritmus rasterizace kružnice, jehož princip je v podstatě stejný jako u Bresenhamova algoritmus pro úsečku. Je postaven na určování __midpointů__ vůči kružnicici. Rozdíl je ve stanovení kritéria pro určení prediktoru. Algoritmus pracuje pouze s celými čísly a je tak efektivní a snadno implementovatelný v HW.

Kružnice se vykresluje z bodu \([0, R]\) postupně po jednotlivých pixelech ve směru hodinových ručiček pro její osminu. Zbývající body získáme symetrií. Ve směru osy \(x\) se pohybujeme s přírůstkem \(dx = 1\) dokud neplatí \(x = y\). Ve směru osy \(y\) klesáme od hodnoty \(R\). O posunu ve směru osy \(y\) __rozhodujeme__ podle __znaménka prediktoru__ \(P_i\). Prediktor je vypočítá z rovnice kružnice v jejím homogením tvaru.

\[
    F(x, y): x^2 + y^2 - R^2 = 0
\]

Rozhodnutí, zda se posuneme v ose \(y\) provedeme podle polohy __středního bodu__ (midpointu) \([x_i + 1, y_i - 1/2]\) vůči kružinice. Midpoint dosadíme do vztahu pro prediktor a následně při porovnání s nulou dosáhneme nové hodnoty \(y\).

\[
    P_i = F(x_i + 1, y_i - 1/2) \\
    P_i = (x_i + 1)^2 + (y_i - 1/2)^2 - R^2 \\\;\\
    P_i < 0 \rightarrow y_{i+1} = y_i \\
    P_i \geq 0 \rightarrow y_{i+1} = y_i - 1
\]

Pro průběžné výpočty během vykreslování kružnice je opět výhodnější vyjádřit prediktor _rekurentně_ (na základě hodnoty z předchozího kroku). Výsledný rekurentní vztah pro prediktor bude opět záležet jak na hodnotě předchozího prediktoru, tak na jeho _znaménku_. Pro vlastní výpočty během rasterizace kružnice jsou rozhodující __rozhodovací vztahy__ pro výpočet prediktoru a vztahy pro rekurnentí výpočet prediktoru.

\[
    P_{i+1} = (x_{i+1} + 1 )^2 + (y_{i+1} - 1/2)^2 - R^2 \\\;\\
    P_{i+1} = P_i + 2x_i + 3 \Leftarrow P_i < 0 \\
    P_{i+1} = P_i + 2x_i - 2y_i + 5 \Leftarrow P_i \geq 0 \\\;\\
    P_0 = 1 - R
\]

```cpp
CircleMid(int s1, int s2, int R) {
    int x = 0, y = R;
    int P = 1 - R;
    int X2 = 3, Y2 = 2*R - 2;

    while (x < y) {
        drawPixel(x, y);
        if (P >= 0) {
            P += - Y2;
            Y2 -= 2;
            y--;
        }

        P += X2;
        X2 += 2;
        x++;
    }
}
```
![Midpoint algoritmus](/Images/11/midpoint_algoritmus.png)

## Rasterizace elipsy
Elipsa je geometrická vektorová entita definovaná:
- Souřadnicemi středu, hodnotami hlavní a vedlejší poloosy a úhlem natočení hlavní poloosy
- Rovnicí elipsy popisující geometrii: \(F(x, y) = b^2 x^2 + a^2 y^2 - a^2 b^2 = 0\)

Elipsa je 4 symetrická a tudíž se algoritmus rasterizace provádí vždy pro jednu čtvrtinu bodů, zbylé body vykreslíme záměnnou souřadnic. Algoritmy jsou odvozeny pro elipsu se středem v počátku \([0, 0]\) a s nulovým natočením.

![Body elipsy](/Images/11/body_elipsy.png)

### Midpoint algoritmus pro elipsu
Midpoint algoritmus pro elipsu je ekvivalentní midpoint rasterizačnímu algoritmus pro kružinici. Opět využívá pouze celočíselnou aritmetiku a tudíž je efektivní a snadno implementovatelný na HW. Vykreslení je rozděleno na dvě části: první polovina se jde s krokem 1 po ose \(x\) a druhá polovina pokračuje s krokem 1 po ose \(y\).

Pro vykreslovanou oblast jdeme po pixelu od bodu \([0, b]\), dokud není \(2b^2x = 2a^2x\) a pro druhou část pokračujeme až do bodu \([a, 0]\). V ose \(x\) (oblast 1) a \(y\) (oblast 2) postupujeme s přírůstek \(dx = 1\) a \(dy = 1\). Posun v ose \(x\)/\(y\) určuje __znaménko prediktoru__.

![Midpoint alguritmus pro elipsu](/Images/11/midpoint_elipsa.png)

## Rasterizace polygonů
Rasterizace polygonů, neboli _vyplňování 2D oblastí_, je proces nalezení a označení všech vnitřních bodů dané oblasti. Vstupem algoritmů je popis hranice oblasti a jejich výstupem je rastrový popis vyplnění oblasti. Pro zjednodušení algoritmů má vektorový popis 2D oblastí určité konvence: seznam hraničních entit vyplňované oblasti musí být orientovaný a spojitý a vnější hrany a otvory uvnitř obrazce jsou orientovány opačným směrem. Orientace hrany lze otestovat vektorovým součinem dvou sousedních hran (konvexní polygony) nebo sumou přes celý polygon (nekonvexní polygony).

Jsou tři způsoby vyplňování složitých (protínajících se) oblastí:
- __Paritní vyplňování__ - Hranice odděluje vyplněný a nevyplněný prostor.
- __Vnitřní vyplňování__ - Jsou vyplněny všechny body, které nejsou vně oblasti.
- __Nenulové vyplňování__ - Nenulové objetí bodu uzavřenou smyčkou při vyřešení sebeprotínání.

![Vyplňování paritní a vnitřní](/Images/11/vyplnovani1.png)
![Vyplňování nenulové](/Images/11/vyplnovani2.png)

Rasterizace polygonů funguje na principu __řádkového vyplňování__. Prochází se po řádcích celý obraz a při začátku oblasti se začne vyplňovat dokud se nenarazí na další hranu oblasti. Z toho vyplývá __paritní řádkové vyplňování__, kde se pro každý řádek vytvoří seznam průsečíků, který se seřadí. Úseky mezi sudými a lichými oblastmi jsou pak vykresleny. Ve vrcholech a hranách rovnoběžnými s řádky je nutné testovat extrémy a navíc se po rasterizaci musí vykreslit i __obrys oblasti__.

![Problém krajních bodů](/Images/11/vyplnovani_krajni_body.png)

### Inverzní řádkové vyplňování
Inverzní řádkové vyplňování je algoritmus rasterizace polygonů. Od každé hrany se jde směrem doprava a invertují se pixely. To se provede pro každou hranu a nakonec je potom nutné zvlášť vykreslit obrys. Algoritmus se musí provádět v separátním bufferu aby neovlivňoval okolí.

### Pinedův algoritmus
Pinedův algoritmus je algoritmus rasterizace polygonů pro konvexní n-úhelníky. Každá hrana úhelníku má z jedné strany kladnou část a z druhé strany zápornou. Kladná část všech hran tvoří vnitřek polygonu. Kladnost/zápornost ploch lze určit podle vektorů hran polygonu - z toho je odvozena __hranová funkce__.

Když hranová funkce vratí pro daná bod kladnou hodnotu, pak tento bod leží uvnitř polygonu. Pro každý bod se tedy spočítají hranové funkce pro všechny hrany polygonu. Vykresleny jsou jen ty body, pro které je hranová funkce všech hran kladná.

![Pinnedův algoritmus: Hranová funkce](/Images/11/pineduv_algoritmus.png)

Není nutné vyhodnocovat hranové funkce \(E_i(x, y)\) pro každý bod. Hodnotu lze určit i na základě sousedního bodu \(P(x \pm 1, y)\) nebo \(P(x, y \pm 1)\).

![Pinnedův algoritmus: Výpočet hranové funkce](/Images/11/pineduv_algoritmus_zjednoduseni.png)

## Křivky v počítačové grafice
Křivky v počítačové grafice se využívají pro vykreslování modelů, fontů, pohybu kamery po křivce atd. Od křivek se očekávají určité požadované vlastnosti:
- __Invariance k lineárním transformacím__ - Rotace řídících bodů křivky nemá vliv na tvar křivky (body je možné transformovat a výsledná křivka má stejný tvar).
- __Konvexní obálka__ - Křivka leží v konvexní obálce svých řídících bodů.
- __Lokalita změn__ - Pohyb řídícím bodem změní křivku pouze lokálně (pouze na daném místě).
- __Interpolace krajních bodů__ - Křivka prochází krajními body.

Existuje několik druhů křivek:
- __Aproximační křivka__ - Křivka, která neprochází svými řídícími body.
- __Interpolační křivka__ - Křivka, která prochází svými řídícími body (body jsou proložené křivkou).
- __Racionální křivka__ - Křivka, která používá váhové koeficienty \(w_i\) řídících bodů. Je invariantní vůči perspektivní projekci.
- __Neracionální křivka__ - Křivka, která má všechny váhové koeficienty rovné jedné. Je neinvariantní vůči perspektivní projekci, tvar křivky lze ovlivnit pouze změnou polohy řídících bodů.

Křivky lze matematicky zapsat několika způsoby:
- __Parametrické vyjádření křivky:__ \(Q(t) = [x(t), y(t)];~t \in \langle 0, 1 \rangle\)
- __Polynomiální křivka__ - _kubické polynomy:_

\[
    x(t) = a_x t^3 + b_x t^2 + c_x t + d_x \\
    y(t) = a_y t^3 + b_y t^2 + c_y t + d_y
\]

- __Maticová zápis:__

![Maticový zápis křivky](/Images/11/maticovy_zapis_krivky.png)

- __Vyjádření bodů křivky pomocí řídicích bodů:__

\[
    Q(t) = P_0 F_0(t) + P_1 F_1(t) + P_2 F_2(t) + P_3 F_3(t)\\
    P \text{... řídící body, } P_i = [x_i, y_i] \\
    F_i \text{... polynomiální funkce (váha jednotlivých bodů)}
\]

### Spojitost křivek
Křivky mohou být spojované ze segmentů po částech polynomiální křivky. Existují dva druhy spojitosti: __Parametrická spojitost__ \(C^n\) a __Geometrická spojitost__ \(G^n\):
- __Parametrická spojitost__ udává jak dlouho oba segmenty křivky k sobě přimykají.
    - \(C^0\) - totožnost navazujících koncových bodů.
    - \(C^1\) - totožnost těšných vektorů v navazujících bodech.
    - \(C^2\) - totožnost vektorů druhé derivace v navazujících bodech.
- __Geometrická spojitost__
    - \(G^0\) - totožnost navazujících koncových bodů.
    - \(G^1\) - tečné vektory v navazujících bodech jsou lineárně závislé.
    - \(G^2\) - shoda první křivosti v navazujících bodech.

### Spline křivka
Spline křivka je křivka spojovaná ze segmentů po částech polynomiální křivky (pružné křivítko, kovový pásek proložený body). Spline křivka, která interpoluje své řídící body (prochází řídícími body) se nazývá __přirozený spline__. Cíle spline křivek je minimalizace křivosti křivy (délka, energie), efektivní řízení tvaru křivky (modelování) a snaha snížit počet řídících bodů.

### Fergusonova kubika
Fergusonova kubika je nejčastěji používaná _interpolační_ křivka. Je určena dvěma koncovými body \(P_0\) a \(P_1\) (určují polohu) a dvěma tečnými vektory \(p_0\) a \(p_1\) (určují vyklenutí). Je to poměrně neinteraktivní a neintuitivní křivka. Mezi dvěma body je jeden segment, jehož změna tvaru je nelokální.

![Fergusonova kubika](/Images/11/fergusonova_kubika.png)

### Beziérovy křivky
Beziérovy křivky jsou _aproximační_ křivky, které se široce využívají v 2D grafice, fontech a šablonování. Je to polynomiální křivka využívající __Bernsteinovy polynomy__ \(B_{i}^n\). Křívka stupně \(n\) je určena \(n + 1\) body, je možné ji specifikovat pro různý počet řídících bodů. Beziérova křivka prochází koncovými body a leží v jejich konvexní obálce.

> Beziérova křivka je definována jako suma řídících bodů váhovaná bernsteinovými polynomy.

![Definice beziérovy křivky](/Images/11/bezierova_krivka_definice.png)

Bernsteinovy polynomy mají nezápornou hodnotu a jejich součet je roven jedné. Bernsteinovy polynomy lze definovat rekurentně. Z předchozích bernsteinových polynomů lze tak vypočítat nové. To využívá algoritmus pro vykreslování beziérovy křivky __de Casteljau__.

\[
    B_i^n(t) = (1 - t) B_i^{n-1}(t) + t B_{i-1}^{n-1}(t)    
\]
![Bernsteinovy polynomy](/Images/11/bernsteinovy_polynomy.png)

#### Algoritmus de Casteljau
Algoritmus de Casteljau je rasterizační algoritmus pro vykreslování beziérových křivek. Je to rekurzivní algoritmus využívající vlastnosti bernsteinových polynomů. Plyne z rekurentní definice pro _bernsteinovy polynomy_. Úseky řídícího polynomu jsou děleny v poměru hodnot \(t\) a \(1-t\).

Vykreslování křivky se tak provádí opakovaným výpočtem pro různé hodnoty \(t\) se zvoleným krokem. Vypočtené body se pak spojí úsečkami. Postup je následující:
1. Zvolí se dostatečně jemný krok, se kterým se mění hodnota \(t\) (\(t \in \langle 0,1 \rangle\)).
2. Úseky polynomů se dělí v poměru \(t\) a \(t-1\), v místě dělení vznikne nový bod pro další dělení. Snižuje se tak s každým krokem stupeň polynomu, až na konci zbyde pouze jeden bod.
3. Vzniklé body se spojí úsečkami.

[Příklad Algoritmu de Casteljau](https://www.youtube.com/watch?v=YATikPP2q70)

![Algoritmus de Casteljau](/Images/11/de_casteljau.png)

#### Speciální případy beziérových křivek
__Beziérovy kubiky__ jsou beziérovy křivky, jejichž segment je popsán čtyřmi řídícími body. Posunem těchto řídících bodu nastává _nelokální_ změna křivky. Navazování segmentů beziérových kubik vyžaduje spojitost \(C^1\), shodnost tečných vektorů a totožnost koncových bodů. Na vykreslování beziérových kubik lze použít algoritmus de Casteljau metodou "divide and conquer". Celá křivka se rekurzivně dělí na dvě podkřivky. Jakmile se získá dostatečně rovná podkřivka, tak se již dále nedělí a podkřivka je vykreslena.

__Racionální beziérovy křivky__ jsou beziérovy křivky, které využívají váhování. Místo neracionálních bernsteinových polynomů jsou použity _racionální polynomy_ \(R_{i}^n\). Tyto polynomy nemají rekurentní definici a tak pro vykreslení křivky nelze použít algoritmus de Casteljau. Polynomy mají nezápornou hodnotu a jednotkový součet, křivka tudíž leží v konvexní obálce,
