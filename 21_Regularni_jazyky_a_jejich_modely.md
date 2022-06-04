# Regulární jazyky a jejich modely
- Otázky: konečné automat, regulární výraz
- Předmět: IFJ (původně okruh 20)
- Zdroje:
    - https://www.fit.vutbr.cz/study/courses/IFJ/private/prednesy/Ifj01-cz.pdf (abecedy a jazyky)
    - https://www.fit.vutbr.cz/study/courses/IFJ/private/prednesy/Ifj03-cz.pdf (modely pro regulární jazyky)
    - https://www.fit.vutbr.cz/study/courses/IFJ/private/prednesy/Ifj04-cz.pdf (konečné automaty)

## Abecedy a jazyky
__Abeceda__ je libovolná neprázdná konečná množina symbolů \(\Sigma = \{a,b,1,2\}\).

> Nechť \(\Sigma^*\) značí množinu všech možných řetězců nad abecedou \(\Sigma\). Každá podmnožina \(L \subseteq \Sigma^*\) je __jazyk__ \(L\) nad abecedou \(\Sigma\).

Jazyk je tedy soubor nějakých slov, čili je to podmnožina řetězců abecedy. Jazyk je charakterizován svou __kardinalitou__, která značí počet všech možných řetězců (slov) nad abecedou. Podle kardinality může být jazyk:
- __Konečný jazyk__ - Má konečnou kardinalitu, obsahuje konečný počet řetězců.
- __Nekonečný jazyk__ - Má nekonečnou kardinalitu.

