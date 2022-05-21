# Číslicové filtry
- Otázky: diferenční rovnice, impulsní odezva, přenosová funkce, frekvenční charakteristika
- Předmět: ISS
- ToDo: Příklad
- Zdroje:
    - https://www.fit.vutbr.cz/study/courses/ISS/public/NEW_PRED/01_filtry/filtry.pdf

## Signál
Signál je časově či prostorově proměnná fyzikální veličina (viz. okruh [14]). Se signálem je možné provádět různé operace - je možné signál __transformovat__:
- __Otočení časové osy__ - \(s(-t)\)
- __Zpoždění signálu__ - \(s(t-x)\)
- __Předběhnutí signálu__ - \(s(t+x)\)
- __Kontrakce signálu__ - \(s(m*t)\)
- __Dilatace signálu__ - \(s(t/m)\)

## Systém
Systém je zařízení upravující signál. Má vstupu a výstupu. Je charakterizován __impulsní odezvou__ \(h\), která značí jak systém reaguje na jednotkový impuls. Výstup systému je dán _konvolucí_ (součtem) vstupu a impulsní odezvy:
- __Konvoluční suma__

\[
    y[n] = \sum_{k=-\infty}^{+\infty} x[k] h[n-k] \\
    y[n] = x[n] \times h[n]    
\]

- __Konvoluční integrál__

\[
    y(t) = \int_{k=-\infty}^{+\infty} x(\tau) h(t - \tau) d\tau \\
    y(t) = x(t) \times h(t)
\]

![Obecné schéma systému](/Images/15/obecne_schema_systemu.png)

> Konvoluce je operace, která ze dvou funkcí vytvoří třetí funkce, která popisuje, jak je tvar jedné funkce ovlivňován funkcí druhou.

### Systémy s diskrétním časem
V systémech s diskrétním časem je signál \(y[n]\) reakcí na vstupní signál \(x[n]\). Značíme jej \(x[n] \rightarrow y[n]\). Rozklad na jednotkové impulsy musí být časově invariantní a na výstupu se provede konvoluce (proužkem papíru).

### Systémy se spojitým časem
V systémech se spojitým časem je signál \(y(t)\) reakcí na vstupní signál \(x(t)\). Značíme jej \(x(t) \rightarrow y(t)\). Při rozkladu na impulsy můžeme signál aproximovat po částech \(\Delta\) a postupně násobit, dokud se nedostaneme na příslušnou hodnotu. 

![Rozklad na impusly systému se spojitým časem](/Images/15/rozklad_na_impulsy.png)

### Vlastnosti systémů
Systémy mohou mít různé vlastnosti:
- __Paměť__
    - _Systémy s pamětí_ - Systém je schopen si pamatovat svoji předešlou hodnotu.
    - _Systémy bez paměti_ - Systém reaguje pouze na okamžitou hodnotu vstupu.
- __Kauzaliza__
    - _Kauzální systémy_ - Systém reaguje pouze na současný nebo minulý vstup (nevidí do budoucnosti). Např.: \(y[n] = x[n] - x[n-1]\)
    - _Nekauzální systémy_ - Systém může reagovat i na budoucí vstupy (vidí do budoucnosti). Např.: \(y(t) = x(-t)\)
- __Stabilita systému__ - Systém pro omezený vstup produkuje omezený výstup (má horní a dolní hranici).
- __Časová invariantnost systému__ - Systém nemění své chování v čase - na stejný vstup zareaguje stejně v jakýkoliv čas.
- __Linearita systému__ - Systém je lineární, pokud jsou splněny následující podmínky:
    - _Aditivita_ - Součet vstupů výstupu odpovídá součtu výstupů \(x_1(t) + x_2(t) \rightarrow y_1(t) + y_2(t)\)
    - _Scaling_ nebo _homogenita_ - Vynásobení konstantou na vstupu má stejný vliv na výstup \(ax_1(t) \rightarrow ay_1(t)\)
    - > Pokud při rozložení vstupních signálů na jednotlivé impulsy a poslání jich do systému zvlášť získáme jejich součtem odpovídající výstupní signál, tak potom je systém lineární.

\[
    a x_1(t) + b x_2(t) \rightarrow a y_1(t) + b y_2(t)    
\]

## Filtr
Filtr je systém, který upravuje signál ve frekvenční oblasti. Je charakteristický svou _impulsní odezvou_. Výstup filtr získáme pomocí konvoluce. Základní stavební bloky filtrů jsou: __zpožďovací článek__, __násobička__ a __sčítačka__.

![Základní bloky filtrů](/Images/15/prvky_filtru.png)

Filtry jsou lineárně a časově _invariantní_ (LTI). Jsou dva základní typy filtrů: 
- __Horní propust__ - Filtr propouští vysoké frekvence signálu.
- __Dolní propust__ - Filtr propouští nízké frekvence signálu.
- __Pásmová propust__ - Filtr propouští jen určité frekvence signálu.
- __Pásmová zádrž__ - Fitlr nepropouští jen určité frekvence signálu.

Filtry se dají implementovat pomocí __diferenčních rovnic__.

