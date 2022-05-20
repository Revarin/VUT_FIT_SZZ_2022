# Množiny, relace a zobrazení
- Otázky:
- Předmět: IDM
- Zdroje:
    - https://www.umat.fekt.vut.cz/~hlinena/IDM/Prednasky/mnoziny.pdf (množiny)
    - https://www.umat.fekt.vut.cz/~hlinena/IDM/Prednasky/relace.pdf (relace)

## Množina
> Množina je matematická struktura (soubor prvků), obsahující prvky, které se neopakují. Je to tedy soubor vzájemně _rozlišitelných_ objektů (např.: celá čísla, reálná čísla...).  Množina je jednoznačně určena svými prvky (nezáleží na pořadí).

Množina může být _konečná_, _nekonečná_ nebo _prázdná_. Může být popsána dvěma způsob:
- __Výčtem prvků__ - \(A = \{1, 2, 3\}\)
- __Predikátem__ - \(X = \{a\:|\:V(a)\}\) (množina všech prvků, pro které platí \(V\))

Prvky množiny mohou být také množiny. V tomto případě mluvíme o __systému množin__.

Počet prvků množiny \(A\) označujeme jako __mohutnost množiny__ a značíme ji \(|A|\). Pokud chceme dokázat, že dvě množiny \(A\) a \(B\) jsou stejně mohutné, tak musíme najít vzájemně jednoznačné přiřazení prvků \(A\) do \(B\). Nekonečné množiny nemají definovanou mohutnost, rozdělují se ale na:
- __Spočetné množiny__ - Spočetné množiny jsou všechny množiny se stejnou mohutností jako množina přirozených čísel (např.: množina celých čísel).
- __Nespočetné množiny__ - (např.: množina všech reálných čísel)

__Podmnožina__ množiny \(A\) je taková množina \(B\), jejíž každý prvek je zároveň prvkem množiny \(A\). Každá množina kromě prázdné množiny obsahuje alespoň dvě podmnožiny - samu sebe a prázdnou množinu.

Množina všech podmnožin množiny \(X\) (včetně prázdné množiny a sebe sama) se nazývá __potenční množina množiny \(X\)__. Potenční množina množiny o \(n\) prvcích má \(2^n\) prvků. Potenční množina prázdné množiny má jeden prvek - prázdnou množinu/sebe sama.

