# Sekvenční logické obvody
- Otázky: sekvenční logické obvody, klopné obvody (RS, JK, T, D), čítače, registry, stavové automaty (reprezentace a implementace)
- Předmět: INC
- Zdroje:
    - https://wis.fit.vutbr.cz/FIT/st/cfs.php.cs?file=%2Fcourse%2FINC-IT%2Flectures%2F04+sekvencni_obvody.pdf (sekvenční obvody)
    - https://wis.fit.vutbr.cz/FIT/st/cfs.php.cs?file=%2Fcourse%2FINC-IT%2Flectures%2F03-klopne_obvody.pdf (klopné obvody)

## Sekvenční logické obvody
Sekvenční logické obvody mají na rozdíl od kombinačních logických obvodů vnitřní stav, který si pamatují. Výstup \(Y\) sekvenčních obvodů je tedy závislý na vstupu \(X\) a aktuálním vnitřním stavu \(Q\). Vnitřní stav se mění na základě vstupu a aktuální vnitřního stavu podle _přechodové funkce_ \(P\). Tyto logické obvody se skládají ze dvou částí - kombinační a paměťové.

Sekvenční logické obvody mohou být asynchronní a synchronní:
- __Asynchronní (Latch)__ - Vstupní signály přímo ovlivňují stav sekvenčního obvodu. Mají dva režimi činnosti:
    - _Fundamentální režim činnosti_ - Vstupní proměnné musí být po jistou dobu stabilní (bez pulsů), aby na ně sekvenční obvod mohl reagovat. Paměťové prvky jsou realizovány pomocí zpožďovacích linek. V jednom okamžiku se může měnit hodnota pouze na jednom vstupu a musí se počkat na ustálení zpětných vazeb.
    - _Pulsní režim činnosti_ - Vstupní proměnné jsou aktivní jen po jistou dobu - puls. Je jeden puls může být na vstupu aktivován v daný okamžik. Paměťové prvky jsou řízeny pouze vstupními pulsy.
- __Synchronní (Flip-Flop)__ - Vstupní signály ovlivňují stav sekvenčního obvodu pouze při aktivním stavu _hodinového signálu_. Činnost obvodu je tak synchronizována. Obvod může na hodinový signál reagovat dvěma způsoby:
- __Úrovňový__ sekvenční obvod - Sekvenční obvod sleduje vstupy po celou dobu hodinového signálu a průběžně na ně reaguje. Hodinový signál je tak aktivní jako _puls_ - __dvooufázový sekvenční obvod__.
- __Hranový__ sekvenční obvod - Sekvenční obvod reaguje na vstupy jen při přechodu hrany (náběžné nebo sestupné) hodinového signálu. Hodinový signál je tak aktivní jako _hrana_ - __derivační klopný obvod__.

### Konečný automat
Sekvenční logické obvody lze modelovat pomocí __sekvečního automatu/konečného automatu__ (Finite State Machine). Sekvenční automat je sekvenční obvod, který se skládá z tří částí:
- __Next-state__ logika - Kombinační síť, která na základě současného vstupu a hodnoty vstupů generuje následující stav automatu.
- __Paměť__ - Registr sestavený z klopných obvodů s dynamickým řízením hodinovým signálem. Pamatuje si současný stav automatu. Paměť musí být před zahájením práce s automatem inicializována.
- __Výstupy__ - Mealyho a Moorovy výstupy.
    - __Mooreovy výstupy__ - Výstup závisý pouze na vnitřním stavu.
    - __Mealyho výstupy__ - Výstup závisý na vnitřním stavu a vstupu.

Příkal __Mooreův automatu__ a __Mealyho automatu__.

![Mooreův automat](/Images/03/mooreuv_automat.png)
![Mealyho automat](/Images/03/mealyho_automat.png)

> Sekvenční automat \(A\) je uspořádaná šestice \(A=(X,Y,Q,q_0,P,V)\), kde:
> - \(X\) je vstupní abeceda.
> - \(Y\) je výstupní abeceda.
> - \(Q\) je vnitřní abeceda.
> - \(q_0\) je počáteční stav.
> - \(P\) je přechodová funkce \(X \times Q \rightarrow Q\).
> - \(V\) je výstupní funkce \(X \times Q \rightarrow Y\) (Mealyho nebo Moorova).

Chování konečného automatu je možné zapsat pomocí grafu přechodů nebo tabulky přechodů.

![Graf přechodů](/Images/03/stavovy_automat_graf.png)
![Tabulka přechodů](/Images/03/stavovy_automat_tabulka.png)

![Konečný automat](/Images/03/konecny_automat.png)

### Zpoždění signálů
Zpoždění signálů v sekvenčním logickém obvodu může být tří druhů:
- __Inerční__ zpoždění signálu - Zpoždění způsobeno setrvačností prvků (parazitní kapacity). Puls musí mít alespoň délku inerčního zpoždění, jinak obvodem neprojde.
- __Transportní__ zpoždění signálu - Zpoždění dáno rychlostí šíření signálu daném médiu.
- __Zpožďovací linka__ - Informace poslaná na vstup nějakého prvku se na výstupu projeví až po určitém čase. Každý prvek tak přidává další zpoždění.

