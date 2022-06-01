# Minimalizace logickych vyrazu
- Otázky: algebraicke metody, Karnaughova mapa, Quine McCluskey
- Předmět: INC
- Zroje:
    - https://wis.fit.vutbr.cz/FIT/st/cfs.php.cs?file=%2Fcourse%2FINC-IT%2Flectures%2F10-booleova_algebra-minimalizace.pdf (p.27)

## Minimalizace logických obvodů
Procesor a všechny jeho součásti jsou implementovány pomocí logických obvodů. Logické obvody se skládají z hradel, které něco stojí a zabírají určité místo na čipu. Je tedy žádoucí logické výrazy a obvody co nejvíce __minimalizovat__. Kritéria minimalizace v reálných obvodech je _velikost obvodu_ (počet hradel), _zpoždění obvodu_ (rychlost), _počet proměnných_ (počet vodičů) a další. Existuje několik __metod minimalizace:__
- __Algebraické metody__ - Aplikace axiomů _Booleovy algebry_, nicméně jsou náročné pro velké výrazy.
- __Grafické metody__ - Vennovy diagramy, Karnaughova mapa, jednotková krychle...
- __Aritmetické metody__ - Quine-McCluskey

Tyto metody nejčastěji začínají s __pravdivostní tabulkou__. V této tabulce jsou zapsány všechny kombinace stavů vstupních proměnných (všechny _vstupní stavy_) a jejich výstupní hodnoty. Každý stav je označen _stavovým indexem_ (_s_), což je vlastně desítkové číslo udávající hodnotu logického stavu.

![Pravdivostní tabulka](/Images/08/pravdivostni_tabulka.png)

Logický výraz se skládá z __termů__. Term je uspořádaná skupina _proměnných_ a _operátorů_. Pokud má logický výraz definovanou výstupní hodnotu pro všechny kombinace vstupů, nazývá se __určená logická funkce__. Naproti tomu, pokud je alespoň jedna výstupní hodnota neurčená (__hodnota X__), tak je výraz __neurčená logická funkce__.

### Normální formy
Logické funkce mohou být zapsány v několika speciálních formách:
- __Úplná normální disjunktní forma__ (UNDF) - Výraz je zapsán jako suma součinů. V jednotlivých součinech (termech, _implikantech_) se vyskytují všechny proměnné dané funkce. Pro každou funkci existuje jenom jedna UNDS. Disjunktní formy se tvoří tak, že se sepisují jen vrcholy funkce, ve kterých funkce nabývá hodnoty log. 1 (Př.: \(((x_1 \land x_2) \lor (\neg x_3 \land x_4))\)).
    - __Zkrácená normální disjunktní forma__ - Částečně minimalizovaná UNDF.
    - __Minimální normální disjunktní forma__ (MNDF) - Funkce, u které již nelze eliminovat žádnou proměnnou z termu. Takovýchto forem může existovat více.
- __Úplná normální konjunktní forma__ (UNKF) - Výraz je sepsán jako součin sum. V jednotlivých součtech (termech, _implicentech_) se vyskytují všechny proměnné dané funkce. Pro každou funkci existuje jenom jedna UNKF. Konjunktní formy se tvoří tak, že se sepisují jen vrcholy funkce, ve kterých funkce nabývá hodnoty log. 0 (Př.: \(((x_1 \lor x_2) \land (\neg x_3 \lor x_4))\)).
    - __Zkrácená normální konjunktní forma__ - Částečně minimalizovaná UNKF.
    - __Minimální normální konjunktní forma__ (MNKF) - Funkce, u které již nelze eliminovat žádnou proměnnou z termu. Takovýchto forem může existovat více.

## Algebraická minimalizace
Při algebraické minimalizaci je logický výraz minimalizován pomocí __Booleových axiomů__ a __De Morganových zákonů__. Tyto axiomy a zákony jsou blíže popsány v okruhu __[20]__.

