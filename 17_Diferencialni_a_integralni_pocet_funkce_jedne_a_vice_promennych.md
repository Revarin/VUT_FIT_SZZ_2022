# Diferenciální a integrální počet funkce jedné a více proměnných
- Otázky:
- Předmět: IMA1, IMA2
- ToDo: Kontrola, příklady
- Zdroje:
    - https://wis.fit.vutbr.cz/FIT/st/cfs.php.cs?file=%2Fcourse%2FIMA1-IT%2Ftexts%2FIma.pdf&cid=14033 (skripta)

## Diferenciální a integrální počet
Diferenciální počet zkoumá změny funkčních hodnot dle změn nezávislé proměnné. Tedy například hledání extrémů na intervalu funkce. Integrální počet slouží k určení funkce, je-li známa její derivace nebo k výpočtu plochy vymezené grafem funkce.

## Limita
Limita je konstrukce vyjadřující, že se funkční hodnota funkce v bodě \(a\) blíží číslu \(b\)

\[\lim_{x \to a} f(x) = b\]

> Řekneme, že funkce \(f\) má v bodě \(a\) __limitu__ \(b\), když:
> - Bod \(a\) je hromadným bodem množiny \(D_f\) (to je bod, v jehož libovolně redukovaném okolí leží alespoň jeden bod dané množiny).
> - K libovolnému ukolí \(U(b)\) limity \(b\) existuje okolí \(U(a)\) bodu \(a\) tak, že funkce \(f\) zobrazí redukované okolí \(U^*(a)\) do \(U(b)\), tedy:
>
> \[\forall U(b)\; \exist U(a):\; U^*(a) \subset f^{-1}(U(b))\]
>
> Potom píšeme \(\lim_{x \to a} f(x) = b\).

![Okoli bodu](/Images/17/okoli_bodu.png)

Limita je __vlastní__, pokud platí \(b \neq \pm \infty\), jinak je to limita __nevlastní__. Rozlišujeme limitu __zprava__ \(\lim_{x \to a^+} f(x)\) a limutu zleva \(lim_{x \to a^-} f(x)\).

### Spojitost funkce
Funkce \(f(x)\) je __spojitá__ v bodě \(a\), pokud platí \(\lim_{x \to a} f(x) = f(a)\), jinak je funkce __nespojitá__. Existuje několik druhů nespojitosti:
- __Odstranitelná nespojitost__ - Nespojitost je odstranitelná pokud pro bod nespojitosti platí \(f(a^+) = f(a^-)\) (existují obě jednostranné limity a rovnají se).
- __Nespojitost prvního druhu__ - Nespojitost prvního druhu vzniká, jestliže existují obě jednostranné limity, které jsou konečné, ale nejsou si rovny.
- __Nespojitost druhého druhu__ - Nespojitost druhého druhu vzniká, jestliže alespoň jedna z jednostranných limit je nevlastní nebo neexistuje. Například se jedná o bod nespojitosti v nule.