## Klopný obvod
Klopný obvod je jednoduchý sekvenční obvod se dvěma (nebo více) diskrétními stavy. Slouží jako základní stavební prvek pro složitější sekvenční sítě. Mezi stavy klopný obvod přechází skokově. Klopné obvody jsou schopny, pomocí zpětné vazby, uchovávat svůj stav a tak se často využívají jako paměťové prvky. Jsou __volatilní__, informaci lze rychle číst i ukládat, ale po vypnutí napájení se ztrácí.

Základní princip činnost klopných obvodů je zavedení __zpětné vazby__ do kombinační logické sítě. Tím lze dosáhnout paměťového jevu.

![Zpětná vazba](/Images/03/zpetna_vazba.png)

Klopné obvody mohou být asynchronní nebo synchronní:
- __Asynchronní__ klopný obvod (Latch) - Obvod zachytí impuls a zapamatuje si jeho hodnotu (záchytný obvod). Neobsahuje hodinový signál, vstupní signál přímo řídí stav klopného obvodu. Může navíc obsahovat i pomolovací vstup.
- __Synchronní__ klopný obvod (Flip-Flop) - Obvod má vstup pro hodinový signál, který synchronizuje jeho chování. Obvod mění svůj stav a výstupy pouze pokudj e aktivní hodinový signál (hrana hodinového signálu).

Podle způsobu paměťové funkce se klopné obvody dělí na:
- __Monostabilní__ klopný obvody - Klopný obvod má jeden stabilní stav, ze kterého se obvod překlopí pouze se spouštěcím impulsem. Používají se jako tvarovače impulsů, časovače, atd.
- __Bistabilní__ klopný obvod - Klopný obvod má dva ustálené stavy, ve který lze zůstav libovolnou dobu. Lze je využívat jako paměť.
- __Astabilní__ klopný obvod - Klopný obvod nemá ustálený stav. Jejich výstup se přepíná mezi 0 a 1. Lze je použít jako generátory obdélníkového signálu.

### RS Klopný obvod
RS klopný obvod má dva vstupy: R (_Reset_), který změní stav obvodu na log. 0, a S (_Set_), který změní stav obvodu na log. 1. Obvod si svůj stav pamatuje a opakovaná aktivace stejného vstupu nemá žádný vliv. Vstupy RS klopného obvodu jsou invertované, tudíž jsou aktivní v log. 0. Aktivace obou vstupů R a S je zakázaná (neznámý stav).

![RS klopný obvod](/Images/03/rs_klopny_obvod.png)

RS klopný obvod lze rozšířit o _povolovací vstup_ C. Tento vstup povolí funkci klopného obvodu pouze pokud je aktivní.

![RS klopný obvod s povolovacím vstupem](/Images/03/rs_klopny_obvod_povolovaci.png)

### JK Klopný obvod
JK klopný obvod je rozšíření RS klopného obvodu, které podporuje původně zakázaný stav, kdy jsou R a S vstupy aktivovány zároveň. Vstupy nazýváme J (místo S) a K (místo R). Aktivace J a K zároveň překlápí vnitřní stav obvodu. JK klopný obvod jinka funguje stejně jako RS.

![JK klopný obvod](/Images/03/jk_klopny_obvod.png)

### T klopný obvod
T (toggle) klopný obvod je rozšíření JK klopného obvodu. T klopný obvod má jeden vstup T, který při aktivaci (log. 1) překlápí aktuální stav klopného obvodu

![T klopný obvod](/Images/03/t_klopny_obvod.png)

### D klopný obvod
D (hold) klopný obvod je další rozšíření RS klopného obvod. Vstup D je připojen na vstup S a invertovaně připojen na vstup R. Na nástupné hraně hodinového signálu ukládá aktuální stav na vstupu D.

![D klopný obvod](/Images/03/d_klopny_obvod.png)

D klopný obvod lze použít jako jednobitový registr.

## Posuvný registr
Posuvný registr je sekvenční logický obvod, který ukládá a posouvá vstupní hodnotu. Posuvný registr je možné sestavit z několika sériově napojených D klopných obvodů. Posuvný registr mění stav při nástupné hraně hodinového signálu.

![Posuvný registr](/Images/03/posuvny_registr.png)

Posuvný registr je možné implementovat i pomocí multiplexorů - _barrel shifter_. 

## Čítač
Čítač je sekvenční logický obvod, který čítá vstupní impulsy. Po přetečení často čítač začíná znovu čítat od začátku. Čítač je možné sestavit z několika sériově napojených T klopných obvodů. Čítač může být asynchronní a synchronní:
- _Asynchronní čítač_ - Neobsahuje synchronizační hodiny.
- _Synchronní čítač_ - Obsahuje synchronizační hodiny.

![Čítač](/Images/03/citac.png)
