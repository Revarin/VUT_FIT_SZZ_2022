# Bezkontextové jazyky a jejich modely
- Otázky: zásobníkové automaty, bezkontextové gramatiky
- Předmět: IFJ (původně okruh 21)
- Zdroje:
    - https://www.fit.vutbr.cz/study/courses/IFJ/private/prednesy/Ifj06-cz.pdf

## Bezkontextová gramatika
Bezkontextová gramatika je gramatika založena na konečné množině gramatických pravidel, které generují řetězce daného jazyka.

> Bezkontextová gramatika (BKG) je uspořádaná čtveřice \(G = (N, T, P, S)\), kde:
> - \(N\) je abeceda neterminálů.
> - \(T\) je abeceda terminálů, přičemž \(N \cap T = \empty\)
> - \(P\) je konečná množina pravidel tvaru \(A \to x\), kde \(A \in N\), \(x \in (N \cup T)^*\).
>   - Obsahuje i speciální _epsilon pravidlo_ \(A \to \varepsilon\).
> - \(S \in N\) je počáteční neterminál.

![Bezkontextová gramatika](/Images/22/bezkontextova_gramatika.png)

Aplikaci pravidla na neterminál označujeme jako __derivační krok__. Sekvenci derivačních kroků zapisujeme jako šipku, kde _číslo_ značí počet kroků, nebo můžeme použít zástupné znaky:
- \(+\) pro jeden a více derivačních kroků.
- \(*\) pro nula a více derivačních kroků.

\[
    aAb \Rightarrow^1 aaBbb \; [1: A \to aBb] \\
    aaBbb \Rightarrow^1 aacbb \; [2: B \to c]
\]

> Nechť \(G = (N, T, P, S)\) je bezkontextová gramatika. Jazyk generovaný bezkontextovou gramatikou \(G\), \(L(G)\) je definován jako \(L(G) = \{w:\; w \in T^*, S \to^* w\}\)

### Bezkontextový jazyk
Bezkontextový jazyk je jazyk generovaný bezkontextovou gramatikou. Přijímá ho nedeterministický zásobníkový automat.

> Nechť \(L\) je jazyk. \(L\) je bezkontextový jazyk (BKJ), pokud existuje bezkontextová gramatika, která ho generuje.

![Příklad bezkontextového jazyku](/Images/22/bezkontextovy_jazyk.png)

### Derivační strom
Pravidlový strom slouží pro grafické znázornění pravidla bezkontextové gramatiky. Z pravidlových stromů se skládá __derivační strom__, který odpovídá použitým pravidlům.

![Příklad derivačního stromu](/Images/22/pravidlovy_strom.png)

Derivace se může provádět buď _libovolně_ nebo v pevně daném pořadí. Výsledný derivační strom bude při použití jakéhokoliv pořadí derivací vždy stejný. Jsou dva způsoby řazení derivačních kroků:
- __Nejlevější derivace__ - Během nejlevějšího derivačního kroku je přepsán nejlevější neterminál. Značí se \(uAv \Rightarrow_{lm} uxv [p]\).
- __Nejpravější derivace__ - Během nejpravějšího derivačního kroku je přepsán nejpravější neterminál. Značí se \(uAv \Rightarrow_{rm} uxv [p]\).

Bez újmy na obecnosti můžeme uvažovat používání pouze nejlevějších nebo nejpravějších derivací.

### Gramatická nejednoznačnost bezkontextové gramatiky
> Nechť \(G = (N, T, P, S)\) je bezkontextová gramatika. Pokud existuje řetězec \(x \in L(G)\) s více jak jedním derivačním stromem, potom je \(G\) __nejednoznačná__. Jinak je \(G\) __jednoznačná__.
>
> Bezkontextový jazyk \(L\) je __vnitřně nejednoznačný__ pokud \(L\) není generován žádnou jednoznačnou bezkontextovou gramatikou.

## Zásobníkové automaty
Zásobníkové automaty jsou konečné automaty rozšířené o zásobník.
> Zásobníkový automat (ZA) je uspořádaná sedmice \(M = (Q, \Sigma, \Gamma, R, s, S, F)\), kde:
> - \(Q\) je konečná množina stavů.
> - \(\Sigma\) je vstupní abeceda.
> - \(\Gamma\) je zásobníková abeceda.
> - \(R\) je konečná množina pravidel tvaru \(Apa \to wq\), kde \(A \in \Gamma\), \(p, q \in Q\), \(a \in \Sigma \cup \{\varepsilon\}\), \(w \in \Gamma^*\).
> - \(s \in Q\) je počáteční stav.
> - \(S \in \Gamma\) je počáteční symbol na zásobníku.
> - \(F \subset Q\) je množina koncových stavů.

