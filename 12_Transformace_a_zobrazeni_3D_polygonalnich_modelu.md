# Transaformace a zobrazení 3D polygonálních modelů
- Otázky: principy programovatelného vykreslovacího řetězce
- Předmět: IZG
- Zdroje:
    - https://www.fit.vutbr.cz/study/courses/IZG/private/lecture/izg_slide_transformace_rev2021_169.pdf (transformace)
    - https://www.fit.vutbr.cz/study/courses/IZG/private/lecture/izg_slide_3d_objekty_rev2021_169.pdf (reprezentace 3D)
    - https://www.fit.vutbr.cz/study/courses/IZG/private/lecture/izg_slide_viditelnost_rev2021_169.pdf (viditelnost)

## Geometrické transformace
Geometrické transformace můžeme chápat jako změnu pozice vrcholů grafického objektu (2D či 3D) v aktuálním souřadnicovém systému nebo změnu tohoto souřadnicového systému. Základem geometrické transformace jsou __lineární transformace__. Všechny základní geometrické transformace jsou lineární a jsou popsány lineárními rovnicemi:
- __Posunutí__
- __Rotace__
- __Zkosení__
- __Změna velikosti__

> Lineární transformace je zobrazení \(f\) z jednoho vektorového prostoru do druhého \(f: V \rightarrow W\), které zachovává lineární kombinace. Pro libovolné dva vektory \(x_1\) a \(x_2\) a skalár \(\alpha\) platí:
>
> \[
    f(x_1 + x_2) = f(x_1) + f(x_2) \\
    f(\alpha x_1) = \alpha f(x_1)
  \]

> Afinní transformace je zobrazení \(f\) z jednoho vektorového prostoru do druhého \(f: V \to W\), které zachovává kolinearitu (bodu ležící na přímce budou ležet na přímce i po zobrazení) a dělící poměr.
>
> Lze jej vyjádřit jako lineární transformaci následovanou posunem

__Kartézská soustava souřadnic__ je taková soustava souřadnic, u které jsou souřadné osy vzájemně _kolmé_ a protínají se v jednom bodě - _počátku soustavy souřadnic_. Soustava souřadnic může být pravotočivá nebo levotočivá

__Homogenní souřadnice__ bodu v 3D prostoru s kartézskými souřadnicemi \([x, y, z]\) je uspořádaná čtveřice \([X, Y, Z, w]\), pro kterou platí, že \(w\) je váha bodu. Lineární transformace mají váhu bodu rovnu jedné, vektory mají váhu bodu rovnu nule.

\[
    x = X/w \;\; y = Y/w \;\; z = Z/w    
\]

Bod je svými homogenními souřadnicemi určen jednoznačně. Homogenní souřadnice umožňují pracovat se všemi druhy základních transformací _jednotně_ pomocí __maticového zápisu__. Bod, který chceme transformovat, je matice \(P(x, y, z, w)\), kde \(x, y, z\) jsou jeho souřadnice a \(w = 1\) pokud je to bod nebo \(w = 0\) pokud je to vektor.

### Posunutí
Pro posun v opačném směru budou koeficienty \(d\) záporné.

Bod je reprezentovám řádkově. Transformace probíhá výpočtem BOD x MATICE. 

![Transformační matice posunutí](/Images/12/matice_posunuti.png)

### Změna velikosti
Pro koeficienty \(S > 1\) dochází ke zvětšení, pro \(0 < S < 1\) dochází ke zmenšení a pro \(S < 0\) dochází k převrácení (zrcadlení) objektu.

![Transformační matice změny velikosti](/Images/12/matice_zmena_velikosti.png)

### Rotace
Stejně jako ve 2D probíhá i ve 3D prostoru rotace okolo počátku souřadného systému. Máme různé transformační matice \(R_X\), \(R_Y\) a \(R_Z\) pro rotaci okolo různých souřadných os.

![Transformační matice rotace](/Images/12/matice_rotace.png)

