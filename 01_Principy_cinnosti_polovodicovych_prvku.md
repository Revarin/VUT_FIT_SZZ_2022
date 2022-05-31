# Principy činnost polovodičových prvků
- Otázky: polovodiče, PN přechod, dioda a její Volt-Ampérova charakteristika, tranzistor, bipolární tranzistor, unipolární tranzistor ve spínacím režimu, realizace logických členů NAND a NOR v technologii CMOS
- Předmět: IEL
- Zdroje:
    - http://www.fit.vutbr.cz/~peringer/UNOFFICIAL/IEL/IEL-polovodice.pdf (polovodiče a diody)
    - https://wis.fit.vutbr.cz/FIT/st/cwk.php.cs?title=Main_Page&src=2020iel8.pdf&ns=IEL&action=download&csid=681121&id=12741 (bipolární ranzistory)
    - https://wis.fit.vutbr.cz/FIT/st/cwk.php.cs?title=Main_Page&src=2020iel_10.pdf&ns=IEL&action=download&csid=681121&id=12741 (unipolární tranzistory)

## Polovodiče
Polovodiče jsou vyrobeny z prvků ze IV. skupiny periodické soustavy. Pro tyto prvky je charakteristické, že jejich atomy obsahují ve valenční vrstvě čtyři elektrony, kterými vytvářejí se sousedními atomy krystalickou vazbu.

Polovodičové součástky jsou nejčastěji postaveny na křemíku (Si). Krystalová mřížka z čistého křemíku nemá příliš významné elektrické vlastnosti. Ty mohou být výrazně pozměněny zanesením příměsy do krystalové mřížky - _doping_. Existují dva druhy dopingu podle použitého prvku:
- __Pětimocný prvek__ - Do mřížky se přidá prvek s pěti valenčními elektrony (např.: fosfor \(P_5\)). Tomuto prvku se říká __donor__. Přebytečný elektron zůstává volný a umožňuje materiálem vést elektrický proud. Jde o _elektronovou vodivost_ a vznikají tak polovodiče __typu N__.
- __Třímocný prvek__ - Do mřížky se přidá prvek s třemi valenčními elektrony (např.: bor \(B_3\)). Tomuto prvku se říká __akceptor__. Na místě chybějícího elektronu vzniká "díra", která umožňuje materiálem vést elektrický proud. Jde o _děrovou vodivost_ a vznikají tak polovodiče __typu P__.

Převažující nosič elektrického proudu (elektrického náboje) v materiálu se nazývá __majoritní__ nosič proudu. Menšinový nosič elektrického proudu se nazývá __minoritní__ nosič proudu.

### PN přechod
PN přechod je rozmezí polovodičů typu P a N. Při jejich spojení nastává _difuze_. Část volných elektronů se přesune z části N do P a část volných děr se přesune z P do N. Procesem _rekombinace_ tak vznikne pásmo, ve kterém nejsou žádné volné nosiče náboje - __potenciálová beriéra__.

## Dioda
Dioda je polovodičová součástka tvořena jedním PN přechodem. Dioda umožňuje propouštět proud pouze jedním směrem. Podle způsobu připojení ke zdroji elektrického pole můžeme teda řídit proud:
- __Propustný směr__ - dioda je ke zdroji připojena shodnými póly, potenciálová bariéra je překonána, proud protéká.
- __Závěrný směr__ - dioda je ke zdroji připojena opačnými póly, potenciálová bariéra se zvětší, proud neprotéká.

![Schématický symbol diody](/Images/01/dioda.png)

Schématický symbol:
- _Anoda_ - typ P - kladný náboj - šipka
- _Katoda_ - typ N - záporný náboj - čára
- Šipka znázorňuje směr proudu v propustném směru

Pro překonání potenciálové bariéry je potřeba alespoň minimální napětí 0,6 - 0,7 V. Při napojení diody v závěrném směru na zdroj příliš velkého napětí může nastat průraz a diodou začne procházet elektrický proud. Volt-Ampérova charakteristika reálné diody je následující:

![Volt-Ampérova charakteristika diody](/Images/01/volt-amper_diody.png)

Diody mohou mít různé funkce: usměrňovací, detekční a spínací, stabilizační (Zenerovy diody), luminiscenční (svítivé LED) a fotodiody.

## Tranzistor
Tranzistor je polovodičová součáska tvořena dvěma PN přechody (skládá se tak ze tří vrstev). Je to základním stavebním prvkem všech dnešních integrovaných obvodů. Tranzistor má dvě hlavní funkce: _spínač_ a _zesilovač_. Tranzistory se dělí na __bipolární__ a __unipolární__.

