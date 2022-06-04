# Struktura překladače a charakteristika fází překladu
- Otázky: lexikální analýza, deterministická syntaktická analýza a generování kódu
- Předmět: IFJ (původně okruh 22)
- ToDo: Vytvoření LL tabulky a precedenční tabulky, obecně kontrola
- Zdroje:
    - https://www.fit.vutbr.cz/study/courses/IFJ/private/prednesy/Ifj02-cz.pdf (úvod do překladačů)
    - https://www.fit.vutbr.cz/study/courses/IFJ/private/prednesy/Ifj05-cz.pdf (lexikální analýza)
    - https://www.fit.vutbr.cz/study/courses/IFJ/private/prednesy/Ifj07-cz.pdf (syntaktická analýza shora dolů)
    - https://www.fit.vutbr.cz/study/courses/IFJ/private/prednesy/Ifj08-cz.pdf (syntaktická analýza zdola nahoru)
    - https://www.fit.vutbr.cz/study/courses/IFJ/private/prednesy/Ifj09-cz.pdf (syntaxí řízený překlad a generování vnitřního kódu)
    - https://www.fit.vutbr.cz/study/courses/IFJ/private/prednesy/Ifj10-cz.pdf (optimalizace a generování cílového programu)

## Překladač
Překladač je program, který převádí vstupní text obsahující zdrojový kód nějakého programu ve zdrojovém jazyce (zdrojový program) na cílový program, který je funkčně ekvivalentní se zdrojovým programem. Před samotným překladem je třeba určit, zda je zdrojový program v daném zdrojovém jazyce korektně zapsaný (je podmnožinou daného jazyka), neboli že neobsahuje chyby.

Překlad zdrojového programu na cílový se dělí na několik dílčích částí:
1. __Lexikální analýza__ - Text ve zdrojovém jazyce -> řetězec tokenů.
2. __Syntaktická analýza__ - Řetězec tokenů -> derivační strom.
3. __Sémantická analýza__ - Derivační strom -> abstraktní syntaktický strom.
4. __Generátor vnitřního kódu__ - Abstraktní syntaktický strom -> vnitřní kód.
5. __Optimalizátor__ - Vnitřní kód -> optimalizovaný vnitřní kód.
6. __Generátor cílového kódu__ - Optimalizovaný vnitřní kód -> cílový program.

Jednotlivé části překladače jsou většinou vzájemně provázané a často probíhají současně. Např.: jakmile lexikální analyzátor vygeneruje nějaký výstup, je hned předán syntaktickému analyzátoru ke zpracování. Některé části překladače také mohou být spuštěny i opakovaně.

![Struktura překladače](/Images/23/struktura_prekladace.png)

## Lexikální analýza
Lexikální analyzátor (__scanner__) je část překladače, která načítá zdrojový program jako textový vstup a identifikuje v něm jednotlivé __lexémy__ (platné posloupnosti znaků v daném jazyce). Jeho hlavní činnost je rozpoznávání a klasifikace lexémů. Přitom odstraňuje prázdná místa a komentáře v kódu.

Lexémy jsou reprezentovány __tokeny__, který v sobě nese:
- Typ lexému (číslo, identifikátor, klíčové slovo ...) - obvykle `int` (`enum`)
- Atribut - hodnota daného lexému - obvykle `union` nebo odkaz do tabulky tokenů.

Lexikální analyzátor může být implementován __deterministickým konečným automatem__, který je formálně specifikován pomocí __regulárních výrazů__. Lexikální analyzátor může už při identifikaci lexémů komunikovat s _tabulkou symbolů_.

Pro rozlišení identifikátorů od klíčových slov jazyka se používají _tabulky klíčových slov_.
O identifikátorech je potřeba uchovávat různé informace (názec, druh, datový typ, hodnota). K tomu se využívají __tabulky symbolů__. Tabulky symbolů bývají uložené v zásobníkové struktuře, což se používá pro implementaci oboru platnosti daného identifikátoru. Tabulky symbolů se v zásobníků prohledávají od vrcholu směrem ke dnu zásobníku.