Při __rotaci kolem obecné osy__ je osa rotace dána směrovým vektorem \(v\) a bodem umístění \(P\). Nelze přímo použít některou z variant základní 3D rotace. Rotaci je nutné rozložit na posloupnost několika transformací:
1. Posunutí osy do počátku souřadného systému.
2. Otočení posunuté osy do jedné ze souřadných rovin (např.: XY).
3. Otočení sklopené osy do jedné ze souřadných os (např.: X).
4. Provedení požadované rotace od ůhel \(\omega\) kolem příslušené osy.
5. Vrácení osy do původní polohy.

Maticový zápis:

\[M = T * R_x * R_z * R_{X(\omega)} * R_z^{-1} * R_x^{-1} * T^{-1}\]

Rotaci kolem obecné osy procházející počátkem lze rozložit na dílčí rotace kolem základních os - __Eulerovy úhly__. Při použití Eulerových úhlu u spojité rotace může dojít ke skokové změně některých úhlů (Gimbal lock). Nejefektivnější způsob práce s rotačními transformacemi jsou __kvaterniony__.

![Rotace kolem obecné osy](/Images/12/obecna_rotace.png)

### Zkosení
Podobně jako u rotační transformace ve 3D je transformace zkosení ve 3D rozdělena na tři různé operace podle směru, ve kterém zkosení probíhá.

![Transformační matice zkosení](/Images/12/matice_zkoseni.png)

### Skládání transformací
Jedna z nejdůležitějších vlastností transformací objektů pomocí transformačních matice je __skládání transformací__. Každá komplexní lineární transformace se dá rozložit na posloupnost základních transformací. Tato složená transformace se dá vyjádřit jednou maticí pomocí __nasobení transformačních matic__. Při skládání složené matice záleží na pořadí transformací. Při zápisu v pořadí jednotlivých transformací pak matice násobíme __zprava__ (neboli matice zapisujeme v opačném pořadí provádění operací).

## Projekce
3D grafické objekty zobrazujeme na 2D výstup (obrazovka). Je nutné transformovat ze 3D prostoru do 2D prostoru. Při transformaci projekční paprsek promítá body na průmětnu, přičemž dochází ke ztrátě informace. Existují dva základní druhy projekce:
- __Perspektivní projekce__ (středová) - Paprsky vycházejí z jednoho bodu (střed projekce, pozorovatel) a promítají se na průmětnu. Projekce nezachovává rovnoběžnost hran. Vzdálenost průmětny od středu projekce ovlivňuje velikost průmětu. Tato projekce odpovídá promítání v realitě.
- __Paralelní projekce__ (rovnoběžná) - Paprsky vycházejí kolmo ze všech bodů průmětny. Projekce zachovává rovnoběžnost hran. Vzdálenost od průmětny neovlivňuje velikost průmětu. Čím blíže je objekt středu promítání, tím je menší. Tato projekce se využívá pro technická schémata.

Paralelní promítnutí do roviny \(XY\) se provede maticí:

![Paralelní projekce](/Images/12/paraleln%C3%AD_projekce.png)

## Reprezentace 3D objektů
Existují různé způsoby reprezentace 3D grafických objektů v prostoru: konstruktivní geometrie, šablonování, dekompoziční modely, hraniční reprezentace a implicitní plochy. Pro tyto modely existují určité základní požadavky:
- __Obecnost__ - Model umožňuje popis co nejrozsáhlejší třídy objektů.
- __Úplnost__ - Model úplně popisuje daný objekt.
- __Jednoznačnost__ - Objekt lze v daném modelu vyhodnotit pouze jedním způsobem.
- __Unikátnost__ - Jednomu tělesu odpovídá pouze jeden model.
- __Přenost__ - Model umožňuje přesný popis objektu.
- __Regulérnost__ - V modelu nelze vytvořit nereálnou reprezentaci.
- __Konzistence__ - Vybrané operace tělesa stejné třídy se chování vždy stejně.
- __Kompaktnost__ - Malá paměťová náročnost modelu.
- __Efektivní zpracování__ - Model umožňuje efektivní implementaci operací s tělesem.

Existují dva základní typy 3D objektů:
- _Manifold_ objekty - Hrany objektu sdílí vždy jen dvě stěny. Tyto objekty jsou vyrobitelné.
- _Nonmanifold_ objekty - Nevyrobitelné objekty.