### Bipolární tranzistor
Bipolární tranzistor využívá obou nosičů náboje přítomných v polovodičích. Ovládá se otevřením PN přechodu báze-emitor, kdy bází musí protékat proud. Existují dva druhy bipolárních tranzistorů: __NPN__ a __PNP__.

Bipolární tranzistor má 3 vodiče:
- __Báze__ B - Řídící vodič.
- __Emitor__ E - Výstupní vodič (šipka).
- __Kolektor__ C - Vstupní vodič.

![Schématický symbol bipolárního tranzistoru](/Images/01/bipolarni_tranzistor.png)
![Obecný tranzistor](/Images/01/tranzistor.png)

Podle toho, zda je na bázi přiveden proud je možné ovládat, zda prochází proud mezi kolektorem a emitorem. NPN tranzistor je aktivní, když je do báze přiveden proud (log. 1); PNP tranzistor je aktivní, když je z báze vyveden proud (log. 0). Volt-Ampérova charakteristika tranzistoru je následující:

![Volt-Ampérova charakteristika tranzistoru](/Images/01/volt-amper_tranzistoru.png)
![Praktické zapojení IO obvodu s tranzistorem](/Images/01/zapojeni_tranzistoru.png)

![Spínací režim tranzistoru](/Images/01/spinaci_tranzistor.png)

#### Princip tranzistoru NPN
Těsná vzdálenost obou PN přechodů způsobí při připojení napětí na bází zvláštní stav, který blízce souvisí s majoritními a minoritními nosiči elektrického náboje. Část majoritních nosičů v emitoru při snížení potenciálnové bariéry vytváří __bázový proud__ \(I_B\). Další majoritní nosiče z emitoru pokračuje přes bázi do kolektoru a tím vytvářet __kolektorový proud__ \(I_C\). To je dáno tím, že přechod báze-kolektor je klasicky nepropustný pro majoritní nosiče, je však nepřímo propustný pro minoritní nosiče. Elektrony z emitoru (kde jsou majoritní) se v bázi stávají minoritní nosiči, pro které je přechod báze-kolektor propustný.

\[I_E = I_C + I_B\]

![Princip tranzistoru](/Images/01/princip_tranzistoru.png)

### Unipolární tranzistory
Unipolární tranzistory využívají pouze jeden typ nosičů náboje přítomných na polovodičích. Jsou založeny na principu řízení pohybu nosičů náboje _elektrickým polem_ FET (Field Effect Tranzistor). Na rozdíl od bipolárních tranzistorů tak nejsou řízeny proudem (levnější) a mají velký vstupní odpor (výhoda). Výstupní výkon unipolárních tranzistorů lze řídit elektrickým nábojem přivedeným na řídící elektrodu:

Unipolární tranzistor má 3 elektrody:
- __Gate__ G - Řídící elektroda.
- __Source__ S - Zdrojová elektroda.
- __Drain__ D - Výstupní elektroda.

![Schématický symbol unipolárního tranzistoru](/Images/01/unipolarni_tranzistor_znacka.png)

Existuje několik druhů tranzistorů, zde se zaměříem pouze na tranzistory __CMOS__ (Complementary MOS (Metal-Oxide Semiconductor)). CMOS technologie je velmi používaná díky její úspornosti (malý odběr). Funkce CMOS tranzistoru pracuje na základě logických úrovní:

![Logické úrovně CMOS](/Images/01/log_urovne_cmos.png)

#### CMOS typu N
Na elektrodu drain je připojeno vyšší napětí než na elektrodu source. Napětí mezi gate a source řídí činnost tranzistoru. Přivedením _kladného_ napětí na gate dojde k sepnutí tranzistoru. Tranzistory CMOS typu N jsou levnější než typu P.

![CMOS typu N](/Images/01/cmos_n.png)

#### CMOS typu P
Funguje podobně jako u tranzistoru CMOS typu N, jen je elektroda source připojená na vyšší napětí než drain. Přivedením _záporného napětí_ na gate dojde k sepnutí tranzistoru. Tranzistory CMOS typu P jsou pomalejší oproti typu N.

![CMOS typu P](/Images/01/cmos_p.png)

### Logická hradla v CMOS
[Vytváření logických hradel CMOS tranzistorů](https://www.youtube.com/watch?v=JXxxdRiKAlk&list=PLAlfkFSsPLoVjtryLRPnt0nZJlYkmeudA&index=2&t=1776s)

### NAND v technologii CMOS

![NAND v technologii CMOS](/Images/01/nand_cmos.png)
![Tabulka logických hodnot](/Images/01/nand_tabulka.png)

### NOR v technologii CMOS

![NOR v technologii CMOS](/Images/01/nor_cmos.png)
![Tabulka logických hodnot](/Images/01/nor_tabulka.png)
