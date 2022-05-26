# Spektrální analýza spojitých a diskrétních signálů
- Otázky:
- Předmět: ISS
- ToDo: Překontrolovat a případně dovysvětlit, příklady
- Zdroje:
    - https://www.fit.vutbr.cz/study/courses/ISS/public/NEW_PRED/02_spectrum/spectrum.pdf

## Signály
Signál je libovolná fyzikální veličina, která je obvykle závislá v čase. Tento čas může být buď __spojitý__ \((t)\) (čas je definován všude) nebo __diskrétní__ \([n]\) (čas je definován pouze celočíselnými hodnotami). Diskrétní signál se dále může dělit podle způsobu reprezentace hodnoty:
- _Vzorkovaný diskrétní signál_ - Hodnota signálu se mění pouze v izolovaných okamžicích.
- _Kvantovaný diskrétní signál_ - Signál může v libovolném okamžiku nabývat pouze jednu z konečného počtu hodnot.
- _Digitální diskrétní signál_ - Kombinace vzorkovaného a kvantovaného signálu.

![Vzorkovaný diskrétní signál](/Images/14/vzorkovany_diskretni_signal.png)
![Kvantovaný diskrétní signál](/Images/14/kvantovany_diskretni_signal.png)
![Digitální diskrétní signál](/Images/14/digitalni_diskretni_signal.png)

Signály mohou být různých druhů:
- __Deterministické signály__ - Deterministické signály je možné definovat vztahem rovnicí. Pro každý čas \((t)\) nebo \([n]\) víme jaké hodnoty signál nabývá.
- __Náhodné signály__ - Náhodné signály není možné popsat rovnicí. Pro čas libovolný \((t)\) nebo \([n]\) nemůžeme přesně říct jakou hodnotu bude mít signál. Popisují se pomocí parametrů jako je střední hodnota nebo rozptyl.
- __Periodické signály__ - Periodické signály jsou signály, které se v čase opakují s periodou \(T\)/\(N\). Platí u nich rovnice \(s(t+T) = s(t)\).
- __Harmonické signály__ - Harmonické signály jsou nejjednodušeji definované periodické signály. Jsou definovány funkcemi \(\sin\), \(\cos\) apod.
    - Pro spojitý čas: \(s(t) = C_1 \cos(\omega_1 t + \phi_1)\)
    - Pro diskrétní čas: \(s[n] = C_1 \cos(\omega_1 n + \phi_1)\)

\[
    C_1\;\text{... amplituda} \\
    \omega_1\;\text{... úhlový nebo kruhový kmitočet} \\
    \phi_1\;\text{... počáteční fáze}    
\]

## Spektrální analýza
Reálné signály nejsou většinou jednoduché sinusovky, ale jedná se o kombinaci několika sinusovek. Spojením těchto sinusovek vzniká výsledný signál. Studium komponent daného signálu je předmětem spektrální analýzy.

> Podstatou spektrální analýzy je zjistit nakolik jsou dané frekvence zastoupeny v analyzovaném signálu. Provádí se tedy rozklad zkoumaného signálu na jednotlivé sinusovky a cosinusovky.
>
> Místo sinusovek se ve spektrální analýze používá __komplexní exponenciála__ (komplexním číslem jsme schopni zapsat jak amplitudu, tak fázi),

Spektrální analýza slouží tedy pro převod signálu z _časové oblasti_ do _frekvenční oblasti_. Výsledkem spektrální analýzy je __spektrum__. Spektrum je zobrazení poloh a hodnot koeficientů __Fourierovy řady__. Koeficienty Fourierovy řady jsou komplexní čísla a tudíž se dělají dva grafy: jeden pro _modul_ a druhý pro _argument_ komplexního čísla. Osa \(x\) spektra představuje frekvenci \(\omega\), osa \(y\) představuje absolutní hodnotu koeficientu pro _graf modulu_ a argument koeficientu pro _graf argumentu_. Výsledné spektrum je dále možné použít pro manipulaci se signálem a posouvání v čase.

