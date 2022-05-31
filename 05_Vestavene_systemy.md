# Vestavěné systémy
- Otázky: mikrokontrolér, periferie, rozhraní, převodníky
- Předmět: IMP
- Zdroje:
    - https://wis.fit.vutbr.cz/FIT/st/cfs.php.cs?file=%2Fcourse%2FIMP-IT%2Flectures%2F04-IMP-seriova_kom.pdf&cid=13324 (sériová komunikace)
    - https://wis.fit.vutbr.cz/FIT/st/cfs.php.cs?file=%2Fcourse%2FIMP-IT%2Flectures%2F04-IMP-GPIO.pdf (porty a obecný I/O)
    - https://wis.fit.vutbr.cz/FIT/st/cfs.php.cs?file=%2Fcourse%2FIMP-IT%2Flectures%2F09-IMP-Analog.pdf (analogový převodník)

## Vestavěné systémy
> Vestavěný systém je definován jako kombinace hardwaru a softwaru, jejímž smyslem je řídit nějaký externí proces, zařízení nebo systém.

Vestavěný systém (Embedded system) je jednoúčelový počítač, který je zabudován do zařízení, které ovládá. Na rozdíl od univerzálních počítačů jsou vestavěné systémy _specializované_ a mají předem určenou činnost, kterou řídí. Obvykle nijak neiteragují s uživatelem, který často ani neví, že se jedná o počítač. Snaží se o:
- __Reaktivnost__ - odezva v reálném čase.
- __Autonomii__ - funguje bez zásahu člověka.
- __Kritičnost__ - bezpečně vykonává svoji funkci (spolehlivé a bezpečné).

Základní vlastnosti vestavěných systémů jsou tedy:
- Omezená množina aplikačních systémů (vykonává pouze jeden úkol).
- Často zpracování fyzikálních veličin.
- Měli by být spolehlivé, bezpečné, zabezpečené a efektivní.
- Často mají pouze jeden program po celý život.
- Hlavní interakce nemusí být s člověkem.

Přestože je funkce vestavěného systému specializovaná, nechceme pro každý systém vyvíjet nový integrovaný obvod (časově a finančně náročené, neflexibilní). Proto je základem vestavěných systémů __mikrokontrolér__ a na něj jsou napojeny dle potřeby periferní zařízení (senzory, display, ...).

### Mikrokontrolér
Mikrokontrolér (MCU) je integrovaný obvod implementující kompletní počítač. Obsahuje základní komponenty počítače (instrukční dekodér, ALU, registry, řadič, sběrnice). Lze jej programovat v normálních programovacích jazycích (nejčastěji C). Navíc od běžných procesorů obsahují i některé specializovanější komponenty, např. AD/DA převodníky, programovatelné časovača aj.

Mikrokontroléry můžeme podle jejich architektury dělit na:
- __Von Neumanovská architektura__ MCU - Společná paměť pro program i data. Je flexibilnější pro měnící se aplikace, ale pomalejší. Pro vestavěné systémy často není potřeba.
- __Hardvardská architektura__ MCU - Oddělená paměti pro program a data. Program může být tak uložen i v paměti jiného typu než data. Umožňuje v jednom taktu z paměti číst instrukci i data. Díky tomu může být procesor rychlejší. V univerzálních počítačích se téměř nepoužívá, ve vestavěných systémech je často používaný.

Podle jejich instrukční sady můžeme mikrokontroléry dělit na:
- __CISC__ (Complex Instruction Set Computer) - Velké množství i velmi specializovaných instrukcí. Instrukce mohou mít různou délku i dobu trvání. Vyznačuje se instrukcemi pro různé operace s pamětí.
- __RISC__ (Reduced Instruction Set Computer) - Menší množství instrukcí. Instrukce mají jednotnou délku a trvání. Pro práci s pamětí pouze `LOAD` a `STORE`.

Mikrokontrolér se obvykle skládá z:
- Procesoru
- Operační paměti - RAM
- Paměti programu - EEPROM, FLASH, ...
- Oscilátoru - Zdroj hodinového signálu
- Vstupně výstuních rozhraních (GPIO - General Purpose Input Output)