![Axiomy Booleovy algebry](/Images/08/boolovy_axiomy.png)
![De Morganovy zákony](/Images/08/boolovy_de_morgan_zakony.png)

Algebraická minimalizace je možná především díky __Boolovské sousednosti__. Ta umožňuje eliminovat proměnné, které se v jednom výrazu vyskytují jak v přímé, tak v komplementární formě.

\((a.b) + (a.\neg b) = a\)

\((a+b) . (a+\neg b) = a\)

## Karnaughova mapa
Karnaughova mapa je grafická metoda minimalizace logického výrazu. Je vhodná především pro výrazy s dvěma až čtyřmi proměnnými. Vytvoří se matice, jejíž pole budou představovat všechny možné kombinace hodnot vstupních proměnných. Do těchto polí se zapíšou výstupní hodnoty výrazu při této kombinaci vstupů.

Následně sdružujeme pole matice se stejnou hodnotou do skupin o velikosti mocniny 2 (2, 4, 8...). Pole lze sdružovat i přes okraje a rohy. Pokud je nějaký výstup výrazu nedefinovaný, můžeme ho považovat za hodnotu, která se nám hodí. Záleží v jaké formě se logický výraz snažíme minimalizovat. Pokud minimalizujeme Karnaughovu mapu v __disjunktivní formě__ tak sdružujeme jedničky, pokud minimalizujeme v __konjunktivní formě__ tak sdružujeme nuly. Výsledek pak můžeme zapsat v normální formě jako kombinaci těch vstupních proměnných, které mají v dané skupině stále stejnou hodnotu.

V buňkách matice pod pruhem má daná proměnná hodnotu log. 1, v buňkách mimo pruh má daná proměnná hodnotu log. 0.

![Karnaughova mapa v disjunktivní formě](/Images/08/karnaugh_disjunktni.png)
![Karnaughova mapa v konjunktivní formě](/Images/08/karnaugh_konjunktni.png)

## N-rozměrná jednotková krychle
N-rozměrná jednotková krychle je grafická metoda minimalizace jednoduchého logického výrazu. Je názorná pro výrazy s třemi proměnnými. Jednotlivé vrcholy krychle jsou uspořádány tak, aby byly _booleovsky sousedné_ (aby se jejich hodnota měnila jen v jedné proměnné). V krychly je tak jeden vrchol zvolen jako počátek, kde mají všechny proměnné stejnou hodnotu a každý směr z tohoto počátku pak značí změnu hodnoty jedné proměnné.

![3-Rozměrná jednotková krychle](/Images/08/n-rozmerna_krychle.png)

## Minimalizační metoda Quine-McCluskey
Minimalizační metoda Quine-McCluskey je _tabulární minimalizační_ metoda vhodná pro větší funkce. Je založena na systematické hledání boolovsky sousedních vrcholů logické funkce. Metoda je vhodná i pro funkce s více proměnnými, kde Kernaughovy mapy a jednotkové krychle selhávají, a pro minimalizaci obvodů s více výstupy. Minimální pokrytí se následně hledá například pomocí __mřížky implikantů__ nabo __Petrickovy funkce__.

### Pojmy
- __Úplný implikant__ - Term UNDF, který obsahuje všechny proměnné dané logické funkce.
    - __Pokrácený implikant__ - Term, který má některé boolovsky sousední proměnné eliminované.
    - __Zkrácený implikant__ - Term, který má všechny boolovsky sousední proměnné eliminované. Po odstranění jakékoliv další proměnné by přestal být implikantem. Obvod sestavený z pouze zkrácených implikantů nemá hazardy.
- __Množina minimálních implikantů__ - Je množina obsahující zkrácené implikanty.
- __Minimální řešení funkce__ - Je jedna nebo více podmnožin množiny minimálních implikantů. Může zároveň existovat i více ekvivalentních řešení, které mohou mít různé další vlastnosti.
    - __Nesporný implikant__ - Zkrácený implikant, který bude vždy součástí minimálního řešení.
    - __Volitelný implikant__ - Zkrácený implikant, který může, ale nemusí být součástí minimálního řešení pokud lze použít jiný zkrácený implikant.