## Syntaktická analýza
Syntaktický analyzátor (__parser__) je část překladače, která přijímá řetězec tokenů a vytváří z něj platný _derivační strom_ daného jazyka. Takto ověřuje správnou posloupnost po sobě jdoucích tokenů. Syntaktická analýza je rozdělena na dvě metody: __shora dolů__ a __zdola nahoru__.

![Derivační strom a abstraktní syntaktický strom](/Images/23/derivacni_strom.png)

### Metoda shora dolů
Syntaktická analýza shora dolů využívá __LL gramatiky__. Začíná největšími (neterminálními) prvky, které postupně dělí, dokud se nedostane k terminálním symbolům, které může porovnat se vstupem. Analýza je prováděna _zleva doprava_ (nejlevější derivace). Tento druh syntaktického analyzátoru bývá implementován pomocí __zásobníkových automatů__. Samotná implementace je provedena buď jako __rekurzivní sestup__ (každý neterminál je reprezentován procedurou) nebo jako __prediktivní syntaktická analýza__ (syntaktický analyzátor se zásobníkem řízený tabulkou).

Pro metodu shora dolů je nutné definovat:
- Bezkontextová gramatika
- Pravidla bezkontextové gramatiky
- __LL tabulku__ - Tabulka, která specifikuje _LL gramatiku_, neboli kdy se má použít jaké pravidlo.