### Komplexní exponenciála
Komplexní exponenciála je způsob zápisu _komplexního čísla_. Komplexní číslo lze zapsat exponenciálně pomocí jeho absolutní hodnoty \(r\) (modul) a fáze \(\phi\) (argument). Výsledný zápis komplexního čísla pak je \(z = r \times e^{j \phi}\).

![Grafický význam exponenciálního zápisu komplexního čísla](/Images/14/exponencialni_zapis_komplexniho_cisla.png)

Nejjednodušší komplexní exponenciála je \(y = e^{jx}\). Při dosazení \(x\) dostaneme komplexní čísla, které leží na jednotkové kružnici. Při vytvoření grafu hodnot _reálné_ a _imaginární_ složky komplexního čísla pro různé hodnoty \(x\) dostaneme spirálu.

![Komplexní spirála](/Images/14/komplexni_spirala.png)

Z různých pohledů na tuto spirálu lze vidět funkce \(\sin(x)\) a \(\cos(x)\). To je proto, že platí \(e^{jx} = \cos(x) + j \sin(x)\). Z tohoto vztahu vychází:

\[
    \cos(x) = \frac{e^{jx} + e^{-jx}}{2}
\]

Pokud budeme chtít, aby se exponenciála točila rychleji nebo pomaleji, vynásobíme exponent nějakým čísme \(e^{j \omega x}\). Pokud budeme chtít exponenciálu širší nebo užší, vynásobíme ji celou nějakým číslem \(C e^{j \omega x}\). Pokud ji budeme chtít posunout doprava/doleva, tak přičteme číslo k exponentu \(C e^{j(\omega x + \phi)} = C e^{j \phi} e^{j \omega x}\).

### Rozdělení Fourierových řad a transformací
|Operace|Vstup (signál)|Výstup (spektrum)|
|-|-|-|
|__Fourierova řada__ (FŘ)|Periodický signál se spojitým časem|Koeficienty|
|__Fourierova transformace__ (FT)|Signál se spojitým časem|Funkce definovaná pro všechny frekvence|
|__Fourierova transformace s diskrétním časem__ (DTFT)|Diskrétní signál|Periodická funkce definovaná všude|
|__Diskrétní Fourierova řada__ (DFŘ)|Periodický diskrétní signál|Periodické koeficienty|
|__Diskrétní Fourierova transformace__ (DFT)|N vzorků diskrétního signálu|N vzorků spektra|

### Spektrální analýza spojitého signálu
Pro získání spektra ze spojitého signálu se využívá těchto transformací:
- __Fourierova řada__ (FŘ) - Periodický signál se spojitým časem \(x(t)\) s periodou \(T_1\) lze rozložit na součet komplexních exponenciál. Jejich frekvence jsou násobky základní frekvence toho signálu \(k \omega_1\) a každá je vynásobená nějakým koeficientem \(c_k\), který danou exponenciálu posunuje nebo mění.
    - _Input_: periodický signál se spojitým časem
    - _Output_: koeficienty, které určují amplitudy a fáze komplexních exponenciál na násobcích základní frekvence

\[
    x(t) = \sum_{k=-\infty}^{+\infty} c_k e^{jk \omega_1 t} \\\;\\
    c_k = \frac{1}{T_1} \int_{T_1} x(t) e^{-jk \omega_1 t} dt
\]

- __Fourierova transformace__ (FT) - Má na vstupu obecný signál, který nemusí být periodický a tudíž se nedá vyjádřit jen pomocí koeficientů, které stojí na násobcích základní frekvence. Spetrum tedy není čárové, ale je to _funkce_ definovaná všude. Z koeficientů \(c_k\) se tedy stane funkce \(X(j \omega)\).
    - _Input_: obecný signál se spojitým časem (i náhodný signál)
    - _Output_: funkce definovaná pro všechny frekvence - __spektrální funkce__

\[
    x(t) = \frac{1}{2 \pi} \int_{-\infty}^{\infty} X(j \omega) e^{j \omega t} d \omega \\\;\\
    X(j \omega) = \int_{-\infty}^{\infty} e^{-j \omega t} dt
\]

