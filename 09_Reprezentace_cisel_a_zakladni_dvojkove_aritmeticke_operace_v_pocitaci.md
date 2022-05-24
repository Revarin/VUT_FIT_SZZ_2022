# Reprezentace čísel a základní dvojkové aritmetické operace v počítači
- Otázky: doplňkové kódy, sčítání, odčítání, násobení, pevná a plovoucí řádová čárka, standard IEEE 754
- Předmět: ISU
- Zdroje:
    - https://www.fit.vutbr.cz/study/courses/ISU/private/prednasky/isu-01-2015.pdf (čísla s pevnou řádovou čárkou)
    - https://www.fit.vutbr.cz/study/courses/ISU/private/prednasky/isu-10-2015.pdf (čísla s plovoucí řádovou čárkou)

## Zobrazení čísel dvojkové soustavy
Čísla lze v počítačích reprezentovat pouze v binární podobě. Existují různé způsoby binární reprezentace čísel, které mají různé vlastnosti a různě pracují s reálnými čísly. Tyto různé zápisy jsou charakterizovány následujícími vlastnostmi:
- __Rozsah zobrazení__ - Interval ohraničení zleva nejmenším a zprava největším zobrazitelným číslem. Závisí na počtu bitů.
- __Rozlišitelnost zobrazení__ - Nejmenší (kladné) zobrazitelné číslo.
- __Přesnost zobrazení__ - Počet platných dekadických číslic, které je možné zobrazit v paměťovém prostoru (hodnota nezávislá na velikosti zobrazovaného čísla).

## Pevná řádová čárka
Pevná řádová čárka (FX) je formát zobrazení dvojkových čísel, který přesně definuje počet bitů pro _celou část_ čísla a _desetinou část_ čísla. Dnes se tento způsob reprezentace využívá výhradně pro celá čísla (tudíž čísla bez desetinné části).

![Pevná řádová čárka](/Images/09/pevna_radova_carka.png)

### Reprezentace čísel se znaménkem
Reprezentace čísel se znaménkem má několik verzí:
- __Přímý kód__ - První bit čísla je rezervován pro znaménko (1 pro záporná čísla, 0 pro kladná čísla), kladné číslo se tak od svého záporného protějšku liší pouze v tomto bitě. Existuje zde však problém dvou nul (kladná nula a záporná nula). Také se zde může vyskytnout problémy u některých aritmetických operací. Používá se pro zobrazení reálných čísel v plovoucí řádové čárce.
- __Doplňkový kód__ (dvojkový doplněk) - Kladné číslo je reprezentováno normálně. Záporné číslo se z kladného čísla tvoří jeho inverzí a následně přičtením 1. Vytvoření kladného čísla ze záporného je provedeno stejně. Je zde pouze jedna reprezentace nuly a nevyskytují se žádné problémy aritmetickými operacemi. Je to nejčastěji používaný způsob reprezentace čísel se znaménkem.
- __Aditivní kód__ (kód s posunutou nulou, kód s transformovanou nulou) - Nejvyšší bit čísla reprezentuje opět znaménko, ale 0 je pro záporná čísla a 1 pro kladná čísla. Celý zápis čísla je tak posunut o nějakou konstantu. Používá se pro zobrazení reálných čísel v plovoucí řádové čárce.
- __Binary Coded Decimal__ (BCD) - Speciální binární zápis dekadických čísel, kde každá dekadická číslice je zobrazena v jednom _niblu_ (4 bity bytu). Znaménko může být v prvním bytu.

![Interval pro přímý kód](/Images/09/interval_primy_kod.png)
![Interval pro doplňkový kód](/Images/09/interval_doplnkovy_kod.png)
![Interval pro aditivní kód](/Images/09/interval_transformovany_kod.png)

### Aritmetické operace
__Sčítání__ se provádí stejně jako v desítkové soustavě. V případě sčítání v procesoru může pro čísla v doplňkovém kódu a kladná čísla v přímém kódu dojít k přetečení. Při sčítání čísel se znaménkem se kontrolují příznaky přenosu z (C) a do (P) nejvyššího bitu. Pokud jsou oba tyto příznaky aktivní nebo neaktivní zároveň, je výsledek správný, jinak se jedná o nesprávný výsledek.

![Sčítání binárních čísel](/Images/09/scitani.png)

__Odčítání__ se provádí stejně jako v desítkové soustavě. Je zde třeba brát v úvahu přenos. Přo odčítání čísel se znaménkem se kontrolují příznaky výpůjčky do (C) a z (P) nejvyššího bitu. Pokud jsou oba tyto příznaky aktivní nebo neaktivní zároveň, je výsledek správný, jinak se jedná o nesprávný výsledek.

![Odčítání binárních čísel](/Images/09/odcitani.png)

__Násobení__ se provádí stejně jako v desítkové soustavě. Výsledek zde může zabírat až dvojnásobný počet bitů, tudíž se musí ukládat do většího registru. V případě násobení čísel se znaménkem se nejdříve provede vynásobení s absolutními hodnotami čísel a poté je výsledné znaménko doplněno dle znamének čísel.

![Násobení binárních čísel](/Images/09/nasobeni.png)

