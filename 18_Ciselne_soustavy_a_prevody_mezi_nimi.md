# Číselné soustavy a převody mezi nimi
- Otázky:
- Předmět: ISU
- Zdroje:
    - https://www.fit.vutbr.cz/study/courses/ISU/private/prednasky/isu-01-2015.pdf

## Číselné soustavy
Číselné soustavy jsou uspořádané množiny symbolů - __číslic__, pomocí nichž se vyjadřují čísla. Každá číselná soustava je charakterizována __základem (bází) číselné soustavy__, který vyjadřuje maximální počet číslic, který je v dané soustavě k dispozici. Nejčastěji používané číselné sosutavy jsou: _dekadická s._, _dvojková s._ (binární), _osmičková s._ (oktalová) a _šestnácková s._ (hexadecimální).

Číselné soustavy mohou být buď polyadické nebo nepolyadické:
- __Polyadické soustavy__ - V těchto soustavách je číslo reprezentováno posloupností, ve které se jednotlivé číslice násobí základem soustavy umocněným podle pozice číslice v čísle. Neboli čísla v těchto soustavách jdou zapsat __polynomiálním zápisem__. Většina používaných číselných soustav jsou polyadická.
- __Nepolyadické soustavy__ - V těchto soustavách čísla nejdou zapsat polynomiálním zápisem. Je to například _římská číselná soustava_.

### Polynomiální zápis
Polynomiální zápis čísla je zápis čísla, ve kterém se jednotlivé číslice násobí základem soustav umocněným podle pozice číslice v čísle. Polynomiální zápis je možný pro _polyadické soustavy_, kde je číslo reprezentováno posloupností.

\[
    N = \sum_{i=-l}^{k-1} n_i \times B^i \\\;\\
    8456 = 8 \times 10^3 + 4 \times 10^2 + 5 \times 10^1 + 6 \times 10^0
\]

### Poziční zápis
V pozičním zápisu čísla pozice každé číslice představuje její relativní váhu významnosti. Píše se v závorce a za závorkou se značí základ soustavy.

\[\pi \dot{=} (3,14)_{10}\]

## Převody mezi soustavami
Pro převod mezi dvěma různými soustavami existuje několik metod:
- Substituční metoda
- Metoda dělení základem
- Metoda násobení základem

### Substituční metoda
Substituční metodu lze použít obecně pro převod mezi libovolnými soustavami. Je __vhodná__ pro vzájemný převod mezi binární, oktalovou a hexidecimální soustavou, nebo pro převod těchto soustav do dekadické soustavy. Je __nevhodná__ pro převod z dekadické soustavy do ostatních. Postup:
1. Číslo, které chceme převést vyjádříme polynomiálním zápisem.
2. Spočtou se mocniny čísel, každá mocnina se vynásobí hodnotou příslušné číslice a vše se sečte.

![Příklad substituční metody](/Images/18/substitucni_metoda.png)

### Metoda dělení základem
Metoda dělení základem je __vhodná__ pro převod celých čísel mezi soustavami, zvláště pak pro převod z dekadické soustavy do ostatních. Postup:
1. Číslo se postupně celočíselně dělí základem cílové soustavy dokud nám jako výsledek nevyjde nula.
2. Výsledné číslo získáme složením zbytků po dílčích dělení v opačném pořadí (poslední zbytek je MSB, první je LSB).

![Příklad metody dělení základem](/Images/18/metoda_deleni_zakladem.png)

### Metoda násobení základem
Metoda násobení základem je __vhodná__ pro převod desetinných čísel mezi soustavami. Postup:
1. Číslo násobíme základem soustavy, do které ho chceme převést.
2. Po každém kroku se sepisuje celočíselná část výsledku a převod končí, když je výsledek násobení roven nule nebo přesáhne požadované přesnosti.

![Příklad metody násobení základem](/Images/18/metoda_nasobeni_zakladem.png)

## Desetinná čísla
Převod desetinných čísel (s pevnou řádovou čárkou) je podobný jako převod celých čísel. První číslice za desetinou čárkou je v řádu \(B^{-1}\).

![Příklad převodu desetinného čísla](/Images/18/prevode_desetineho_cisla.png)