### Spektrální analýza diskrétního signálu
Pokud chceme signály zpracovávat v počítačích - zpracovávat číslicově - musíme spojitý signál navzorkovat a tím z něj vytvořit diskrétní signál. Vzorkovaný signál získáme vynásobením periodickým signálem (např.: sledem _Diracových impulzů_). Tak získáme opět sled Diracových impulzů, ale s mocnostmi danými hodnotami původního signálu.

![Diracův impluz](/Images/14/diracuv_impuls.png)

> __Shanonův/Lotelnikovův/Nyquistův teorém__ říká, že vzorkovací frekvence musí být alespoň dvakrát větší než frekvence vzorkovaného signálu. Jednotlivé kopie původního spektra se tak nepřekrývají a můžeme ho rekonstruovat. Pokud tento teorém nedodržíme tak dochází k k __aliasingu__ - překryvu kopií.

![Aliasing](/Images/14/aliasing.png)

Pro získání spektra z diskrétního signálu se využívá těchto transformací:
- __Fourierova transformace s diskrétním časem__ (DTFT) - Analyzuje obecný diskrétní signál a výsledné spektrum je periodické. Periodické spektrum je u diskrétních signálů proto, že diskrétní exponenciála zůstane stejná, když se k její frekvenci přičte násobek \(2 \pi\). Spektrální funkce je značena \(X(e^{j \omega})\).
    - _Input_: dikrétní signál
    - _Output_: funkce definovaná pro všechny frekvence, periodická se vzorkovací frekvencí.

\[
    x[n] = \frac{1}{2 \pi} \int_{-\pi}^{\pi} X(e^{j \omega}) e^{j \omega n} d\omega \\\;\\
    X(e^{j \omega}) = \sum_{n=-\infty}^{\infty} x[n] e^{-j \omega n}    
\]

- __Diskrétní Fourierova řada__ (DFŘ) - Analyzuje diskrétní periodický signál a výsledkem je diskrétní periodické spektrum.
    - _Input_: diskrétní signál periodický po \(N\) vzorcích
    - _Output_: koeficienty periodické po \(N\) vzorcích (jedna N-tice odpovídá jednomu násobku vzorkovací frekvence)

\[
    x[n] = \frac{1}{N} \sum_{k=0}^{N-1} X[k] e^{j \frac{2 \pi}{N} kn} \\\;\\
    X[k] = \sum_{n=0}^{N-1} x[n] e^{-j \frac{2 \pi}{N} kn}
\]

- __Diskrétní Fourierova transformace__ (DFT) - Transformace posloupnosti diskrétního signálu délky \(N\) na jinou posloupnost délky \(N\). Prakticky se jedná o transformaci jedné periody na jednu periodu v DFŘ, narozdíl od DTFT, který transformuje neomezeně dlouhý navzorkovaný signál.
    - _Input_: \(N\) vzorků diskrétního signálu
    - _Output_: \(N\) vzorků spektra, které udávají jeho hodnoty od \(0\) až po \(\frac{N}{N-1} F_s\)

\[
    x[n] = \frac{1}{N} \sum_{k=0}^{N-1} X[k] e^{j \frac{2 \pi}{N} kn} \\\;\\
    X[k] = \sum_{n=0}^{N-1} x[n] e^{-j \frac{2 \pi}{N} kn} = \sum_{n=0}^{N-1} x[n] \times [\cos(\frac{2 \pi}{N} kn) - j \sin(\frac{2 \pi}{N} kn)]    
\]

## Používané frekvence
Pří spektrální analýze se používají následující formáty _frekvence_:
- __Normální nenormovaná frekvence__ \(f [Hz]\)
- __Normální normovaná frekvence__ \(f / F_s [-]\)
- __Kruhová nenormovaná frekvence__ \(\omega = 2 \times \pi \times f [rad/s]\)
- __Kruhová normovaná frekvence__ \((2 \times \pi \times f) / F_s [rad]\)

## Příklady
Spektrální analýza různých druhů signálů. Neboli využít výše uvedené Fourierovy vzorce.
