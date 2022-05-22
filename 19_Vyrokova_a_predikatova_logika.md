# Vyroková a predikátová logika
- Otázky: syntaxe a sémantika výrokové logiky, splnitelnost a platnost, logická ekvivalence a logický důsledek, normální formy, jazyk predikátové logiky prvního řádu, termy a formule, volné a vázané proměnné
- Předmět: IDM (nový okruh)
- ToDo: Příklady
- Zdroje:
    - https://www.fit.vutbr.cz/~lengal/idm-2021/vyrokova-logika.pdf (výroková logika)
    - https://www.fit.vutbr.cz/~lengal/idm-2021/predikatova-logika.pdf (predikátová logika)

## Výroková logika
### Syntaxe
Syntaxe výrokové logiky určuje jak správně zapsat _formule_ výrokové logiky. Syntaxe výrokové logiky je definována pomocí:
- __Abecedy__ - Množiny symbolů, které se ve formulích mohou vyskytovat.
- __Gramatiky__ - Množina pravidel, pomocí nichž můžeme pomocí symbolů z abecedy stavět formule.

__Abeceda výrokové logiky__ je množina \(X \cup \{0, 1, \neg, \land, \lor, \rightarrow, \leftrightarrow, (, )\}\), kde \(X\) je množina _výrokových proměnných_, symbolům \(\{\neg, \land, \lor, \rightarrow, \leftrightarrow\}\) říkáme _logické spojky_ a symbolům \(\{0, 1\}\) _logické konstanty_. __Formule výrokové logiky__ jsou pak řetězce symbolů, které můžeme nad touto abecedou tvořit pomocí následujících pravidel:
- Je-li \(x\) výroková proměnné, pak řetězce "\(x\)", "\(0\)" a "\(1\)" jsou formule.
- Jsou-li \(\varphi\) a \(\psi\) formule, pak jsou formule i řetězce "\((\neg \varphi)\)", "\((\varphi \land \psi)\)" a další.
- Formule výrokové logiky jsou právě všechny konečné řetězce získané pomocí předchozích dvou pravidel.

Ve výsledných formulí je možné vynechat závorky na těchto místech: kolem celé formule, u asociativních spojek a kolem negace. Tato množina formulí je definována pomocí __induktivní definice__ (rekurzivní definice). Induktivní definice množiny je zadána pomocí _základních prvků_ a _konstrukčních pravidel_. Každý prvek z induktivně definované množiny lze reprezentovat jako _(abstraktní) syntaktický strom_:

![Abstraktní syntaktický strom](/Images/19/abstraktni_syntakticky_strom.png)

### Sémantika
Sémantika formule určuje její význam. Ve výrokové logice sémantika tedy určuje to, kde platí. Pro definice sémantiky je nutné znát __ohodnocení proměnných__ \(I\), což je zobrazení, které každé proměnné z \(X\) přiřadí hodnotu 0 nebo 1: \(I:\; X \rightarrow \{0, 1\}\).

Sémantika formula pak určuje, jakou pravdivostní hodnotu formule nabude pro jednotlivá ohodnocení proměnných. Tato hodnota se často definuje induktivně pomocí __pravidivostní tabulky__.

![Pravdivostní tabulka](/Images/19/pravdivostni_tabulka.png)

