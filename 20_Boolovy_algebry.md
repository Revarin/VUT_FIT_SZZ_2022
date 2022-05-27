# Boolovy algebry
- Otázky:
- Předmět: INC, IDM
- ToDo: Příklady
- Zdroje:
    - https://wis.fit.vutbr.cz/FIT/st/cfs.php.cs?file=%2Fcourse%2FINC-IT%2Flectures%2F10-booleova_algebra-minimalizace.pdf (booleova algebra)
    - https://www.umat.fekt.vut.cz/~hlinena/IDM/Prednasky/algebra.pdf (algebra obecně)

## Boolova algebra
Algebra definuje množinu prvků, množinu operátorů nad těmito prvky, axiomy a teorémy. __Boolova algebra__ je šestice \((B, +, *, ', 0, 1)\), kde:
- \(B\) je neprázdná množina s alespoň dvěma různými prvky.
- \(+\) je logický součet (binární operace OR, sjednocení).
- \(*\) je logický součin (binární operace AND, průnik).
- \('\) je komplement (doplněk).
- \(0\) je nejmenší (nulový) prvek, \(0 \in B\).
- \(1\) je největší (jedničkový) prvek, \(1 \in B\).

> Buď \((X, \lor, \land)\) distributivní komplementární svaz s nejmenším prvkem \(0 \in X\) a největším prvkem \(1 \in X\). Pak \((X, \lor, \land)\) nazýváme _Booleovým svazem_. Uspořádanou šestici \((X, \lor, \land, -, 0, 1)\), kde \(-: X \rightarrow X\) je operace komplementu v \(X\), nazýváme _Booleovou algebrou_ na \(X\).

## Axiomy Boolovy algebry
Axiomy jsou základní, natvrdo daná, pravidla, která definují vlastnosti algebry. Boolova algebra má následující axiomy:
- __Uzavřenost__ - Výsledky logických operací nad prvky množiny \(B\) také patří do množiny \(B\).

\[
    (a + b) \in B \;\text{ (I.a)} \\
    (a * b) \in B \;\text{ (I.b)}
\]

- __Neutralita prvků 0 a 1__ - Výsledek logické operace proměnné \(a\) s neutrálním prvkem je opět proměnná \(a\).

\[
    a + 0 = a \;\text{ (II.a)} \\
    a * 1 = a \;\text{ (II.b)}
\]

- __Zákony komutativní__ - Nezáleží na pořadí prvků.

\[
    a + b = b + a \;\text{ (III.a)} \\
    a * b = b * a \;\text{ (III.b)}
\]

- __Zákony distributivní__ - Logickou operaci je možné distribuovat přes jinou operaci.

\[
    a + (b * c) = (a + b) * (a + c) \;\text{ (IV.a)} \\
    a * (b + c) = (a * b) + (a * c) \;\text{ (IV.b)}
\]

- __Existence komplementu__ - Ke každému prvku existuje prvek, který má následující vlastnosti:

\[
    a * a' = 0 \;\text{ (V.a)} \\
    a + a' = 1 \;\text{ (V.b)}
\]

- __V množině \(B\) existují alespoň dva různé prvky__ (VI)

### Teorémy Boolovy algebry
Teorémy jsou další pravidla, která jsou odvozena z axiomů algebry a definují další užitečné vlastnosti algebry. Boolova algebra má následující teorémy:
- __Asociativní zákony__ - V rámci jedné logické operace nezáleží na závorkách.

\[
    (a + b) + c = a + (b + c) \;\text{ (XIII.a)} \\
    (a * b) * c = a * (b * c) \;\text{ (XIII.b)}
\]

- __Idempotence__ - Jakákoliv logická operace proměnné \(a\) se sebe samou má za výsledek tu samou proměnnou \(a\).

\[
    a + a = a \;\text{ (VIII.a)} \\
    a * a = a \;\text{ (VIII.b)}
\]

- __Agresivita 1 a 0__

\[
    a + 1 = 1 \;\text{ (IX.a)} \\
    a * 0 = 0 \;\text{ (IX.b)}
\]

- __Absorpce negace__

\[
    a + (a * b) = a \;\text{ (X.a)} \\
    a * (a + b) = a \;\text{ (X.b)}
\]

- __Sousednost__ (spojování)

\[
    (a * b) + (a * \overline{b}) = a \\
    (a + b) * (a + \overline{b}) = a
\]

- __Existence jediného komplementu__ - Každá prvek \(B\) má právě jeden komplement.
- __DeMorganovy zákony__

\[
    \overline{(a + b)} = \overline{a} * \overline{b} \;\text{ (XII.a)} \\
    \overline{(a * b)} = \overline{a} + \overline{b} \;\text{ (XII.b)}
\]

- __Princip duality__ - Pokud platí nějaké tvrzení, tak platí i duální tvrzení, které vznikne vzájemnou záměnou operací \(+\) a \(*\) a prvků 0 a 1. Princip duality umožňuje realizovat libovolný logický obvod s použitím jen jedné operace a komplementů jednotlivých proměnných.

### Vennovy diagramy
Vennovy diagramy jsou grafické znázornění prvků množiny \(B\) Boolovy algebry jako uzavřené plochy a jejich vzájemných operací.

![Vennovy diagramy](/Images/20/vennovy_diagramy.png)

## Dvouhodnotová Boolova algebra
Ve dvouhodnotové Boolově algebře nabývají logické proměnné a výsledky logických funkcí pouze hodnot \(0\) a \(1\). Počítače realizují tuto algebru ve svých obvodech pomocí tranzistorů (dříve relé). Autorem dvouhodnotové Boolovy algebry je _Shannon_.

__Logická funkce__ \(f(x_1, x_2, ..., x_n)\) je zobrazení \(f:\; \{0,1\}^n \rightarrow \{0,1\}\). Hodnota logické funkce nabývá pouze hodnot 0 nebo 1. Pro \(n\) proměnných existuje \(2^n\) možností jak přiřadit hodnoty. Celkem pak existuje \(2^{2^n}\) různých logických funkcí \(n\) proměnných.

__Logický výraz__ je řetězec symbolů, který obsahuje _logické konstanty_, _proměnné_ a _operace_. Jeden logický výraz může mít několik tvarů, kterých je možné dosáhnout pomocí booleovy algebry.

__Logické operace__ jsou základní operace prováděné nad _logickými funkcemi_, _proměnnými_ a _konstantami_. Jsou reprezentovány logickými členy. Základní logické operace jsou:
- OR (\(+\)), AND (\(*\)), NOT (\(\overline{A}\))
- NOR (\(NOT(OR)\)), NAND (\(NOT(AND)\)), XOR (\(A \oplus B = \overline{A} * B + A * \overline{B}\)), XNOR (\(NOT(XOR)\))
- Implikace \(\Rightarrow\)
- Inhibice \(!\Rightarrow\)

Existují dvě speciální logické operace: __Kontradikce__, kdy výsledek je 0 nezávisle na vstupech, a __Tautologie__, kdy výsledek je 1 nezávisle na vstupech.

## Switching algebra
Switching algebra je modifikace Booleovy algebry, v které proměnná \(x\) reprezentuje __spínač___
- Hodnota \(0\) znamená __rozepnutý spínač__ (nekonečná impedance).
- Hodnota \(1\) znamená __sepnutý spínař__ (nulová impedance).
- Operace \(+\) (AND) reprezentuje sériové spojení dvou proměnných.
- Operace \(*\) (OR) reprezentuje paralelní spojení dvou proměnných.

![Switching algebra AND](/Images/20/switchig_algebra_and.png)
![Switching algebra OR](/Images/20/switchig_algebra_or.png)

## Shefferova algebra
Shefferova algebra je Booleova algebra, která využívá pouze logickou funkci __NAND__ a negaci. Pomocí funkce NAND lze realizovat ostatní logické členy a tedy i veškeré logické funkce. V Shefferově algebře platí _komutativní zákon_, ale neplatí _zákon asociativní_.

![Shefferova algebra](/Images/20/shefferova_algebra.png)

## Piercova algebra
Piercova algebra je Booleova algebra, která využívá pouze logickou funkce __NOR__ a negaci. Pomocí funkce NOR lze realizovat ostatní logické členy a tedy i veškeré logické funkce. V Piercove algebře platí _komutativní zákon_, ale neplatí _zákon asociativní_.

![Piercova algebra](/Images/20/piercova_algebra.png)

## Pojmy
- __Binární operace__ - Binární operace na množině \(A\) je zobrazení množiny \(A \times A\) do \(A\).
- __Neutrální prvek__ - Neutrální prvek \(e\) je prvek množiny \(A\), který při binární operaci s jiným prvkem \(a\) tento prvek nijak neovlivní. \(a \circ e = e \circ a = a\).
- __Inverzní prvek__ - Inverzní prvek \(a'\) je prvek, který při binární operaci s prvkem \(a\) má za výsledek neutrální prvek. \(a \circ a' = a' \circ a = e\).
- __Svaz__ - Svaz vymezuje mezi uspořádanými množinami ty, které jsou uspořádány "rozumě", tedy že zachovávají _suprema_ (největší prvek) a _infima_ (nejmenší prvek).
- __Hasseův diagram__ - Diagram pro zobrazení konečné částečně uspořádané množiny.

![Hasseův diagram](/Images/20/hasseuv_diagram.png)

## Příklady
Příklady v Boolově algebře