\[
    y[n] = \sum_{k=0}^Q b_k x[n-k] - \sum_{k=1}^P a_k y[n-k]    
\]

![Obecně rekurzivní filtr](/Images/15/obecny_rekurzivni_filtr.png)

### Rekurzivní filtr
Rekurzivní filtr(_Infinite impulse response_, IIR) má _nekonečnou_ impulsní odezvu. __Čistě rekurzivní__ filtr se vstupním signálem neprovádí žádné změny (koeficienty \(b jsou nulové\)). Naproti tomu __obecně rekurzivní__ filtr se vstupním signálem provádí změny (koeficienty \(b\) a \(a\) jsou nenulové).

![Čistě rekurzivní filtr](/Images/15/cisty_rekurzivni_filtr.png)

### Nerekurzivní filtr
Nerekurzivní filtr (_Finite Impulse Response_, FIR) má _konečnou_ impulsní odezvu. Na výstupu filtru je po celém průchodu vstupního signálu nula. Impulsní odezva je přímo dána koeficienty \(b\). 

![Nerekurzivní filtr](/Images/15/nerekurzivni_filtr.png)

### Impulsní odezva filtru
Filtr (systém) může být charakterizován __impulsní odezvou__ \(h\), která značí jak systém reaguje na jednotkový impuls. Pokud máme k systému zadanou jeho impulsní odezvu, dokážeme spočítat odpověď systému na jakýkoliv signál, a to tak, že vstupní signál rozložíme na jednotkové impulsy. Ty necháme projít systémem a jejich výsledky sečteme. To je možné proto, že pracujeme s lineárním a časově invariatním systémem.

![Příklad tabulky impulsní odezvy](/Images/15/tabulky_impulsni_odezvy.png)
![Impulsni odezva](/Images/15/impulsni_odezva.png)

Matematicky lze impulsní odezva zapsat jako __konvoluce__:

\[
    y[n] = \sum_{k=-\infty}^{\infty} x[k] h[n-k] \\\;\\
    y[n] = x[n] * h[n]    
\]

### Komplexní frekvenční charakteristika filtru
Se signály je často výhodné pracovat ve frekveční doméně. Proto je dobré vědět, co se stane se spektrem signálu po průchodu filtrem.

![Spektrum po průchodu filtrem](/Images/15/spektrum.png)

K tomu slouží __komplexní frekveční charakteristika filtru__ (kmitočtová charakteristika filtru) \(H(e^{j \omega})\). Získáme ji posláním komplexní exponenciály na vstup systému. To odpovídá DTFT (Fourierova transformace s diskrétním časem) impulsní odezvy. Když ji vynásobíme se spektrem vstupního signálu získáme spektrum výstupního signálu.

\[
    Y(e^{j \omega}) = X(e^{j \omega}) H(e^{j \omega})    
\]

### Přenosová funkce filtru
__Přenosová funkce__ je další způsob popsání chování filtru. Z přenosové funkce lze vyčíst, jestli je filtr stabilní a také z ní lze odhadnou _komplexní kmitočtová charakteristika filtru_. Přenosovou funkci získáme pomocí operace __z-transformace__:

\[
    X(z) = \sum_{n=-\infty}^{\infty} x[n] z^{-n} 
\]

Z-transformace je komplexní funkce nad komplexní rovinou. Pro její provedení lze využít její následující vlastnosti:
1. Konstanty zůstanou konstanty.
2. Všechna \(x[n]\) se přepíšou na \(X(z)\) a všechna \(y[n]\) na \(Y(z)\).
3. Když je někde zpoždění o \(n\), musí se vajádřit pomocí \(z^{-n}\).

\[
    a x_1[n] + b x_2[n] \rightarrow a X_1(z) + b X_2(z) \\\;\\
    x[n-k] \rightarrow z^{-k} X(z)   
\]

Ze z-transformace lze vypočítat přenosovou funkce, která je definována jako \(H(z) = Y(z) / X(z)\).

\[
    H(z) = \frac{Y(z)}{X(z)} = \frac{\sum_{k=0}^{Q} b_k z^{-k}}{1 + \sum_{k=1}^{P} a_k z^{-k}} = \frac{B(z)}{A(z)} \\\;\\
    H(z) = b_0 z^{P-Q} \frac{\prod_{k=1}^{Q} (z - n_k)}{\prod_{k=1}^{P} (z - p_k)}
\]

Čísla \(n_k\) a \(p_k\) se nazývají __nuly__ a __póly__. Jsou to komplexní čísla, která můžeme zakreslit do komplexní roviny a podle nich vyhodnotit stabilitu filtru a odhadnout komplexní kmitočtovou charakteristiku filtru. Filtr je stabilní, pokud všechny jeho póly leží uvnitř jednotkové kružnice (\(|p_k| < 1\)). Komplexní kmitočtovou charakteristiku filtru z přenosové funkce získáme tak, že za \(z\) dosadíme \(e^{j \omega}\).

\[
    H(e^{j \omega}) = H(z)|_{z=e^{j \omega}} = \frac{\sum_{k=0}^{Q} b_k e^{-j \omega k}}{1 + \sum_{k=1}^{P} a_k e^{-j \omega k}}    
\]

## Příklady
[TODO]
