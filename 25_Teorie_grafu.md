# Teorie grafů
- Otázky: pojem grafu, isomorfismus grafů, souvislost, grafové algoritmy
- Předmět: IDM

## Graf
Graf je speciální případ binární relace. Skládá se z vrcholů a hran, které tyto vrcholy propojují.

> Jednoduchý neorientovaný grf je uspořádaná dvojice \(G = (V, E)\), kde
> - \(V\) je množina vrcholů.
> - \(E\) je množina hran, množina vybraných dvouprvkových podmnožin z množiny vrcholů \(V\)

Hranu mezi vrcholy \(u\) a \(v\) zapisujeme jako \(\{u,v\}\) nebo zkráceně \(uv\). Vrcholy spojené hranou se nazývají _sousední vrcholy_. Hrana \(uv\) pak _vychází_ z těchto vrcholů. Grafy můžeme zadat buď neformálně graficky, nebo formálně výčtem vrcholů a hran.

![Neformální zadání grafu](/Images/25/graficky_graf.png)

\[V = \{1, 2, 3, 4,\}\;\; E = \{\{1,2\},\{1,3\},\{1,4\},\{3,4\}\}\]

### Stupeň vrcholu
Stupeň vrcholu \(x\) v grafu \(G\) rozumíme počet hran vycházejících z vrcholu \(x\). Stupeň vrcholu \(x\) v grafu \(G\) značíme \(d_G(x)\). Graf je __d-regulární__ jestliže mají všechny jeho vrcholy stejný stupeň d. _Nejvyšší_ stupeň grafu \(G\) značíme \(\Delta(G)\), _nejnižší_ stupeň grafu značíme \(\delta(G)\).

### Typy grafů
- __Kružnice__ - Graf délky \(n,\; n \geq 3\), který má všechny vrcholy spojeny do jednoho cyklu přes \(n\) hran. Značí se jako \(C_n\).

![Kružnice](/Images/25/kruznice.png)

- __Cesta__ - Graf délky \(n,\; n \geq 0\), který má \(n + 1\) různých vrcholů spojených za sebou přes \(n\) hran. Žádné vrcholy ani hrany se v něm neopakují. Znáčí se jako \(P_n\).

![Cesta](/Images/25/cesta.png)

- __Úplný graf__ - Graf s \(n \geq 1\) vrcholy, z nichž každý vrchol je spojen se všemi ostantími vrcholy. Celkem má graf \(\binom{n}{2}\) hran. Značí se \(K_n\).

![Úplný graf](/Images/25/uplny_graf.png)

- __Úplný bipartitní graf__ - Úplný graf, jehož vrcholy jsou rozděleny do dvou skupin (partit) o velikosti \(m \geq 1\) a \(n \geq 1\). Každý vrchol skupiny je spojen se všemi vrcholy druhé skupiny, jsou spojeny všechny \(m.n\) dvojice. Značí se jako \(K_{m,n}\).

![Úplný bipartitní graf](/Images/25/uplny_bipartitni_graf.png)

- __Hvězda__ - Graf s \(n \geq 1\) rameny je zvláštní případ úplného bipartitního grafu. Značí se jako \(K_{1,n}\).

![Hvězda](/Images/25/hvezda.png)

- __Sled__ - Sled je v grafu __posloupnosti vrcholů__ taková, že mezi každými dvěma po sobě jdoucími vrcholy je hrana. Hrany i vrcholy se mohou na rozdíl od kružnice opakovat. Sled je tedy průchod po hranách grafu z \(u\) do \(v\), který může obsahovat cykly.
- __Tah__ - Tah je sled, ve kterém se neopakují hrany. Speciální případ tahu je __uzavřený tah__, který končí ve vrcholu ve kterém začínal. Graf \(G\) lze nakreslit jedním uzavřeným tahem právě, když je \(G\) souvislý a všechny jeho vrcholy jsou sudého stupně.

### Orientované grafy
V orientovaném grafu má každá hrana určitý směr.

> Orientovaný graf \(G\) je uspořádaná dvojice \(G = (V, A)\), kde
> - \(V\) je množina vrcholů.
> - \(A\) je množina orientovaných hran \(A \subseteq V(G) \times V(G)\).

![Orientovaný graf](/Images/25/orientovany_graf.png)