__Rozklad množiny__ \(A\) je systém množin \(A'=\{A_1, A_2, ...\}\), pro který platí \(A_1 \cup A_2 \cup ... = A\) a pro libovolné dva různé prvky platí, že jejich průnik je prázdný \(A_x \cap A_y = \emptyset;\;x \neq y\). Prvky množiny rozkladu nazýváme třídy rozkladu.

![Rozklad množiny](/Images/16/rozklad_mnoziny.png)

Pro algebraické operace s množinami platí __uzavřenost množiny__. Když se s prvky množiny procede nějaká operace, tak výsledkem budou zase prvky této množiny.

### Operace s množinami
S dvěma a více množinami lze provádět různé operace:
- __Sjednocení__ - \(X \cup Y = \{x | x \in X \lor x \in Y\}\)

![Sjednocení dvou množin](/Images/16/sjednoceni.png)

- __Průnik__ - \(X \cap Y = \{x | x \in X \land x \in Y\}\)

![Průnik dvou množin](/Images/16/prunik.png)

- __Rozdíl__ - \(X \setminus Y = \{x | x \in X \land x \notin Y\}\)

![Rozdíl dvou množin](/Images/16/rozdil.png)

- __Symetrická diference__ - \(X \div Y = (X \setminus Y) \cup (Y \setminus X)\)

![Symetrická diference dvou množin](/Images/16/symetricka_diference.png)

Operace nad množinami mají různé vlastnosti:
- __Komutativnost__  - Výsledek _binární operace_ nezávisí na pořadí jejích operandů. Pozn.: rozdíl komutativní není.

\[
    X \cup Y = Y \cup X \\
    X \cap Y = Y \cap X    
\]

- __Asociativita__ - Výsledek _binární operace_ nezávisí na tom, jak použijeme závorky u výrazu s více operandy, v jakém pořadí budeme tedy tento výraz počítat.

\[
    (X \cup Y) \cup Z = X \cup (Y \cup Z) \\
    (X \cap Y) \cap Z = X \cap (Y \cap Z)
\]

- __Distributivnost__ - Vlastnost _binární operace_ vůči jiné binární operaci. Udává, že můžeme tuto operaci distribuovat přes jinou operaci (např.: distributivita násobení vůči sčítání čísel).

\[
    (X \cup Y) \cap Z = (X \cap Z) \cup (Y \cap Z) \\
    (X \cap Y) \cup Z = (X \cup Z) \cap (Y \cup Z)
\]

Dále pro _binární operace_ platí takzvané __De Morganovy zákony__, které definují vlastnosti pro binární výrazy.

\[
    \overline{A \cup B} = \overline{A} \cap \overline{B} \\
    \overline{A \cap B} = \overline{A} \cup \overline{B}
\]

## Relace
Relace nebo __n-ární__ relace je libovolný vztah mezi skupinou prvků jedné nebo více množin. 

> N-ární relací mezi množinami \(A_1\), \(A_2\), ..., \(A_n\), kde \(x\) náleží do \(n\) rozumíme libovolnou podmnožinu __kartézského součinu \(n\) množin.

> __Kartézským součinem__ množin \(A\) a \(B\) je množina všech uspořádaných dvojic jejich prvků. Kartézský součin komutativní.
>
> \[X \times Y = \{(x,y) | x \in X \land y \in Y\}\]

>__Uspořádaná dvojice__ je výraz \((a,b)\), který se obecně liší od \((b,a)\). Tedy na rozdíl od množin záleží na pořadí prvků.

Pod pojmem relace se většinou myslí __binární relace__. Binární relací z \(X\) do \(Y\) rozumíme jakoukoli podmnožinu jejich kartézského součinu \(R \subset X \times Y\). Pokud platí \(X = Y\), tak hovoříme o binární relaci na \(X\). Binární relace je tak vztah mezi dvěma množinami. Formální definice binární relace je:

> Binární relace je uspořádaná trojice \([A, B, R]\), kde \(A\) a \(B\) jsou libovolné množiny a \(R\) je podmnožina kartézského součinu \(A \times B\). Množině \(A\) se říká __definiční obor__, množině \(B\) __obor hodnot__ a množinu \(R\) nazýváme graf relace.

### Vlastnosti relací
Relace mohou mít různé vlastnosti:
- __Symetrická relace__ - Relace je symetrická v případě, že při prohození prvků, které jsou v relaci, zůstanou stále v relaci. Pokud \(a\) je v relaci s \(b\), tak i \(b\) je v relaci s \(a\).
- __Antisymetrická relace__ - Relace je antisymetrická v případě, že při prohození prvků, které jsou v relaci, tak v relaci nebudou. Je to opak symetrie. Relace může být _slabě_ nebo _silně_ antisymetrická (silně vylučuje relaci prvků sama se sebou).
- __Reflexivní relace__ - Relace je reflexivní v případě, že prvky jsou v relaci sami se sebou.
- __Tranzitivní relace__ - Relace je tranzitivní v případě, když je \(a\) v relaci s \(b\) a \(b\) je v relaci s \(c\), tak i \(a\) je v relaci s \(c\).
- __Inverzní relace__ - Inverzní relace je relace vzniklá prohozením pořadí prvků v uspořádaných dvojicích, neboli prohození definičního oboru a oboru hodnot.

Pokud je relace zároveň reflexivní, symetrická a tranzitivní, tak se nazývá __relace ekvivalence__. Každá relace ekvivalence rozdělí množinu \(M\) na systém disjunktních množin nazývané _třídy ekvivalence_, neboli vytvoří __rozklad množiny__.

\[
    M[x] = y \in M;\:[x, y] \in R
\]

## Zobrazení
> Zobrazení \(f: X \rightarrow Y\) je taková relace, která jednomu prvku \(x\) z množiny \(A\) přiřazuje právě jeden prvek \(y\) množiny \(B\). Množina \(A\) se nazývá __definiční obor__ a její prvky se nazývají __vzory__. Množina \(B\) se nazývá __obor hodnot__ a její prvky se nazývají __obrazy__.

Zobrazení je tedy přiřazení prvků jedné množiny k prvkům množiny druhů. Jeden vzor nesmí být přiřazen k více obrazů. Naopak jeden obraz může mít více vzorů nebo žádný.

### Druhy zobrazení
- __Injektivní zobrazení__ (prosté zobrazení) - Každý prvek oboru hodnot má namapován _nejvíce jeden_ prvek z definičního oboru.

![Injektivní zobrazení](/Images/16/injektivni_zobrazeni.png)

- __Surjektivní zobrazení__ - Každý prvek oboru hodnot má namapován _alespoň jeden_ prvek z definičního oboru.

![Surjektivní zobrazení](/Images/16/surjektivni_zobrazeni.png)

- __Bijektivní zobrazení__ - Každý prvek oboru hodnot má namapován _právě jeden_ prvek z definičního oboru. Speciální vlastností bijektivního rozbrazení je existence _inverzního zobrazení_.

![Bijektivní zobrazení](/Images/16/bijektivni_zobrazeni.png)

## Svaz
Množina \(X\) s relací \(R\) je __svazem__, pokud pro každou dvouprvkovou podmnožinu v relaci \(R\) lze definovat maximim a minimum. Neboli, svaz je _uspořádatelná_ množina. Když jsou dva stejné, tak se stále jedná o svaz (maximum a minimum jsou oba prvky).

> Nechť \(X\) je množina, \(\land\) a \(\lor\) jsou operace na množině \(X\) s následujícími vlastnostmi pro všechny prvky \(x, y, z \in X\):
> 1. \(x \lor x = x\), \(x \land x = x\) (idempotence)
> 2. \(x \lor y = y \lor x\), \(x \land y = y \land x\) (komutativita)
> 3. \((x \lor y) \lor z = x \lor (y \lor z)\), \((x \land y) \land z = x \land (y \land z)\) (asociativita)
> 4. \(x \land (x \lor y) = y\), \(x \lor (x \land y) = x\) (absorbční zákony)
>
> Pak trojici \((X, \lor, \land\) nazýváme _svazem na \(X\)_ O svazu \((X, \lor, \land)\) někdy říkáme, že je algebraicky definovaný, abycho zdůraznili, že jej chápeme jako algebru, na rozdíl od svazově uspořádané množiny.

## Grupa
> Grupa je dvojice \((A, o)\), kde \(A\) je množina a \(o\) je nějaká binární operace, která splňuje následující _tři axiomy_:
> - __Asociativita__: \((a + b) + c = a + (b + c)\)
> - __Existence neutrálního prvku__: \(a + 0 = a\)
> - __Existence inverzního prvku__: \(a + (-a) = 0\)