Pro kontrolu topologie objektu (toho, že objekt je manifold) se používají __Eulerovy rovnice__. Ty kontrolují, že hrana spojuje vždy dva vrcholy, ve vrcholu se potkávají maximálně tři hrany a žádný stěny se neprotínají. Pro každý manifold objekt bez otvorů platí: _počet vrcholů - počet hran + počet stěn = 2_.

### Konstruktivní geometrie (CSG)
V konstruktivní geometrii je objekt popsán _stromem_ složeným z:
- 3D primitiv (základní 3D tělesa) - listy stromu
- Transformací 3D primitiv - uzly stromu
- Booleovských operací - uzly stromu

Pro přidání každé nové operace je nutná regenerace tohoto stromu. Nejsou zde žádné informace o povrchu, a tak je nutné objekty převést na polygonální modely. Používají se ve strojním inženýrství a architektuře. Pro zlepšení výkonu ve velkých stromech se používají optimalizace jako _oktalové stromy_, které urychlují regeneraci a zobrazování CSG modelu.

### Šablonování
Šablonování vytváří objekt pohybem křivy, plochy nebo tělesa po zvolené trajektorii. Může být součástí CSG operací (primitiva vytvořená šablonováním). Existují dva druhy šablonování:
- __Translační šablonování__ - Pohyb po přímce nebo obecné křivce.
- __Rotační šablonování__ - Pohyb po kružnici s využitím vlastností NURBS křivek.

### Dekompoziční modely
Objekt je popsán diskrétně pomocí dekompozice na elementární objemové jednotky - __voxely__ (krychle, hranoly). Je vhodný pro popis objemových diskrétních objektů (mlha, mraky). Využívá se v geologii, medicíně a strojírenství. Data jsou uložena buď jako _3D pole_ diskrétních hodnot (rychlé ale paměťově náročné) nebo jako _oktalový strom_ (rekurzivní dělení krychle na menší částí). Dekompoziční modely se vykreslují pomocí algoritmu __Marching cubes__, který převádí objemové data na polygonální model.

### Hraniční reprezentace
Hraniční reprezentace je nejčastější reprezentace komplexních 3D objektů. Existuje několik modelů hraniční reprezentace:
- __B-rep__ (boundary representation) - Objekt je popsán prostřednictvím svého povrchu. Informace o jeho vnitřní struktuře není uložena. Objekty jsou definovány pomocí tří základních prvků: __vrcholů__, __hran__ a __stěn__.
- __Drátový model__ - Objekt je popsán pouze pomocí vrcholů a hran. Obsahuje málo topologických informací a tudíž je _nejednoznačný_.
- __Polygonální model__ - Objekt je definován pomocí vrcholů, hran a stěn. Využívá rozdělení objektu na trojúhelníky (polygony). Je to jednoznačný popis objektu, ale má malou přesnost (lineární aproximace povrchu). Pro reprezentaci polygonálního modelu se používá datová struktura __okřídlená hrana__. V počítačích je HW podpora zobrazení polygonálních objektů.
- __Hraniční spline model__ - Objekt je definován pomocí vrcholů, hran (křivek) a stěn (spline plochy). Model je vhodný pro přesné geometrické modelování, přesnost modelu je dána přeností aproximace. Nutnost dodržovat a ověřovat uzavřenost.

## Viditelnost objektů ve 3D
V 3D prostoru jsou viditelné ty plochy, které jsou přivráceny k pozorovateli. Přivrácené části mají normálu směrem k pozorovateli. Viditelnost _hran_ je rozdělena do tří případů:
- Hrana mezi viditelnými plochami je potenciálně viditelná.
- Hrana mezi neviditelnými plochami je neviditelná.
- Hrana mezi viditelnou a neviditelnou plochou je obrysová.

Jsou dva základní druhy _algoritmů viditelnost_:
- __Vektorové algoritmy viditelnosti__ - Jejich výsledkem je soubor viditelných a neviditelných hran.
- __Rastrové algoritmy viditelnosti__ - Jejich výsledkem je obraz viditelných ploch, barva, osvětlení, stínování...