### Podgraf
> Podgrafem grafu \(G\) rozumíme libovolný graf \(H\), pro který platí:
> - Množina vrcholů grafu \(H\) je podmnožinou vrcholů grafu \(G\): \(V(H) \subseteq V(G)\).
> - Za hrany má libovolnou podmnožinu hran grafu \(G\, které ale mají oba vrcholy v množině \(V(H)\).

![Podgraf](/Images/25/podgraf.png)

Speciální případ podgrafu je __indukovaný podgraf__. Indukovaný podgraf je podgraf \(H \subseteq G\), který obsahuje všechny hrany grafu \(G\) mezi dvojicemi vrcholů z \(V(H)\). Neboli, graf \(H\) vznikne smazáním části vrcholů grafu \(G\) a pouze hran, které z těchto vrcholů vycházeli.

![Indukovaný podgraf](/Images/25/indukovany_podgraf.png)

### Izomorfismus grafů
> Izomorfismus grafů \(G\) a \(H\) je __bijektivní__ zobrazení \(f: V(G) \to V(H)\), pro které každá dvojice \(u,v \in V(G)\) je spojená hranou v grafu \(G\) právě tehdy, když dvojice \(f(u), f(v) \in V(G)\) je spojená hranou v grafu \(H\).
>
> \[\exist F: V(G) \to V(G'): \{x,y\} \in E(G) \Leftrightarrow \{f(x), f(y)\} \in E(G')\]

Pro izomorfní grafy \(G\) a \(H\) platí:
- \(G\) a \(H\) mají stejný počet vrcholů.
- \(G\) a \(H\) mají stejný počet hran.
- Zobrazení \(f\) zobrazuje na sebe vrcholy stejných stupňů (tzn. mají stejné počty vrcholů o stejných stupních)

Postup důkazu izomorfismu dvou grafů je následující:
1. Ověříme, že oba grafy mají stejný počet vrcholů a hran.
2. Vytvoříme posloupnosti stupňů vrcholů pro každý graf (seřazeny od nejmenšího po největší) a ověříme, že jsou stejné.
3. Zkoušíme všechny přípustné možnosti zobrazení izomorfismu.

![Izomorfismus](/Images/25/izomorfismus.png)

#### Typy podgrafů v grafu
- Kružnice v grafu \(G\) je podgraf \(H \subseteq G\), který je izomorfní nějaké kružnici.
    - Indukovaná kružnice v \(G\) je indukovaný podgraf \(H \subseteq G\), který je izomorfní nějaké kružnici.
- Cesta v grafu \(G\) je podgraf \(H \subseteq G\), který je izomorfní nějaké cestě.
- Klika v grafu \(G\) je podgraf \(H \subseteq G\), který je izomorfní nějakému úplnému grafu.
- Nezávislá množina \(X\) v grafu \(G\) je podmnožina vrcholů \(X \subseteq V(G)\), mezi kterými nevedou v grafu \(G\) žádné hrany.

### Souvislost
Souvislost představuje možnost se v grafu pohybovat z jakéhokoliv vrcholu do libovolného jiného vrcholu podél jeho hran.

> Graf \(G = (V, E)\) je souvislý, jestliže pro každé dva jeho vrcholy \(u, v \in V(G)\) existuje sled z vrcholu \(u\) do vrcholu \(v\).

U orientovaných grafů rozlišujeme dva druhy souvislosti:
- __Slabá souvislost__ - Graf je slabě souvislý, pokud jeho symetrizace (odstranění směru hran) je souvislý graf.
- __Silná souvislost__ - Graf je silně souvislý, pokud pro každé dva vrcholy \(u\), \(v\) existuje cesta oběma směry.

> Relace \(\sim\) na množině vrcholů \(V(G)\) libovolného grafu \(G\) je definována tak, že \(u,v \in V(G)\) jsou v relaci \(u \sim v\) právě tehdy, když v grafu \(G\) existuje __sled__ začínající v \(u\) a končící ve \(v\). Tato relace je:
> - _Reflexivní_ - Každý vrchol je spojen sám se sebou sledem délky 0.
> - _Symetrická_ - Sled z \(u\) do \(v\) lze obrátit na sled z \(v\) do \(u\) vždy u neorientovaného grafu.
> - _Tranzitivní_ - Dva sledy na sebe můžeme vždy navázat v jeden sled.

Relace \(\sim\) je tedy relací __ekvivalence__.

#### Komponenty souvislosti
Komponenty souvislosti jsou jednoltivé __třídy ekvivalence__ grafu. Graf je souvislý, pokud má pouze jednu komponentu souvislosti. [TODO]

### Stromy
Strom je jednoduchý souvislý graf \(T\) bez kružnic (acyklický). Graf tvořený více stromy je pak zvaný __les__. Stromové grafy jsou zároveň kostrou grafu a platí pro ně:
- Pokud mají více než jeden vrchol, existuje vrchol se stupněm 1.
- Mezi každými dvěma vrcholi vede právě jedna cesta.

## Grafové algoritmy