- __Mřížka implikantů__ - Mřížka implikantů představuje grafické znázornění pokrytí vrcholů funkce, které umožňuje přehledné hledání minimálního pokrytí dané funkce zkrácenými implikanty nalezenými pomocí metody Quine-McCluskey.
- __Petrickova funkce__ - Algoritmus nalezení minimálního pokrytí aritmeticky. Funkce umožňuje nalezení optimálního řešení, její složitost však narůstá s počtem zkrácených implikantů.

### Postup pro UNDF
1. Seřadíme do řádků tabulky jednotlivé implikanty v pořadí dle jejich vah a počtu jedniček jejich binárních vah. Tímto dostáváme skupiny booleovsky sousedních implikantů.
2. Provedeme hledání a soupis do skupin všech boolovsky sousedních implikantů mezi jednotlivými skupinami v tabulce.
    - V tabulce označíme eliminovanou proměnnou pomlčkou.
    - Opakujeme krok 2 pro skupiny vytvořené v kroku 2 tam, kde existuje další boolovská sousednost.
    - Pokud některý z implikantů nemá další boolovsky sousední implikanty, nazýváme jej zkrácený implikant.
3. Následně hledáme minimální řešení pokrytí dané funkce pomocí __mřížky implikantů__.

![Příklad postupu](/Images/08/quine_mccluskey_postup.png)

### Mřížka implikantů
Mřížka implikantů představuje grafické znázornění pokrytí vrcholů funkce, které umožňuje přehledné hledání minimálního pokrytí dané funkce zkrácenými implikanty nalezenými pomocí metody Quine-McCluskey. V této mřížce jsou jako řádky zapsané všechny poteciální zkrácené implikanty (_volitelné implikanty_) a sloupce jsou všechny elementární implikanty, které pokrývají.

Při řešení je nejdříve nutné zahrnout _nesporné implikanty_ - elementární implikanty pokryté pouze jedním volitelným implikantem. Následně se hledá co nejmenší množina volitelných implikantů, která pokrývá všechny zbylé elementární implikanty. Tato výsledná množina představuje výsledek minimálního pokrytí pomocí zkrácených a nesporných implikantů.

![Mřížka implikantů](/Images/08/mrizka_implikantu.png)
![Řešení mřížky implikantů](/Images/08/mrizka_implikantu_reseni.png)

### Petrickova funkce
Petrickova funkce je algoritmus nalezení minimálního pokrytí aritmeticky. Funkce umožňuje nalezení optimálního řešení, její složitost však narůstá s počtem zkrácených implikantů. Postup Petrickovy funkce je následující:
1. Vhodným způsobem se naleznou všechny zkrácené implikanty (Quine-McCluskey).
2. Pomocí mřížky implikantů se identifikují všechny _nezbytné implikanty_.
3. Pro zbývající zkrácené implikanty se napíše normální konjunktivní formou logický výraz, reprezentující všechny možná pokrytí následovně:
    - Pro každý nepokrytý implikant se zapíše výraz jako suma zkrácených implikantů, které jej pokrývají.
    - Výsledné sumy se zapíšou jako součin - vznikne tak konjunktivní forma.
4. Vzniklý zápis v konjunktní formě se přepíše na disjunktní (prosté roznásobení).
5. Tento výraz se zjednodušší pomocí teorémů Boolovy algebry.
6. Každý vzniklý term představuje jedno možné pokrytí
7. Z těchto termů vybereme pokrytí s nejnižší cenou, kde cenou rozumíme počet zkrácených implikantů a počet proměnných v každém zkráceném implikantu.

## Příklady
UNDF, UNKF, Karnaughova mapa, Quine-McCluskey, Mřížka implikantů