### Robertsův algoritmus
Robertsův algoritmus je vektorový algoritmus viditelnosti. Dělí potenciálně viditelné hrany na úseky, kde se mění velikost. Těmto hranám se vytvoří průsečíky s obrysovými hranami a následně testujeme viditelnost jejich úseků podle vzdálenosti průsečíků a zakrytí.

### Plovoucí algoritmus
Plovoucí algoritmus se používá k vizualizaci grafů.

### Malířův algoritmus
Malířův algoritmus je rastrový objektový algoritmus řešení viditelnosti. Objekty jsou seřazeny podle vzdálenosti od kamery a vykreslují se od zadu dopředu. Nastává problém s cyklicky se překrývajícími objekty. Tento problém lze řešit rozdělením objektu na více částí.

### Z-buffer
Z-buffer je rastrový obrazový algoritmus řešení viditelnosti. Udržuje se __paměť hloubky__ (z-buffer), který obsahuje Z-souřadnice nejbližších bodů ploch. Z-buffer má stejné rozměry jako zobrazovací buffer, počítá se pro každý pixel obrazovky. Každá plocha je zpracována pouze jednou - fronta. Je to rychlý algoritmus se snadnou implementací v HW:

### Ray-casting
Ray-casting je rastrový obrazový algoritmus řešení viditelnosti. Vrhá paprsky z místa pozorovatele skrze každý pixel obrazovky. Pro každý paprsek počítáme na jakých souřadnicích protíná objekty podél jeho dráhy. Zobrazí se pak část nejbližšího objektu. Algoritmus je pomalý, ale má kvalitní výsledky. Má náročnou HW realizaci. Používá se pro zobrazení CSG modelů, implicitních ploch atd.

### Radiozita
Algoritmus radiozita je nejkomplexnější algoritmus řešení viditelnosti. Vystřeluje "radiozity" z plošek, které mají nejvíce energie. Ozářené plošky se stávají sekundárními zdroji světla. Toto se rekurzivně opakuje, dokud se energie neutlumí. Je to nejpomalejší algoritmus, ale zohledňuje fyzikální vlastnosti světla.

## Osvětlovací modely
Pro kalkulaci světla, stínů a odrazů na objektech ve 3D prostoru se používají různé osvětlovací modely.

### Lambertův osvětlovací model
Lambertův osvětlovací model je empirický model, který počítá pouze s difuzí. Difuzi aproximuje na ideální difuzi, při níž se paprsek při dopadu odrazí půlkruhově do všech směrů. Intenzita difuze závisí na úhlu dopadu paprsku na povrch (kosínové pravidlo).

### Phongův osvětlovací model
Phongův osvětlovací model je empirický model, který počítá jak s difuzí tak s reflexí. Počítá s ideální reflexí, při níž je odraz světla symetrický podle normály. Intenzita reflexe závisí na směru odrazu a směru k pozorovateli. Využívá ambientní složku světla IA, světelný šum a rozptýlené světelné pozadí.

### BRDF
BRDF je fyzikálně založený model. Umožňuje realistické zobrazení pomocí technologie _Ray-tracing_. Specializován na jednotlivé efekty nebo materiály. Je výpočetně nejnáročnější.

### Stínování
Existuje několik modelů stínování polygonálních 3D objektů:
- __Flat shading__ - Pro každý polygon se osvětlovacím model vyhodnotí středový pixel. Celý polygon má pak konstantní barvu. Nezohledňuje se zakřivení povrchu objektu.
- __Goraud shading__ - Pro každý polygon se osvětlovacím modelem vyhodnotí pixely ve vrcholech. Při rasterizaci polygonu probíhá interpolace barvy. Zohledňuje se zakřivení povrchu objektu.
- __Phong shading__ - Při rasterizaci probíhá interpolace normál z vrcholů. Osvětlovací model se pak počítá pro každý pixel polygonu. Zohledňuje se zakřivení povrchu objektu. Má velmi kvalitní výsledky, realistické zobrazení.

## Vykreslovací řetězec
![Vykreslovací řetězec](/Images/12/gpu_pipeline.png)