Mikrokontrolér má obvykle řadu periferií jako například:
- Hodiny - Přesnější zdroj hodinového signálu.
- Časovač - Měření času.
- Čítač
- __Watchdog__ - Komponenta, která se stará o to, aby nedošlo k zaseknutí MCU při chybě. Pokud mu nepřijde pravidelné upozornění, tak resetuje celý MCU.
- FPGA - Programovatelné hradlové pole.
- Řadič přerušení
- Různé senzory

![Mikropočítač](/Images/05/mikropocitac.png)

## Sériová komunikační rozhraní
Sériová komunikační rozhraní slouží pro komunikaci s MCU. Komunikace probíhá po jednotlivých bitech po jednom vodiči __sekvenčně__. Je třeba jednoznačně určit, v kterém okamžiku je na datovém vodiči hodnota kterého bitu. Existují dva způsoby sériového přenosu:
- __Synchronní přenos__ - Spolu s daty je přenášen i hodinový signál, který určuje kdy lze číst další bit. Vyžaduje vodič navíc pro hodinový signál.
- __Asynchronní přenos__ - Hodinový signál není přenášen. Přijímač i vysílač si sami musí generovat hodinový signál (musí mít smluvený __baud rate__). Je nutné zajistit dostatečnou přesnost hodinového signálu a jeho synchronizaci.

### UART
_Asynchronní_ komunikační rozhraní (nepřenáší se hodinoví signál). Komunikace probíhá následovně:
1. Vysílač vysílá klidovou hodnotu log. 1.
2. Pro začátek komunikace slouží přechod do log. 0 - __start bit__.
3. Dále se posílají datové bity.
4. Za poslední datovým bitem (případně _paritním bitem_) se vyšle alespoň jeden (nebo dva) __stop bit__, který má hodnotu klidového stavu.

![UART spojení](/Images/05/uart.png)
![UART přenos](/Images/05/uart_prenos.png)

Komunikace UART je většinou _full-duplex_ (obousměrná komunikace naráz oběma směry), může být ale i _half-duplex_ (obousměrná komunikace naráz pouze jedním směrem) nebo pouze _simplex_ (jednosměrná komunikace).

### SPI
_Synchronní_ komunikační rozhraní (přenáší se hodinový signál). Jedná se o rozhraní typu __Master-Slave__, které umožňuje _full-duplex_ komunikaci. Rozlišují se zařízení:
- __Master__ - Na SPI sběrnici je vždy jediný. Je _zdrojem_ hodinového signálu, _inciuje_ a _řídí_ celou komunikaci.
- __Slave__ - Na SPI sběrnici jich může být více. Master určuje, se kterým se v daný okamžik komunikuje.

Mezi zařízení jsou následující vodiče:
- MOSI (Master Out Slave In) - Datový vodič z Master do Slave.
- MISO (Master In Slave Out) - Datový vodič z Slave do Master.
- SPSCK (SPI Serial Clock) - Vodič s hodinovým signálem.
- SS_x (Slave Select) - Povolovací vstup. Na tomto vodiči Master určuje s jakým Slave zrovna komunikuje. Je neaktivní v log. 1, v log. 0 je _aktivní_. Signál musí být v log. 0 po celou dobu komunikace.

![SPI spojení](/Images/05/spi.png)

### IIC
_Synchronní_ komunikační rozhraní, které umožňuje _half-duplex_ komunikaci. Funguje na principu __Master-Slave__. Mezi zařízeními jsou dva vodiče:
- SDA (datový signál)
- SCL (hodinový signál).

Oba vodiče jsou zapojeny přes _pull-up rezistory_ k zdroji elektrického napětí. V klidovém stavu je tak SDA v log. 1. Přenos probíhá následovně:
1. __Start condition__ - Komunikaci zahajuje Master změnou úrovně SDA \(1 \to 0\) při SCL v log. 1.
2. __Komunikace__ - Data jsou vzorkována z vodiče SDA s _náběžnou_ hranou na vodiči SCL. Změna úrovně na SDA musí být tedy prováděna, když je SCL v log. 0.
3. __Stop condition__ - Master na vodiči SDA změní úroveň \(0 \to 1\) při SCL v log. 1.