![Zásobníkový automat](/Images/22/zasobnikovy_automat.png)
![Grafická reprezentace ZA](/Images/22/zasobnikovy_automat_graficka_reprezentace.png)

Zásobníkové automaty jsou modely pro bezkontextové gramatiky. Pro každou bezkontextovou gramatiku \(G\) existuje zásobníkový automat \(M\), pro které platí \(L(G) = L(M)_{\varepsilon}\).

__Interpratece pravidel__ \(Apa \to wq\) znamená, že pokud je aktuální stav \(p\), aktuální symbol na vstupní pásce \(a\) a symbol na vrcholu zásobníku \(A\), potom zásobníkový automat \(M\) může přečíst \(a\) a na zásobníku nahradit \(A\) za \(w\) a přejít ze stavu \(p\) do \(q\).

__Konfigurace__ zásobníkového automatu je aktuální stav ZA, stav zásobníku a část vstupní pásky, která ještě nebyla přečtená.
> Nechť \(M = (Q, \Sigma, \Gamma, R, s, S, F)\) je zásobníkový automat. Konfigurace \(M\) je řetězec \(\chi \in \Gamma^* Q \Sigma^*\),

![Konfigurace ZA](/Images/22/konfigurace_za.png)

__Přechod__ zásobníkového automatu je jeden výpočetní krok ZA. Při přechodu přejde ZA z původní konfigurace do nové konfigurace použitím nějakého pravidla. Přechod se zapisuje \(xApay \vdash xwqy [r]\). Několik přechodů po sobě se nazývá sekvence přechodů.

![Přechod ZA](/Images/22/prechod_za.png)

### Přijímané jazyky zásobníkových automatů
Existují tři typy jazyků přijímanými zasobníkovým automatem \(M = (Q, \Sigma, \Gamma, R, s, S, F)\). Tyto jazyky jsou si ekvivalentní a existují algoritmy pro jejich vzájemné převody.

> 1. Jazyk přijímaný zásobníkovým automatem \(M\) __přechodem do koncového stavu__, značen jako \(L(M)_f\), je definován jako \(L(M)_f = \{w: w \in \Sigma^*,\; Ssw \vdash^* zf,\; z \in \Gamma^*,\; f \in F\}\).
> 2. Jazyk přijímaný zásobníkovým automatem \(M\) __vyprázdněním zásobníku__, značen jako \(L(M)_{\varepsilon}\), je definován jako \(L(M)_{\varepsilon} = \{w: w \in \Sigma^*,\; Ssw \vdash^* zf,\; z = \varepsilon,\; f \in Q\}\).
> 3. Jazyk přijímaný zásobníkovým automatem \(M\) __přechodem do koncového stavu a vyprázdněním zásobníku__, značen jako \(L(M)_{f \varepsilon}\), je definován jako \(L(M)_{f \varepsilon} = \{w: w \in \Sigma^*,\; Ssw \vdash^* zf,\; z = \varepsilon,\; f \in F\}\).

### Druhy zásobníkových automatů
- __Deterministický zásobníkový automat__ (DZA) - ZA, který může z každé konfigurace provést maximálně jeden přechod. Obecné ZA jsou silnější než deterministické ZA.
- __Rozšířený zásobníkový automat__ (RZA) - ZA, která může z vrcholu zásobníku číst celý řetězec, více symbolů (obyčejný ZA může ze zásobníku číst jen jeden symbol). Rozšířený ZA a obyčejný ZA jsou ekvivalentní - jejich třída přijímaných jazyků je stejná.

RZA a ZA se používají jako modely pro syntaktickou analýzu. Mohou simulovat konstrukci derivačního stromu pro bezkontextovou gramatiku _shora dolů_ a _zdola nahoru_.

![Syntaktická analýza](/Images/22/syntakticka_analyza.png)

## Příklady
ZA pro správné uzávorkování, \((a^n.b^n)\),
