# Kombinační logické obvody
- Otázky: kombinační logické obvody, multiplexor, demultiplexor, kodér, dekodér, binární sčítačka
- Předmět: INC, INP
- Zdroje:
    - https://wis.fit.vutbr.cz/FIT/st/cfs.php.cs?file=%2Fcourse%2FINC-IT%2Flectures%2F02-kombinacni_obvody.pdf

## Logické obvody
Logický obvod je hierarchicky uspořádaný obvod, ve kterém jednotlivé komponenty zpracovávají a mezi sebou komunikují informaci reprezentovanou v binární podobě. Logické obvody se dělí na dva základní typy: __kombinační__ a sekvenční. Kombinační logické obvody mají vstup a výstup, který je závislý pouze na aktuálním vstupu (žádný vnitřní stav, žádná paměť). Tyto obvody se skládají ze stavebních bloků zvané logické členy.

![Schéma logických hradel](/Images/02/logicke_hradla.png)

## Multiplexor
Multiplexor (MX) je kombinační logická síť, která přepíná signál z více vstupů na jeden výstup. Pracuje tedy jako přepínač. Podle binární kombinace na řídícím vstupu \(S\) (Select) se vybere jeden ze vstupů \(X_i\), jehož úroveň se přenese na výstup \(Y\). Multiplexor se označuje podle poměru přepínání, např.: 2-1, 4-1.

![Multiplexor komponenta](/Images/02/multiplexor_hradlo.png)
![Multiplexor schéma](/Images/02/multiplexor_schema.png)

Multiplexory vyššího poměru lze skládat z multiplexorů nižšího poměru. Nižší multiplexor tak označuje pouze menší počet bitů z celkové adresy. Multiplexor se využívá pro převod paralelního vstupu na sériový (data selector) nebo pro tvorbu vlastních logických funkcí.

## Demultiplexor
Demultiplexor (DMX) je kombinační logická síť, která mapuje vstup na jeden z několika výstupů. Pracuje tedy jako přepínač. Podle binární kombinace na řídícím vstupu \(S\) (Select) se vybere na který výstup \(Y_i\) se úroveň signálu \(I\) pošlě. Demultiplexor se označuje podle poměru, např.: 1-2, 1-4.

![Demultiplexor komponenta](/Images/02/demultiplexor_hradlo.png)
![Demultiplexor schéma](/Images/02/demultiplexor_schema.png)

Demultiplexor se používá jako datový distributor nebo pro implementaci vlastních logických funkcí.

## Dekodér
Dekodér (DC) je kombinační obvod, který funguje velmi podobně jako multiplexor, který má na vstupu vždy log. 1. Binární kombinace na vstupu \(S\) (o velikosti \(N\)) určuje, jaký z \(2^N\) výstupů \(Y\) bude aktivní (log. 1). Vždy bude aktivní pouze jeden výstup.

![Dekodér komponenta](/Images/02/dekoder.png)

Dekodér se využívá například pro dekódování adres, jako dekodéry pro sedmisegmentové displeje a taky pro převod BCD na číslo 1-10 (_dekodér BCD_). Také lze použít pro generování logických funkcí.

## Kodér
Kodér (C) je kombinační obvod, pro každý vstup z více vstupů produkuje unikátní výstup. Má vlastně opačnou funkci k dekodéru. Na výstup \(Y\) (o velikosti \(N\)) mapuje binární adresu právě aktivního vstupu ze \(2^N\) vstupů. Pouze jeden vstup může být v daný okamžik aktivní, jinak není výstup kodéru platný (vyplývá z definice kodéru).

![Kodér komponenta](./Images/02/koder.png)

Kodér se využívá například pro prioritní kodér (přidělování sběrnice, řadič přerušení) a pro převody kódů.

## Binární sčítačka
### Neúplná sčítačka
Nejjednodušší sčítačka se nazývá __Half-adder__ (HA). Tato sčítačka má pouze dva vstupy, nebere v potaz předchozí přenos (_carry_). Má dva výstupy: výsledek __S__ a příznak přenosu __C__.

![Half-adder](./Images/02/half-adder.png)

### Úplná sčítačka
Při rozšíření o přenos vzniká __Full-adder__ (FA). Tato sčítačka bere v potaz přenos z nižšího řádu.

![Full-adder](./Images/02/full-adder.png)

### Sériová sčítačka
Plná sčítačka se v praci pro vícebitové sčítání nepoužívá, poněvadž je příliš pomalá a složitá. Pro zjednodušení lze využít sériovovou sčítačku, která má vstupy a výstupy v posuvných registrech a carry v jednoduchém registru. Nicméně tato sčítačka je stále velmi pomalá.

![Seriová sčítačka](./Images/02/seriova_scitacka.png)

### Rozšířená sčítačka
V praxi se využívá CLA sčítačka (Carry-Look-Ahead). Tato sčítačka má navíc výstupy G (_Generate carry_) a P (_Propagate carry_), které umožňují paralelně generovat přenos:
- __G__ (generate) - značí případ, kdy __určitě__ nastane přesun do vyššího řádu
- __P__ (propagate) - značí případ, kdy __může__ nastat přesun do vyššího řádu

Jednotlivé výstupy CLA sčítačky se vypočítají následovně:
- \(C_{i+1} = G_i\,and\,(P_i\,or\,C_i)\)
- \(S_i = A\,xor\,B\,xor\,C_i\)
- \(G_i = A\,and\,B\)
- \(P_i = A\,xor\,B\)

![CLA sčítačka](./Images/02/cla_scitacka.png)
![Vícebitová sčítačka](./Images/02/cla_scitacka_vicebitova.png)