Standardně se data přenáší v datových rámcí o velikosti jednoho byte užitečných dat. Každý rámec je zakončen s ACK (potvrzení Slave, že data obdržel). Na SDA je možné provádět i adresaci připojených zařízení. Výběr Slave probíhá v odeslání prvního rámce (__adresový rámec__), kde prvních sedm bitů označuje adresu Slave a osmý bit určuje, zda půjde o čtení nebo zápis.

![I2C spojení](/Images/05/i2c.png)
![I2C přenos](/Images/05/i2c_prenos.png)

## Převodníky
Převodníky umožňují komunikaci digitálního počítače s vnějším světem, který je typicky analogový. Využívají se většinou k získávání informací z různých senzorů, které převádí měřené veličiny na napětí a toto napětí se pomocí __AD převodníků__ převádí na binární hodnoty. U __DA převodníku__ pak procesor může pomocí binární hodnoty vysílat potřebné napětí na výstup (např.: nastavení teploty).

### AD převodník
AD převodník (Analog-to-Digital converter) převádí __analogový__ (spojitý) signál na __digitální__ (diskrétní) hodnotu. Naměřené hodnoty MCU dostává v rozsahu \(0 - 2^{N-1}\) a musí je převést na odpovídající hodnotu napětí. Existuje více druhů AD převodníků, dva základní jsou následující:

#### Flash ADC
Flash ADC je __kombinační obvod__, který převádí napětí paralelně s konstatní rychlostí. \(N\) bitový převodník je tvořen \(2^{N} - 1\) komparátory, které jsou připojeny k _napěťovému žebříku_, který dělí __referenční napětí__, a k měřenému napětí. Výsledky komparátorů jsou připojeny k prioritnímu kodéru, na jehož výstupu je výsledek převodu.

Výhodou Flash ADC je jeho rychlost (převod probíhá v \(\pm\) reálném čase). Nevýhodou je vyšší cena a poměrně složitá realizace (vyžaduje přesné odpory).

![Flash ADC](/Images/05/flash_adc.png)

#### Aproximační ADC
Aproximační ADC je __sekvenční obvod__. Měřené napětí musí být nejdříve __navzorkováno__ a až poté probíhá převod. Funguje na principu binárního vyhledávání (_půlení intervalů_) správné hodnoty napětí, pracuje ale s lineární časovou složitostí \(O(N)\), kde \(N\) je počet převáděných bitů. Je tvořen částmi:
- _Sample and hodl obvod_ - Navzorkuje napětí na začátku převodu a poté jej drží beze změny až do jeho konce.
- _DA převodník_ - Převádí aktuální odhad napětí z binární hodnoty na napětí.
- _Komparátor napětí_ - Porovnává odhad napětí naměřeného napětí s měřeným napětím.
- _SAR_ - Registr, který obsahuje aktuální odhad naměřeného napětí v binární podobě. Na začátku je tato hodnota rovna polovině rozsahu.

Převod probíhá tak, že MSB v SAR je nastaven na jedna a zbylé bity jsou vynulovány. Tato binární hodnota je převedena na napětí pomocí DAC a komparátorem porovnána s měřeným napětím. Pokud je odhad menší než měřené napětí, zůstane MSB v SAR v log. 1 (odhad je příliš malý a tak musí mít větší hodnotu), jinak je změněn na log. 0. V obou případech je nastaven další MSB na log. 1 a proces se opakuje. Při porovnání se mění tento bit a na log. 1 se nastavuje bit další.

![Aproximační ADC](/Images/05/aproximacni_dac.png)
![AD převodník](/Images/05/ad_prevod.png)

### DA převodník
DA převodník (Digital-to-Analog converter) převádí __digitální__ signál na __analogový__ signál. Většina DAC je tvořena __odporovým žebříkem__.

![DA převodník](/Images/05/da_prevodnik.png)

#### Dělič napětí
![Dělič napětí](/Images/05/delic_napeti.png)

\[
    U_1 = U \frac{R_1}{R_1 + R_2} \\
    U_2 = U \frac{R_2}{R_1 + R_2}    
\]