__LL gramatika__ je speciální případ bezkontextové gramatiky. Může být bez epsilon pravidel nebo s epsilon pravidly. BKG jsou silnější než LL gramatiky. Některé BKG mohou být převedeny na ekvivalentní LL gramatiky pomocí následujících transformací:
- __Faktorizace__ - Faktorizace je zaměnění pravidel tvaru \(A \to xy_1,\; A \to xy_2\) na pravidla \(A \to xA',\; A' \to y_1,\; A' \to y_2\), kde \(A'\) je nový neterminál.
- __Odstranění levé rekurze__ - Odstranění levé rekurze je zaměnění pravidel tvaru \(A \to Ax,\; A \to y\) za pravidla \(A \to yA',\; A' \to xA',\; A' \to \varepsilon\), kde \(A'\) je nový neterminál.

LL gramatika je vyjádřena __LL tabulkou__, která se skládá z množiny _First_ pokud je bez epsilon pravidel a dále množiny _Empty_, _Follow_ a _Predict_ pokud je s epsilon pravidly:. 

- Množina __First__ - \(First(x)\) je množina všech terminálů, kterými může začínat řetězec derivovatelný z \(x\).

![Množina First](/Images/23/mnozina_first.png)

- Množina __Empty__ - \(Empty(x)\) je množina, která obsahuje jediný prvek \(\varepsilon\), pokud \(x\) derivuje \(\varepsilon\), jinak je prázdná.

![Množina Empty](/Images/23/mnozina_empty.png)

- Množina __Follow__ - \(Follow(A)\) je množina všech terminálů, které se mohou vyskytovat vpravo od \(A\) ve větné formě.

![Množina Follow](/Images/23/mnozina_follow.png)

- Množina __Predict__ - \(Predict(A \to x)\) je množina všech terminálů, které mohou být aktuálně nejlevěji vygenerovány, pokud pro libovolnou větnou formu použijeme pravidlo \(A \to x\).

![Syntaktická analýza založená na LL tabulce](/Images/23/sa_ll_tabulka.png)

### Metoda zdola nahoru
Syntaktická analýza zdola nahoru začíná vstupním textem, který se snaží postupně převést na počáteční symbol. Hledá nejprve pravidla obsahující dané terminální symboly, pak teprve pravidla, která mohou takovýmto pravidlům předcházet. Existuje několik typů syntaktických analyzátorů využívající metody zdola nahoru:
- __Precedeční syntaktický analyzátor__ - Nejslabší druh, který se ale snadno implementuje. Vyžaduje ke své funkci precedenční tabulku. Její gramatika nesmí obsahovat epsilon pravidla a nesmí existovat více pravidel se stejnou pravou stranou. Základ precedenční tabulky tvoří asociativita a precedence operátorů. Často se používá pro překlad matematických výrazů.
- __LR syntaktický analyzátor__ - Nejsilnější druh, který je ale složitý. Je založen na rozšířeném zásobníkovém automatu. Skládá se z akční a přechodové části.

![Precedenční syntaktická analýza](/Images/23/precedencni_sa.png)

## Sémantická analýza
Sémantický analyzátor je část překladače, která kontroluje sémantické aspekty programu. Přijímá derivační strom a vytváří z něj abstraktní syntaktický strom. Během toho provádí kontrolů typů (implicitní přetypování), kontrolu deklarací a další sémantické kontroly programu. V praxi se často používá __syntaxí řízený překlad__, při němž překladač kontroluje sémantiku už při vytváření derivačního stromu (při syntaktické analýze).

## Generátor vnitřního kódu
Generátor vnitřního kódu je část překladače, která konvertuje abstraktní syntaktický strom do vnitřního kódu. Tato část překladače je volitelná, ale často se implementuje kvůli výhodám, které vnitřní kód poskytuje. Často se jako vnitřní kód používá __trojadresné instrukce__ (tříadresný kód), který má následující výhody:
- Všechny jeho instrukce jsou zapsány jednotně.
- Snadno se převádí do cílového kódu narozdíl od přímého překladu, který je často složitý.
- Snadno se dá zoptimalizovat.

![Tříadresny kód](/Images/23/triadresny_kod.png)

## Optimalizátor
Optimalizátor je část překladače, která má za cíl optimalizovat vnitřní kód. Tato část překladače je volitelná, ale všechny významné překladače ji obsahují. Optimalizátor program rozdělí do __základních bloků__, což je sekvence příkazů, které se vždy musí vykonat v daném pořadí. Základní bloky se generují podle následujících pravidel:
- Hned první příkaz je _vedoucí_ (úvodní příkaz bloku).
- Každý příkaz, který je návěští je vedoucí.
- Každý příkaz za `goto` je vedoucí.

Na konec spočítáme počet vedoucích příkazů a tak získáme počet bloků. Z toho můžeme vytvořit graf bloků (podobný konečnému automatu). Z grafu lze zjistit, zda je nějaký blok nedostupný (mrtvý blok) a lze jej odstranit - __globální optimalizace__. V rámci jednoho bloku lze provádět __lokální optimalizace__.

Existují základní optimalizační metody:
- __Zabalení konstanty__
- __Šíření konstanty__
- __Kopírování promněnné__
- __Výrazové invarianty v cyklu__
- __Rozbalení cyklu__
- __Eliminace mrtvého kódu__

![Zabalení konstanty](/Images/23/optimalizace_1.png)
![Šíření konstanty](/Images/23/optimalizace_2.png)
![Kopírování proměnné](/Images/23/optimalizace_3.png)
![Výrzové invarianty v cyklu](/Images/23/optimalizace_4.png)
![Rozbalení cyklu](/Images/23/optimalizace_5.png)

Při optimalizaci často nastává konflikt mezi optimalizací _rychlosti_ a optimalizací _paměti_.

## Generátor cílového kódu
Generátor cílového kódu je část překladače, která převádí zoptimalizovaný kód do výsledného kódu programu. Výsledný kód může být např.: strojový kód nebo assembler. Jsou dva typy generování cílového kódu:
- __Slepé generování__ - Pro každou instrukci vnitřního kódu existuje procedura, která generuje příslušný cílový kód. Hlavní nevýhoda tohoto typu je, že každá instrukce je mimo kontext ostatních instrukcí bloku a dochází tedy k přebytečným načítáním a ukládáním proměnných.
- __Kontextové generování__ - Minimalizace počtu načítání a ukládání mezi registry a pamětí. Používá obecné pravidlo: Jestliže je hodnota proměnné v registru a bude brzy použita, tak je tam ponechána. K tomu používá tabulky: __Tabulka základního bloku__ TZB (které proměnné je potřeba a kde), __Tabulka registrů__ TR (obsah registrů), __Tabulka adres__ TA (kde je uložena aktuální hodnota proměnné).