Formálně lze sémantiku výrokové logiky definovat následovně:
> Nechť \(V\) je množina všech ohodnocení proměnných \(V = (X \rightarrow \{0, 1\}\). Potom sémantika výrokové formule je funkce \([\cdot]:\; V \rightarrow \{0, 1\}\).

> Logické spojky \(\land\), \(\lor\), \(\leftrightarrow\) jsou _asociativní_. Logická spojka \(\rightarrow\) _asociativní_ není.

### Terminologie
Ohodnocení proměnných \(I:\; X \rightarrow {0,1}\) __splňuje__ formuli \(\varphi\) tehdy, když platí, že po dosazení hodnot proměnných v ohodnocení \(I\) do formule bude výsledná pravdivostní hodnota formule 1. V takovém případě říkáme, že \(I\) je __modelem__ formule \(\varphi\), což značíme jako \(I \models \varphi\) (\(I\) splňuje \(\varphi\)). Opačnou vlastnost značíme \(I \not\models \varphi\).

Existuje-li nějaké ohodnocení proměnných \(I\) takové, že \(I \models \varphi\), pak říkáme, že formule \(\varphi\) je __splnitelná__. Formule je __nesplnitelná__ (__kontradikce__), pokud není splnitelná, tj. neexistuje žádné ohodnocení, ve kterém by formule byla splnitelná. Formule je __platná__ (__tautologie__) pokud splněna ve všech možných ohodnocení proměnných, tj. její platnost nezávisí na hodnotách proměnných, což zapisujeme \(\models \varphi\). Formule je __neplatná__, pokud existuje ohodnocení proměnných, které ji nesplňuje, což značíme \(\not\models \varphi\).

> Platí následující:
> - Formule je platná právě tehdy, když její negace je nesplnitelná.
> - Formule je splnitelná právě tehdy, když její negace je neplatná.

Dvě formule \(\varphi\) a \(\psi\) jsou (logicky) __ekvivalentní__ (\(\varphi \Leftrightarrow \psi\)), pokud pro všechna ohodnocení proměnných \(I\) platí, že \(I\) je modelem \(\varphi\) právě tehdy, když \(I\) je modelem \(\psi\). V tabulce lze poznat tak, že ve všech řádcích mají obě formule stejné hodnoty.

Formule \(\psi\) je __logickým důsledkem__ formule \(\varphi\) \((\varphi \Rightarrow \psi)\), tehdy, když pro každé ohodnocení proměnných \(I\) platí, že je-li \(I\) modelem \(\varphi\), pak je \(I\) rovněž modelem \(\psi\).

### Algebraické úpravy formulí
S formulemi výrokové logiky lze různými způsoby manipulovat a upravovat je se zachováním jejich sémantiky (např.: _minimalizace_ formule). K tomu slouží __algebraické úpravy__, které nám umožní s formulemi pracovat jako s výrazy. Možné algebraické úpravy výrokových výrazů, kde \(x\), \(y\) a \(z\) jsou výrokové formule, jsou zapsány níže:

![Výrokové algebraické úpravy](/Images/19/vyrokove_upravy_1.png)
![Výrokové algebraické úpravy](/Images/19/vyrokove_upravy_2.png)

### Normální formy
Normální formy jsou tvary formulí, které splňují jistá syntaktická omezení.

#### Negační normální forma
Formule je v __Negační normální formě__ (NNF) pokud:
- Obsahuje jen následující logické spojky: \(0, 1, \neg, \land, \lor\).
- Negace \(\neg\) se vyskytuje jen před proměnnými.

Negační normální forma je vlastně seznam literálů spojenými konjunkcemi a disjunkcemi. __Literál__ je označení proměnné nebo její negace. Libovolná formule lze převést do NNF následujícím algoritmem využívající algebraické upravy:
1. Přepíšeme všechny bikondicionály \(\leftrightarrow\) ve formuli na implikace.
2. Přepíšeme všechny implikace \(\rightarrow\) ve formuli za negaci a disjunkci.
3. Pomocí De Morganových zákonů postupně přesuneme negace co nejhlouběji.
4. Kdykoliv to jde, eliminujeme dvojitou negaci.

#### Disjunktivní normální forma
Formule je v __Disjunktivní normální formě__ (DNF), pokud má následující tvar:

\[\bigvee_i \bigwedge_j \iota_{i,j}\]

kde \(\iota_{i,j}\) je literál. DNF je tedy disjunkce konjunkcí literálů. Konjunkci literálů se říká _klauzule_.

#### Konjunktivní normální forma
Formule je v __Konjunktivní normální formě__ (CNF), pokud má následující tvar:

\[\bigwedge_i \bigvee_j \iota_{i,j}\]

kde \(\iota_{i,j}\) je literál. CNF je tedy konjunkce disjunkcí literálů. Disjunkci literálů se také říká _klauzule_.

#### Převode do DNF a CNF
Převod formule do DNF nebo CNF je možný pomocí algebraických úprav. Pro převod formule \(\varphi\) do DNF/CNF lze použít následující algoritmus:
1. Převedeme formuli \(\varphi\) do NNF.
2. Formuli v NNF převedeme do tvaru, kde jsou všechny konjunkce pod disjunkcemi/disjunkce pod konjunkcemi pomocí distributivních a De Morganových zákonů.

Také je možné dělat převod formula do DNF nebo CNF pomocí _pravdivostní tabulky_. Tento způsob převodu je často jednodušší (především pro formule s malým počtem proměnných). Základní myšlenka převodu do DNF je následující: v pravdivostní tabulce najdeme přávě všechna ohodnocení proměnných \(I\), pro které má formule hodnotu 1. Výsledná formule v DNF se pak sestaví jako disjunkce konjunktivních klauzulí, kde každá klauzule odpovídá právě jednomu ohodnocení \(I\) tak, že se se sestaví konjunkce literálů odpovídající tomu, jakou \(I_j\) přiřazuje proměnným hodnotu. Převod do CNF probíhá duálně, jen se najdou ohodnocení, pro které má formule hodnotu 0 a literály mají negovanou hodnotu jak v ohodnocení.

## Predikátová logika 1. řádu
Predikátová logika 1. řádu (FOL) nám oproti výrokové logice umožňuje mluvit o _entitách_ nějakého _univerza_ a jejich _vlastnostech_ a _vztazích_ mezi nimi.

### Syntaxe
Syntaxi predikátové logiky lze chápat jako rozšíření syntaxe výrokové logiky a skládá se z:
- __Abecedy__ - Množiny symbolů, které se ve formulích mohou vyskytovat.
- __Gramatiky__ - Množina pravidel, pomocí nichž můžeme pomocí symbolů z abecedy stavět formule.

#### Abeceda
Abeceda predikátové logiky se skládá z následujících prvků:
- _Logické spojky_
- _Proměnné_
- _Závorky_
- __Kvantifikátory__: \(\exist, \forall\)
- __Funkční symboly__: \(f_1, f_2, ... \in F\)
- __Predikátové symboly__: \(p_1, p_2, ... \in P\)
- __Predikátový symbol rovnosti__: \(=\)

Novými prvky jsou __funkční symboly__ (z množiny \(F\)) a __predikátové symboly__ (z množiny \(P\)). Tyto množiny nejsou pevné, ale lze je chápat jako "parametr" jazyka, který si volíme podle toho, co chceme v logice vyjádřit. Každý funkčí i predikátový symbol má danou __aritu__, která udává kolik parametrů daný symbol běre. Aritu lze chápat jako funkci \((F \cup P) \rightarrow \N\) a je značena jako dolní index symbolu.

__Signatura__ jazyka predkátové logiky je dána jako dvojice \(\langle F,P \rangle\). Signaturu můžeme chápat jako "parametr" jazyka predikátové logiky, až po dodání signatury můžeme začít tvořit samotné formule predikátové logiky.

![Příklady signatur](/Images/19/priklad_signatury.png)

#### Gramatika
Základní prvek gramatiky predikátové logiky je __term__. Termy popisují, jakým způsobem se počítá nějaká hodnota. Formálně lze termy definovat následovně:
> 1. Je-li \(x\) proměnná (\(x \in X\)), pak řetězec "\(x\)" je term.
> 2. Je-li \(f\) funkční symbol s aritou \(n\) a \(t_1, ..., t_n\) jsou termy, pak i řetězec "\(f(t_1, ..., t_n)\)" je term

Často se termy zapisují bez závorek a v různým pořadí funkčního symbolu a jeho parametrů podle zvyklostí v daném jazyku (např.: místo \(+(x, 10)\) píšeme \(x + 10\)).

__Formule__ predikátové logiky jsou definovány následovně:
> 1. Je-li \(p\) predikátový symbol s aritou \(n\) a \(t_1, ..., t_n\) jsou termy, potom je řetězec "\(p(t_1, ..., t_n)\)" formule (platí i pro vestavěný binární predikátový symbol \(=\)). Formuli v tomto tvaru říkáme __atomická formule__.
> 2. Jsou-li \(\varphi\) a \(\psi\) formule, pak jsou formule i řetězce "\((\neg \varphi)\)", "\((\varphi \lor \psi)\)" a podobné.
> 3. Je-li \(\varphi\) formule a \(x \in X\) proměnná, pak jsou formule i řetězce "\((\exist x \varphi)\)" a "\((\forall x \varphi)\)".

Formule predikátové logiky se často (například v programech) reprezentují pomocí jejich syntaktických stromů.

![Syntaktický strom predikátové logiky](/Images/19/predikatova_log_syntakticky_strom.png)

#### Volné a vázané výskyty proměnných
_Kvantifikátory_ vážou proměnné a umožňují nám mluvit o všech prvcích z univerza diskurzu. Výskyt proměnné \(x\) je ve formuli __vázaný__, pokud se nachází v oboru platnosti nějakého kvantifikátoru \(\exist x\), \(\forall x\). Pokud je výskyt proměnné vázaný, pak je vázaný nejbližším kvantifikátorem nad sebou. Pokud výskyt proměnné není vázaný žádným kvantifikátorem, pak je __volný__. Volné a vázané proměnné lze názorně zobrazit v syntaktickém stromu.

![Volné a vázané proměnné v syntaktickém stromě](/Images/19/volne_vazane_promenne.png)

Říkáme, že proměnná je ve formuli volná, pokud v ní má alespoň jeden volný výskyt. Formuli \(\varphi\) s proměnnými \(x_1, ..., x_n\) často značíme jako \(\varphi(x_1, ..., x_n)\) a používáme notaci \(FREE[\varphi] =^{def} \{x_1, ..., x_n\}\). Formuli s volnými proměnnými říkáme __výroková forma__, formuli bez volných proměnných říkáme __uzavřená formule__ nebo __výrok__.

### Sémantika
Sémantika predikátové logiky je složitější. V predikátové logice musíme proměnným přiřazovat hodnoty z nějakého _univerza_ a musíme interpretovat funkční a predikátové symboly. Tomuto zevšeobecnění ohodnocení proměnných se říká __realizace__ (interpretace) jazyka.

> Realizace jazyka predikátové logiky se signaturou \(\langle F,P \rangle\) je dvojice \((D_I, \alpha_I)\), kde:
> - \(D_I\) je _neprázdná_ množina zvaná __doména__ nebo __univerzum diskurzu__.
> - \(\alpha_I\) přiřazuje funkčním a predikátovým symbolům jazyka a proměnným sémantiku následujícím způsobem:
>   - Každému funkčnímu symbolu \(f_{/n} \in F\) přiřazuje n-ární (totální) funkci: \(f_i:\; D_I \times \dots \times D_I \rightarrow D_I\).
>   - Každému predikátovému symbolu \(p_{/m} \in P\) přiřazuje m-ární relaci: \(p_I \subseteq D_I \times \dots \times D_I\).
>   - Každé proměnné \(x \in X\) přiřazuje hodnotu z domény \(D_I\).

Místo \(\alpha_I(f)\), \(\alpha_I(p)\) a \(\alpha_I(x)\) píšeme jen \(I(f)\), \(I(p)\) a \(I(x)\). Část, která určuje doménu a interpretaci funkčních a predikátových symbolů se říká _struktura_ a části, která určuje hodnoty proměnných se říká _ohodnocení proměnných_.

#### Sémantika formule v realizace
Sémantika formule je dána realizací \(I\), bez ní nelze říci, zda formule platí či neplatí. Když realizaci máme, můžeme pravdivostní hodnotu formule zjistit dosazením realizace do formule (místo proměnných, funkčních symbolů a predikátových symbolů) a formuli vyčíslit.

První věc, co je třeba provést je spočítat hodnotu všech termů ve formuli pro danou realizaci. V pevně dané realizace \(I\) s doménou \(D_I\) má term \(t\) konkrétní hodnotu. Hodnota obecného termu pro n-ární funkční symbol se definuje:

\[I(f(t_1, ..., t_n)) =^{def} f_I(I(t_1), ..., I(t_n)) \;\text{ pro }\; f_I = I(f)\]

Jak máme vyčíslené všechny termy, můžeme vyhodnotit pravdivostní hodnoty formule v realizaci. __Platnost__ formule \(\varphi\) v realizaci \(I\), značeno \(I \models \varphi\), je definováno induktivně následujícím způsobem:

> 1. Je-li \(\varphi\) atomická formule \(p(t_1, ... ,t_m)\) pro m-ární predikátový symbol \(p \in P\), potom \(I \models P(t_1, ..., t_m)\) právě když \((I(t_1), ..., I(t_m)) \in p_I\), kde \(p_i = I(p)\) je relace interpretující symbol \(p_{/m}\) v \(I\).
> 2. Je-li \(\varphi\) atomická formule \(t_1 = t_2\) potom \(I \models t_1 = t_2\) právě když \(I(t_1)\) a \(I(t_2)\) jsou identické prvky.
> 3. Pravdivostní hodnota pro výrokové spojky je definována očekávaným způsobem takto:
>
> ![Pravdivostní hodnota pro výrokové spojky](/Images/19/pravdivostni_hodnota_vyrokove_spojky.png)
>
> 4. Pravdivostní hodnota existenčně a univerzálně kvantifikovaných formulí v realizaci \(I\) je definována tak, že
>   - \(I \models \exist x \varphi\) pokud existuje realizace \(I'\), která rozšiřuje realizaci \(I\) o ohodnocení proměnné \(x\) na nějakou hondotu z \(D_I\) takové, že \(I' \models \varphi\).
>   - \(I \models \forall x \varphi\) pokud pro libovolnou realizace \(I'\), která rozšiřuje realizaci \(I\) o ohodnocení proměnné \(x\) na nějakou hodnotu z \(D_I\) platí, že \(I' \models \varphi\).

### Terminologie
Formule \(\varphi\) v jazyce \(L\) je __splnitelná__, pokud má nějaký model, tedy pokud existuje nějaká realizace \(I\) jazyka \(L\) taková, že \(I \models \varphi\).

Formule \(\varphi\) je (logicky) __platná__ pokud platí v libovolné realizace. Pro všechny realizace daného jazyka \(I\) platí \(I \models \varphi\). Platnost lze značit \(\models \varphi\).

Dvě formule \(\varphi\) a \(\psi\) jsou (logicky) __ekvivalentní__, zapisováno \(\varphi \Leftrightarrow \psi\) pokud pro všechny realizace \(I\) platí, že \(I\) je modelem \(\varphi\) právě tehdy, když \(I\) je modelem \(\psi\).

Formule \(\psi\) je __logickým důsledkem__ formule \(\varphi\), zapisováno \(\varphi \Rightarrow \psi\), tehdy, když pro každou realizaci \(I\) platí, že je-li \(I\) modelem \(\varphi\), pak je \(I\) rovněž modelem \(\psi\).

### Albebraické úpravy formulí
Podobě jako ve výrokové logice je možné formule predikátové logiky upravovat a manipulovat na jiné, logicky ekvivalentní formule. Mimo logických ekvivalencí z výrokové logiky můžeme ještě využít následující ekvivalence pro výroky predikátové logiky, kde \(\varphi\) a \(\psi\) jsou formule:

![Úpravy predikátových výroků](/Images/19/predikatove_upravy.png)

### Prenexní normální forma
Základní normální forma v predikátové logice je __prenexní normální forma__ (PNF). Tato forma slouží jako základní forma pro další úpravy. Formule \(\varphi\) je v PNF, pokud začíná prefixem všech kvantifikátorů, za nímž následuje formule bez kvantifikátorů:

\[\varphi:\; Q_1x_1Q_2x_2 ... Q_kx_k (\psi(x_1, ..., x_n))\]

kde \(Q_n \in \{\exist, \forall\}\) jsou kvantifikátory a \(\psi\) je formule bez kvantifikátorů. Pro převod formule do PNF se používají algebraické úpravy.

## Příklady
[TODO]