__Celočíselné dělení__ je v počítači velmi náročná operace, která se může provádět různými metodami. V případě dělení čísel se znaménkem se nejdříve provede dělení s absolutními hodnotymi čísel a poté je výsledné znaménko doplněno dle znamének čísel. Obecně je postup následující:
1. Vezmeme část dělence, která je větší nebo rovna děliteli, ale menší jak dvojnásobek dělitele.
2. Provedeme podíl vybrané části (bude vždy 1) a zapíšeme do výsledku.
3. Zbytek si zapíšeme a připíšeme si další číslo z dělence. Pokud je část menší jak dělitel, do výsledku zapíšeme 0 a připíšeme další část.

![Celočíselné dělení binárních čísel](/Images/09/deleni.png)
![Tabulka celočíselného dělení se znaménkem](/Images/09/deleni_tabulka.png)

V omezeném paměťovém prostoru musíme brát v potaz __přenos__ (Carry) z nejvyššího bitu a __výpůjčku__ (Borrow) do nejvyššího bitu. Pokud tyto události nastanou na bitu mimo paměťový rozsah, nastává __přetečení__, a je nutné nastavit odpovídající příznaky, které tuto skutečnost signalizují.

## Plovoucí řádová čárka
Plovoucí řádová čárka (__floating point__, FP) je speciální způsob zápisu reálných čísel. Narozdíl od _pevné řádové čárky_ umožňuje reprezentovat čísla s různou přesností a rozsahem (čísla nejsou na číselné ose rozložena rovnoměrně - čím větší číslo, tím menší přenost a naopak). V dnešní době se pro reprezentaci reálných čísel používá standard __IEEE754__ pro reprezentaci čísel v plovoucí řádové čárce.

Číslo s plovoucí řádovou čárkou je rozděleno na několik částí: __znaménkový bit__ (S), __mantisa__ (M), __základem__ (B) a __exponentem__ (E).

> __Kódování čísel s plovoucí řádovou čárkou__
>
> \(x_{FP} = (-1)^S \times B^E \times M\)

\[
x = 4,2 \\
4,2 \times 2^0 \rightarrow 0,42 \times 2^1 \\
S = 0;~B = 2;~E = 1;~M = 42_D = 101010_B \\
\rightarrow S|E|M = 0|0000001|101010
\]

Pro malá čísla je potřebný záporný exponent (\(2^{-1}=0,5\)). Používá se sudý nebo lichý posun __BIAS__. Rozsah exponentu se rozdělí na polovinu a podle sudého/lichého BIAS se nula nachází buď v sudém nebo v lichém čísle rozsahu. Nula je tak umístěna (exponent s rozsahem \(2^5\)) na hodnotě \(32/2=16\) pro sudé BIAS, nebo na hodnotě \(32/2-1=15\) pro liché BIAS. Výhoda tohoto zápisu je, že exponent zůstaně vždy kladný. Vzorec číslo s plovoucí řádovou čárkou pak vypadá:

> \(x_{FP} = (-1)^S \times B^{E - BIAS} \times M\)

Při tomto zápisu nastává problém, že zobrazení čísel není unikátní. To je řešeno tak, že mantisa bude vždy začínat jedničkou. Pro zjednodušení zápisu a ušetření jednoho bitu je možné v mantise čísla vynechat první jedničku, neboť je tam vždy (\(1.011 \rightarrow .011\)) - __implicitní jednička__. Opačný případ, kde je nutné tuto jedničku zapisovat, se nazývá __explicitní jednička__.

Čísla s plovoučí řádovou čárkou obsahují ze své podstaty jistou chybu. Existuje několik druhů chyb, které mohou ovlivnít správnost daného čísla:
- __Chyba měření__ - Vzniká při pořizování čísla vlivem chyby metody měření.
- __Chyba stupnice__ (scaling) - Zvolená číselná soustava nemůže na konečném počtu míst vyjádřit přesně všechny hodnoty.
- __Chyba zanedbáním__ (truncation) a __chyba zaokrouhlením__ (rounding)
- __Chyba zobrazení__ - Protože se číslo v binárním zápisu skládá ze součtu zlomků druhé mocniny, není možné na konečné délce čísla (registru) reprezentovat všechna čísla. Dochází tak k nepřesnostem. Chyba zobrazení je rovna: \(E_{FP}=(B^{E-1} + B^{E-1}) / B^{Délka~M - (1~if~norm.~M < 1)}\)

![Číslo v plovoucí řádové čárce](/Images/09/floating_point.png)

### Standard IEEE754
IEEE754 je standard pro reprezentaci čísel v plovoucí řádové čárce. Tento standard definuje několik způsobů zápisu:
- __Float__ (jednoduchá přesnot) - 32 bitů, kde E = 8b, M = 23b
- __Double__ (dvojitá přenost) - 64 bitů, kde E = 10b, M = 53b
- _Základní rozšířená přesnost_ - více než 43 bitů
- _Dvojitá přenost_ - více než 79 bitů

Norma počítá s implicitní jedničkou v mantise. Dále tento standard definuje hodnoty se speciálním významem pro _float_ a _double_.

|Exponent|Mantisa|Hodnota|
|-|-|-|
|0|0|přesná nula|
|255|0|nekonečno|
|0|not 0|denormalizované číslo|
|255|not 0|_not a number_ (NaN)|

### Aritmetické operace
__Součin__ čísel s plovoucí řádovou čárkou není asociativní (chyba). Je to vlastně součin vynásobených mantis a základu na součet exponentů (\(X \times Y = (M_X \times M_Y) \times B^{E_X + E_Y}\)).

__Sčítání__ a __odčítání__ čísel s plovoucí rádovou čárkou se provede převodem obou čísel na stejný exponent a následným sečtením/odečtením mantis obou čísel.