Jazyk \(L\) je množina a tudíž nad jazykem můžeme provádět veškeré operace s množinami:
- Sjednocení \(L_1 \cup L_2\)
- Průnik \(L_1 \cap L_2\)
- Rozdíl \(L_1 - L_2\)
- Doplněk \(L_1'\)
- _Konkatenace_ \(L_1 . L_2\)
- _Reverzace_ \(reverse(L_1)\)
- _Mocnina_ \(L^i = L . L...L\)
- _Iterace_ \(L^* = L^0 \cup L^1 \cup ... \cup L^i \cup ...\), \(L^+ = L^1 \cup ... \cup L^i \cup ...\)

## Regulární jazyky a jejich modely
Regulární jazyk je formální jazyk, který je generován regulární gramatikou. Regulární jazyky lze modelovat pomocí dvou ekvivalentních modelů: konečné automaty a regulární výrazy.

> Daný jazyk \(L\) je _regulární_:
> - Pokud existuje __konečný automat__, který akceptuje právě všechna slova z jazyku \(L\).
> - Pokud existuje __regulární výraz__ \(r\), který tento jazyk značí.

Pro důkaz, že daný jazyk _není_ regulární lze použít __Pumping lemma__. Pumping lemma nelze použít k dokázání že daný jazyk je regulární.

> Pumping lemma: Nechť \(L\) je regulární jazyk. Potom existuje \(k \geq 1\) takové, že pokud \(z \in L\) a \(|z| \geq k\), pak existuje \(u, v, w:\; z = uvw\), kde:
> - \(v \neq \varepsilon\)
> - \(|uv| \leq k\)
> - Pro každé \(m \geq 0\), \(uvmw \in L\)

### Regulární gramatika
Regulární jazyk je definován právě __regulární gramatikou__.
> Regulární gramatika je uspořádaná čtveřice \(G = (T, N, P, s)\), kde:
> - \(T\) je konečná množina terminálních symbolů (abeceda).
> - \(N\) je konečná množina neterminálních symbolů.
> - \(P\) je konečná množina pravidel ve tvaru \(n \to (t \land n)\) nebo \(n \to t\). Použití pravidla se nazývá __odvození__.
> - \(s \in N\) je počáteční symbol.

![Příklad regulární gramatiky](/Images/21/regularni_gramatika.png)

### Pojmy
- __Prázdné slovo__ \(\varepsilon\) je prázdný řetězec, který ale vyhovuje jazyku - je možné tento řetězec vygenerovat nebo přijmout.
- __Řetězec__ je jakákoliv posloupnost terminálních i neterminálních symbolů abecedy (znaků).
- __Větná forma__ je řetězec, který lze odvodit z počátečního symbolu gramatiky.
- __Věta__ je větná forma složená pouze z terminálních symbolů.

## Konečné automaty
Konečný automat je nejjednodušší model založený na konenčné množině stavů a výpočetních pravidel.

> Konečný automat je uspořádaná pětice \(M = (Q, \Sigma, R, s, F)\), kde:
> - \(Q\) je konečná množina stavů.
> - \(\Sigma\) je vstupní abeceda.
> - \(R\) je konečná množina pravidel tvaru \(pa \to q\), kde \(p,q \in Q\) a \(a \in \Sigma \cup {\varepsilon}\).
> - \(s \in Q\) je počáteční stav.
> - \(F \subseteq Q\) je množina koncových stavů.

![Příklad konečného automatu](/Images/21/konecny_automat.png)
![Tabulka konečného automatu](/Images/21/konecny_automat_tabulka.png)

Pokud jsme schopni s nějakou vstupní posloupností znaků daného jazyka \(L\) v konečném automatu dojít z počátečního stavu do konečného stavu, pak je tento jazyk \(L\) __přijímaný jazyk__ tohoto konečného automatu. Dva konečné automaty jsou __ekvivalentní__, pokud přijímají i zamítají stejná slova.

### Pojmy
__Konfigurace__ je instance popisu KA. Skládá se z aktuálního stavu KA a ještě nezpracovaného vstupního řetězce.
> Nechť \(M = (Q, \Sigma, R, s, F)\) je KA. _Konfigurace_ KA \(M\) je řetězec \(\chi \in Q \Sigma^*\).

__Přechod__ je jeden výpočetní krok KA.
> Nechť \(pax\) a \(qx\) jsou dvě konfigurace KA \(M\), kde \(p, q \in Q\), \(a \in \Sigma \cup \{\varepsilon\}\) a \(x \in \Sigma^*\). Nechť \(r = pa \to q \in R\) je pravidlo. Potom \(M\) může provést _přechod_ z \(pax\) do \(qx\) za použití pravidla \(r\), zapsáno \(pax \vdash qx [r]\)

__Sekvence přechodů__ je několik výpočetních kroků po sobě. Je to vlastně několik přechodů po sobě.

### Druhy konečných automatů
Existuje několik typů konečných automatů:
- __Základní konečný automat__ (KA) - KA, který obsahuje __epsilon přechody__ (přechod z jednoho stavu do druhého bez vstupního znaku abecedy) a v němž je možné z jedné konfigurace přejít do více dalších konfigurací.
- __Konečný automat bez epsilon přechodů__ - KA, který neobsahuje _epsilon přechody_. Stále je v něm možné z jedné konfigurace přejít do více dalších konfigurací.
- __Deterministický konečný automat__ (DKA) - KA, který neobsahuje _epsilon přechody_. Z jedné konfigurace (stavu) může pomocí písmena ze vstupní abecedy přejít pouze do _jednoho_ dalšího stavu.
- __Úplný deterministický konečný automat__ (ÚDKA) - DKA, kde v každém stavu pro každý znak vstupní abecedy existuje právě jeden přechod do dalšího stavu. Přechody, které nejsou potřeba směřují do __false stavu__. Tento KA se nemůže zaseknout, ale končí ve stavu _false_.
- __Dobře specifikovaný konečný automat__ (DSKA) - ÚDKA, který nemá _nedostupné stavy_ (stav, do něhož se nelze dostat z počátečního stavu) a má maximálně jeden _neukončující stav_ (stav, z něhož se nelze dostat do koncového stavu) a to stav _false_.
- __Minimální konečný automat__ (MKA) - KA, který obsahuje pouze rozlišitelné stavy. Pro každý DSKA existuje právě jeden MKA.

### Determinizace
Pokud má nedeterministický konečný automat \(n\) stavů, bude jeho deterministická varianta mít nejvíce \(2^n\) stavů. Každý nedeterministický konečný automat má svoji deterministickou variantu. Tato deterministická varianta nemusí být minimální.

Postup převodu obecného konečného automatu na deterministický konečný automat je následující:
1. Odstranění epsilon přechodů

![Odstanění epsilon přechodů](/Images/21/odstraneni_epsilon_prechodu.png)

2. Odstranění nedeterminismu - Vytvořit stavy ze všech podmnožin množiny stavů KA bez epsilon přechodů a přidat přechody mezi nimi tak, aby simulovaly přechody původního automatu.

![Odstranění nedeterminismu](/Images/21/odstraneni_nedeterminismu.png)

## Regulární výrazy
Regulární výraz (RV) je řetězec popisující celou množinu řetězců. Jsou to výrazy s operátory \(.\), \(+\) a \(^*\), které značí konkatenaci, sjednocení a iteraci.

> Nechť \(\Sigma\) je abeceda. Regulární výrazy nad abecedou \(\Sigma\) a jazyky, které tyto výrazy značí jsou definovány následovně:
> - \(\empty\) je regulární výraz značící prázdnou množinu (prázdný jazyk).
> - \(\varepsilon\) je regulární výraz značící jazyk s jedním prvkem \(\{\varepsilon\}\).
> - \(a\), kde \(a \in \Sigma\), je regulární výraz značící jazyk \(\{a\}\).
> - Nechť \(r\) a \(s\) jsou regulární výrazy značící jazyky \(L_r\) a \(L_s\). Potom:
>   - \((r . s)\) je regulární výraz značící jazyk \(L = L_r . L_s\) (_konkatenace_).
>   - \((r + s)\) je regulární výraz značící jazyk \(L = L_r \cup L_s\) (_sjednocení_).
>   - \((r^*)\) je regulární výraz značící jazyk \(L = L_r^*\) (_iterace_).

### Převod regulárního výrazu na konečný automat
Příklad převodu regulárního výrazu \(r= ((ab) + (cd))^*\) na ekvivalentní konečný automat \(M\):

![Převod RV na KA](/Images/21/prevod_rv_ka_1.png)
![Převod RV na KA](/Images/21/prevod_rv_ka_2.png)
![Převod RV na KA](/Images/21/prevod_rv_ka_3.png)

## Příklady
Deteminizace KA, převod RV na KA
