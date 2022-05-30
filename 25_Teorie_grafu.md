# Teorie grafů
- Otázky: pojem grafu, isomorfismus grafů, souvislost, grafové algoritmy
- Předmět: IDM (nový okruh)
- ToDo: Příklady
- Zdroje:
    - https://www.umat.fekt.vut.cz/~hlinena/IDM/Prednasky/grafy1.pdf
    - https://www.umat.fekt.vut.cz/~hlinena/IDM/Prednasky/grafy2.pdf
    - https://www.umat.fekt.vut.cz/~hlinena/IDM/Prednasky/grafy3.pdf

## Graf
Graf je speciální případ binární relace. Skládá se z vrcholů a hran, které tyto vrcholy propojují.

> Jednoduchý neorientovaný graf je uspořádaná dvojice \(G = (V, E)\), kde
> - \(V\) je množina vrcholů.
> - \(E\) je množina hran - množina vybraných dvouprvkových podmnožin z množiny vrcholů \(V\)

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

- __Úplný graf__ - Graf s \(n \geq 1\) vrcholy, z nichž každý vrchol je spojen se všemi ostatními vrcholy. Celkem má graf \(\binom{n}{2}\) hran. Značí se \(K_n\).

![Úplný graf](/Images/25/uplny_graf.png)

- __Úplný bipartitní graf__ - Úplný graf, jehož vrcholy jsou rozděleny do dvou skupin (partit) o velikosti \(m \geq 1\) a \(n \geq 1\). Každý vrchol skupiny je spojen se všemi vrcholy druhé skupiny, jsou spojeny všechny \(m.n\) dvojice. Značí se jako \(K_{m,n}\).

![Úplný bipartitní graf](/Images/25/uplny_bipartitni_graf.png)

- __Hvězda__ - Graf s \(n \geq 1\) rameny je zvláštní případ úplného bipartitního grafu. Značí se jako \(K_{1,n}\).

![Hvězda](/Images/25/hvezda.png)

- __Sled__ - Sled je v grafu __posloupnost vrcholů__ taková, že mezi každými dvěma po sobě jdoucími vrcholy je hrana. Hrany i vrcholy se mohou na rozdíl od kružnice opakovat. Sled je tedy průchod po hranách grafu z \(u\) do \(v\), který může obsahovat cykly.
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
> - Za hrany má libovolnou podmnožinu hran grafu \(G\), které ale mají oba vrcholy v množině \(V(H)\).

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
- Mezi každými dvěma vrcholy vede právě jedna cesta.

## Grafové algoritmy
Grafové algoritmy umožňují algoritmicky zpracovat (projít) graf. Typicky využívají nějakou paměť - zásobník, frontu, seřazené pole.

### Prohledávání do šířky
Prohledávání do šířky (BFS) je grafový algoritmus, který postupně prochází celé úrovně grafu od počátečního vrcholu. Jako paměť využívá __frontu__. Funkce algoritmu BFS je následující:
1. První vrchol grafu se vloží do fronty.
2. Pokud není fronta prázdná, zpracuje se vrchol na začátku fronty. Zpracování vrcholu znamená umístění vrcholů, do kterých vede hrana ze zpracovaného vrcholu, do fronty. Tento krok se cyklicky opakuje.

Algoritmus BFS lze použít pro zjištění nejkratší vzdálenosti mezi dvěma vrcholy spojitého _neváženého_ grafu.

### Prohledávání do hloubky
Prohledávání do hloubky (DFS) je grafový algoritmus, který prochází nejprve do co nejvzdálenější úrovně grafu a poté se postupně vynořuje a zase co nejvíce zanořuje. Jako paměť využívá __zásobník__. Algoritmus DFS pracuje následovně:
1. První vrchol grafu se vloží na zásobník.
2. Pokud není zásobník prázdný, zpracuje se vrchol na vrcholu zásobníku. Zpracování vrcholu znamená umístění vrcholů, do kterých vede hrana ze zpracovaného vrcholu, na zásobník. Tento krok se cyklicky opakuje.

### Dijkstrův algoritmus
Dijkstrův algoritmus je algoritmus pro hledání _nejkratší_ cesty mezi dvěma vrcholy \(u\) a \(v\) v __kladně váženém__ grafu. Jako uložiště používá _prioritní frontu_. Může pracovat s časovou komplexitou \(O((h+v) * \log{v})\) nebo \(O(v^2)\) při použití pole. Princip Dijkstrova algoritmu je následující:
1. Všechny vrcholy grafu až na počáteční jsou ohodnoceny _nekonečnem_ (neznáme do nich cestu) a počáteční vrchol je ohodnocen 0. Všechny vrcholy jsou označeny za nezpracované.
2. Z nezpracovaných vrcholů vybereme ten s nejmenší hodnotou (leží na začátku prioritní fronty, v první iteraci to bude počáteční vrchol \(u\)). Pokud je tento vrchol hledaným vrcholem \(v\), ukončíme algoritmus. Jinak přepíšeme vzdálenosti všech vrcholů (již zpracované ignorujeme), do kterých se můžeme z vybraného vrcholu dostat hranou, přičtením ohodnocení této hrany k hodnotě zpracovávaného vrcholu, pokud je tato hodnota __menší__ než aktuální ohodnocení. V tomto případě si také zaznamenáme, přes jaký vrchol vede tato nejkratší cesta.
3. Aktuálně zpracovávaný uzel označíme za zpracovaný a pokud jsou ještě nezpracované vrcholy, pokračujeme 2. bodem.
4. Zpětně rekonstruujeme _cestu_ z cílového vrcholu \(v\) k startovacímu vrcholu \(u\) na základě zapamatovaných údajů v bodě 2.

### Jarníkův (Primův) algoritmus
Jarníkův (Primův) algoritmus je grafový algoritmus, který hledá __minimální kostru__ ve _váženém grafu_ (stromový podgraf, který propojuje všechny vrcholy) - __minimum spanning tree__. Jako uložiště může použít např. _prioritní frontu_ pro nenavštívené vrcholy. Princip algoritmus je následující:
1. Do uložiště se uloží všechny vrcholy s ohodnocení _nekonečno_ (ještě nejsou v kostře).
2. Z tohoto uložiště se vybere libovolný uzel grafu, změní se jeho ohodnocení na 0 a odstraní se z uložiště.
3. U dosud nenavštívených vrcholů (jsou v uložišti), do kterých se lze z vybraného vrcholu dostat, se aktualizují jejich ohodnocení hodnotou cesty k tomuto vrcholu, pokud je tato hodnota menší než aktuální. Vrchol, ze kterého tato cesta vede se zapíše.
4. Z uložiště se vybere vrchol s nejmenším ohodnocení a z uložiště se odstraní.
5. Pokud uložiště není prázdné pokračuje se bodem 3.
6. Zpětně rekonstruujeme použité hrany.

### Kruskalův algoritmus
Kruskalův algoritmus je algoritmus pro hledání minimální kostry ve váženém grafu. Pracuje na principu, že z grafu vybíráme vždy hranu s nejmenším ohodnocením tak, aby se nevytvořila kružnice, dokud nejsou spojeny všechny vrcholy. Časová složitost algoritmu je \(O(|E|* \log{|V|})\).

## Příklady
Příklady průchodů grafy