## Derivace
> V bodě \(x_0\) nechť pro funkci definovanou na nějakém okolí \(U(x_0)\) existuje vlastní limita \(f'(x_0) = \lim_{x \to x_0} \frac{f(x) - f(x_0)}{x - x_0}\), potom tuto limitu nazýváme derivací funkce \(f\) v bodě \(x_0\).
>
> Derivaci funkce \(f\) v bode \(x_0\) značíme \(f'(x_0)\).

![Graf derivace](/Images/17/graf_derivace.png)

Grafická význam derivace:
1. K pevně zvolenému bodu \(A[x_0, f(x_0)]\) si v jeho blízkosti zvolíme bod \(B[x, f(x)]\).
2. Vzniklá _sečna_ \(AB\) ve směrnicovém tvaru \(y = kx + q\) má směrnici \(\tan \alpha = \frac{f(x) - f(x_0)}{x - x_0}\).
3. Následně limitním přechodem zvolíme pozici bodu \(B\) nekonečně blízko tak, že se sečna funkce \(AB\) změní v _tečnu_. Směrnice tečny bude nyní \(k = \lim_{x \to x_0} \frac{f(x) - f(x_0)}{x - x_0}\) -> __derivace__ v bodě \(x_0\).
4. Jinými slovy: derivace funkce je změna její hodnoty v poměru ke změně jejího argumentu.

V některých bodech funkce nemusí mít definovanou derivace. Derivace neexistuje v bodech nespojitosti nespojitých funkcí a také v některých speciálních bodech spojitých funkcí. Z toho plyne, že pokud je funkce v daném bodě _diferencovatelná_, je v tomto bodě spojitá.

![Derivace neexistuje a funkce je spojitá](/Images/17/neex_derivace_spojita.png)
![Derivace neexistuje a funkce je nespojitá](/Images/17/neex_derivace_nespojita.png)

### Derivační vzorce
![Vzorce pro derivace](/Images/17/vzorce_derivace.png)

### L'Hospitalovo pravidlo
__L'Hospitalovo pravidlo__ je pravidlo pro výpočet limity se zlomkem. Výpočet limity se může provést derivací čitatele a jmenovatele zvlášť

> Mějme limitu \(y = \lim_{x \to a} \frac{f(x)}{g(x)};\; f(a) = g(a) = 0\;nebo\;\pm\infty\). Potom lze limitu spočítat jako \(y = \lim_{x \to a} \frac{f'(x)}{g'(x)}\).

Funkce, jejíž limitu v daném bodě počítáme, musí mít tvar zlomku, jinak pravidlo nelze použít. Pokud po dosazení limitní hodnoty do čitatele a jmenovatele vyjdou oba nula nebo nekonečno, můžeme použít toto pravidlo. Při výpočtu je možné použít L'Hospitalovo pravidlo i vícekrát (kroky se mohou opakovat).

### Derivace vyšších řádů
Provedeme-li __n-krát__ derivaci funkce \(f(x)\) po sobě, dostaneme derivaci __n-tého__ řádu. Např.: \(f''(x) = \frac{d^2 f}{f x^2}\) značí derivaci druhého řádu.

### Využití derivací pro analýzu průběhu funkce
Derivaci funkce lze využít pro určení průběhu funkce. Při dosazení daného bodu do rovnice funkce v _derivaci prvního řádu_ lze podle znaménka výsledku určit _směr_ funkce:
- __Rostoucí funkce__ - Její první derivace je větší nebo rovna nule.
- __Klesající funkce__ - Její první derivace je menší nebo rovna nule.
- __Lokální extrémy__ - Bod, v němž je první derivace funkce rovna nule, může být lokální extrém. V lokálním maximu/minimu je derivace funkce rovna nule - __stacionární bod__, ale nulová derivace nemusí znamenat lokální extrém. Pokud pro stacionární bod platí:
    - \(f'(x) = 0 \land f''(x) > 0\) je v daném bodě _lokální minimum_.
    - \(f'(x) = 0 \land f''(x) < 0\) je v daném bodě _lokální maximum_.

_Derivací druhého řádu_ lze podle znaménka výsledku určit _tvar_ funkce:
- __Konkávní funkce__ - Její druhá derivace je menší nebo rovna nule. Funkce je vypouklá od osy x.
- __Konvexní funkce__ - Její druhá derivace je větší nebo rovna nule. Funkce je vpuklá k ose x.
- __Inflexní body__ - Bod, v němž je druhá derivace funkce rovna nule, se nazývá inflexní bod. V inflexním bodu se funkce mění z konvexní na konkávní a naopak.

![Průbeh funkce](/Images/17/prubeh_funkce.png)

Přímka, ke které se graf funkce \(f(x)\) nekonečně blíží se nazývá __asymptota grafu funkce__. Jsou dva druhy asymptot:
- __Asymptota bez směrnice__ (vertikální) - Potenciální body v nichž se nachází asymptota bez směrnice jsou body vyloučené z definičního oboru. Pro ověření se v daném bodě spočítá limita zleva a zprava. Pokud vyjdou \(\pm \infty\), tak se v daném bodě nachází asymptota.
- __Asymptota se směrnicí__ - Je to přímka, která není rovnoběžná s osou \(y\). Mohou být maximálně dvě pro jednu funkci. Pro její určení hledáme přímku \(y = kx + q\), kde:

\[
    \lim_{x \to \pm \infty} [f(x) - (ax + b)] = 0    
\]

## Integrály
Integrál je inverzní operace k derivaci na intervalu. Pokud nespecifikujeme interval, tak máme __neurčitý integrál__.

> Říkáme, že \(F(x)\) je v intervalu \((a,b)\) __primitivní funkcí__ k funkci \(f(x)\), jestliže pro všechny \(x \in (a,b)\) platí \(F'(x) = f(x)\). Ke každé funkci \(f(x)\) spojité na intervalu \((a,b)\) existuje v \((a,b)\) nekonečně mnoho primitivních funkcí. Je-li \(F(x)\) jedna z těchto primitivních funkcí, pak všechny ostatní mají tvar
>
> \[F(x) + C\]
>
> kde \(C\) je __integrační konstanta__, která je libovolná.

> Používáme formální zápis
>
> \[\int f(x) dx = F(x) + C\]
>
> \(\int f(x) dx\) značí _množinu_ všech promitivních funkcí k funkcí \(f(x)\) a nazývá se __neurčitý integrál__ funkce \(f(x)\).

### Integrační vzorce
![Vzorce integrace](/Images/17/vzorce_integrace.png)

### Řešení integrálů
Existuje několik metod výpočtu neurčitých integrálů:
- __Přímá integrace__ - Přímé využívání vzorců integrace.
- __Metoda Per Partes__ - Metoda integrace po částech. Volíme \(u\) a \(u'\) tak, aby se derivování zjednodušilo a \(v'\) šlo integrovat.

![Příklad metody Per Partes](/Images/17/per_partes.png)

- __Substituční metoda__ - Hledáme výhodnou substituci.

![Příklad substituční metody](/Images/17/substitucni_metoda.png)

### Určitý integrál
> Je-li
>
> \[\overline{\int_{a}^{b}} f(x)dx = \underline{\int_{a}^{b}} f(x)dx\]
>
> pak společné hodnotě těchto integrálů říkáme integrál z funkce \(f(x)\) v intervalu \(\langle a,b \rangle\) a o funkci \(f(x)\) říkáme, že je v \(\langle a,b \rangle\) integrovatelná ve smyslu _Riemannovy definice_.

Pro výpočet určitého integrálu je zásadní __Newtonova-Liebnizova formule__
> Je-li funkce \(f(x)\) spojitá na intervalu \(\langle a,b \rangle\) a je-li \(F(x)\) primitivní funkce k \(f(x)\) ma intervalu \(\langle a,b \rangle\) a na tomto intervalu spojitá, potom platí:
>
> \[\int_a^b f(x)dx = [F(x)]_a^b = F(b) - F(a)\]

Určitým integrálem je možné spočítat obsah plochy ohraničené funkcí \(f(x)\) na daném intervalu \(\langle a,b \rangle\). Pokud počítáme plochu pro prostor daný dvěma funkcemi, výslednou plochu dostaneme rozdílem jejích integrálů:

\[
    \int_a^b(f(x) - g(x))dx    
\]

I zde je možné použít metody _Per Partes_ a _substituce_ pro výpočet integrálů, jenom se provádí dosazení po integraci:
- Per Partes pro spojité integrály: \(\int_a^b u(x)v'(x)dx = [u(x)v(x)]_a^b - \int_a^b u'(x)v(x)dx\)
- Substituce pro spojité integrály: \(\int_a^b f(g(x))g'(x) dx = \int_{g(a)}^{g(b)} f(t)dt\)

## Funkce více proměnných
Funkce více proměnných jsou reálné funkce s \(n\) reálnými proměnnými \(f:\; R^n \rightarrow R,\; f(x,y,z)\; pro\; R^3\). Každému \(x \in R^n\) přiřadí nejvíce jedno \(f(x) \in R\). Skládá se z _bodů_, _definičního oboru_, _oboru hodnota_ a _grafu_.

U funkcí dvou proměnných nazýváme části grafu se shodnou hodnotou \(f(x,y)\) __vrstevnicemi__. U funkcí s obecně \(n\) proměnnými nazýváme množinu bodů se stejnou funkční hodnotou __hladinami__. Pojmy okolí, limita, hromadný bod, spojitost atp. jsou definovány podobně jako v jednorozměrném prostoru.

![Vrstevnice](/Images/17/vrstevnice.png)

U n-rozměrných prostorů nedefinujeme obecně tečnu jako přímku, ale jako (n-1)-rozměrný prostor. Ve 3D prostoru se tak jedná o __tečnou rovinu__. _Parciální derivace_ ve 3D neurčují směrnici tečné přímky, ale právě určují tečné roviny - proto jsou dvě.

_Limity_ funkcí více proměnných se formálně definují stejně jako pro funkci jedné proměnné. Fungují podobně jako u funkcí jedné proměnné, jen je okolím kruh o poloměru.

## Derivace podle více proměnných
Derivaci podle více proměnných se říká __parciální derivace__. Parciální derivaci prvního řádu podle proměnné \(x\) získáme klasickou derivací funkce v daném bodě. Všechny ostatní proměnné (mimo \(x\)) považujeme za konstanty.

Derivovat je také možné podle vektoru. Tomu se říká __směrová derivace__ - derivuje se ne podle osy, ale podle libovolného směrového vektoru.

### Gradient
__Gradient__ je vektor, který udává směr, ve kterém funkce v daném bodě roste nejrychleji. Je kolmý na vrstevnici. Gradient je výsledkem derivace funkce více proměnných (derivace v podobě vektoru). Např.: pokud máme funkci pro dvě proměnné a derivujeme nejprve podle \(x\) a pak podle \(y\) tak složením výsledných derivací do vektoru vznikne gradient.

Body, ve kterých je gradient _nulový vektor_ (všechny parciální derivace jsou nulové) se nazývají __stacionárními body__.

### Taylorova řada
[TODO:Is_Neccessary]

### Derivace vyšších řádů
Derivace vyšších řádů se provádí podobně jako u funkcí jedné proměnné. U funkcí více proměnných mluvíme o __totálním diferenciálu__. Vyjadřuje závislost změny hodnoty funkce na malé změně jejího argumentu. Tuto závislost aproximuje jakou přímou úměrnost v okolí daného bodu.

## Dvojný a trojný integrál
Integrál funkce více proměnných počítáme jako několik jednoduchých integrálů. Analogicky se počítají jak určité tak neurčité integrály. Dvojné a trojné integrály se používají k výpočtu objemu těles.

Pro výpočet dvojného integrálu na daném intervalu se používá __Fubiniho věta__:

\[
    V = \int_a^b F(X)dx = \int_a^b [\int_c^d f(x,y)dy]dx = \int_c^d [\int_a^b f(x,y)dx]dy    
\]

## Další pojmy
- __Okolí__ bodu \(a \in \R\) - \(U(a, \epsilon) = {x \in \R|\; |x-a| < \epsilon} = (a - \epsilon) \cup (a + \epsilon)\)
- __Redukovaný okolí__ bodu - \(U^*(a, \epsilon) = u(a, \epsilon) - {a}\) - okolí daného bodu bez tohoto bodu.

- __Otevřená množina__ - Množina, která neobsahuje žádný bod ze své hranice.
- __Uzavřená množina__ - Množina, která obsahuje všechny body ze své hranice.
- __Vnitřní bod__ - Bod uvnitř množiny.
- __Hraniční bod__ - Bod na hranici množiny.
- __Hranice množiny__ - Množina všech hraničních bodů.
## Příklady
[TODO]
