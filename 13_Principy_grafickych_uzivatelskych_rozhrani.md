# Principy grafických uživatelských rozhraní
- Otázky: komunikační kanály, módy komunikace, systémy řízené událostmi, standardní prvky rozhraní
- Předmět: ITU

## Komunikační kanály
Komunikační kanály jsou způsoby komunikace mezi člověkem a strojem. Jsou to vlastně všechna možná __periferní zařízení__ - obrazovka, klávesnice, myš, tiskárna, reproduktory... Všechny tyto zařízení jsou založené na lidských smyslech - zrak, hmat, sluch, (chuť a čich).

Komunikační kanály __od stroje k člověku__ jsou následující:
- __Obraz__ (zrak) - Obraz je nejvýhodnější médium pro přenos informace od stroje k člověku. Důvodem je zejména velmi vysoká informační propustnost a možnost _náhodného přístupu_ pozorovatele k informacím obsaženým v obraze.
- __Zvuk__ (sluch) - Zvuk je výhodný pro přenos menšího množství informací od stroje k člověku pro doplnění obrazu. Nevýhodou oproti obrazu je nižší propustnost a _sériový_ přístup k informacím.
- __Hmat__ - Hmat je dosud používaný pouze výjimečně. Je však perspektivní pro budoucí aplikace ve spojení s virtuální realitou a to ve formě hmatové a silové zpětné vazby. V současné době je využíván zejména jako prostředek pro komunikaci nevidomých se stroji.
- __Čich, chuť__ - Čich a chuť v současnosti nejsou pro komunikaci použitelné. Důvodem je především stav současné chemie a techniky, který neumožňuje uměle syntatizovat chutě a vůně v reálném čase. V budoucnosti by se mohly uplatnit jako doplněk pro virtuální realitu.

Komunikační kanály __od člověka ke stroji__ jsou následující:
- __Pohyb__ (hmat) - Nejobvyklejším prostředkem pro předání informací člověkem do strojů jsou klávesnice v nejrůznějších podobách. Ty bývají často doplňovány mechanickými polohovacími zařízeními, jako je například myš. Existují však i další zařízení podobných typů.
- __Zvuk__ (řeč) - Komunikace ve směru od člověka ke stroji zvukem (řečí) je velmi perspektivní. V některých aplikacích by mohl i nahradit klasické ovládání hmatem. Dosud však tento způsob komunikace není prakticky moc použitelný. Není dostatečně vyřešeno porozumění lidské řeči na straně strojů. Není také vhodné na některé typy informací jako jsou například hesla.
- __Obraz__ (gesta) - Úplné sdělování informace stroji pomocí gest těla i ruky případně mimiky je dosud nerealizovatelné a realizace je pravděpodobně vzdálená. Některé dílčí aplikace rozpoznávání obrazu jsou však reálné již nyní (sledování rukou, postavy, pohybu, atd.). Další příkladem může být rozpoznávání osob, strojové čtení, či automatické řízení vozidel.

## Komunikace
V praxi se oba směry komunikace kombinují (oboustranná komunikace). Pro komunikaci se používají dva principy:
- __Drag and drop__ - Manipulace s předměty jako v reálném životě (přesun souboru).
- __Look and feel__ - Komunikace s rozhraním vyplývá z prvků reálného života.

### Aktivní komunikace
Aktivní komunikace je taková komunikace, kdy uživatel řídí činnost počítače, tedy kdy činnost počítače závisí na vůli uživatele. Rozhraní používající aktivní komunikaci je například panel nástrojů nebo příkazová řádka. Uživatel sám vybírá nástroj, když se mu chce a pak následně uživatel sám určuje, jak ho bude používat.

### Pasivní komunikace
Pasivní komunikace je taková komunikace, při níž uživatel v obecném smyslu odpovídá na dotazy počítače. Pasivní komunikací se myslí stav, kdy počítač vznese dotaz a uživatel na něj odpovídá. Toho lze v GUI dosáhnout například dialogovými boxy.

|Vlastnost|Aktivní komunikace|Pasivní komunikace|
|-|-|-|
|Efektivní práce|~ dle aplikace|- často neefektivní|
|Učení|- obtížné|+ snadné|
|Tvůrčí práce|+ snadná|- otížná|
|Možnost chyby|- velká|+ malá|

### Mody komunikace
Změnou z pasivní a aktivní komunikace (a naopak) plyne nutnost přecházení z aktivního a pasivního režimu - __změny chování__ počítače na akce uživatele. Změny chování počítače lze dosáhnout pomocí tzv. __modů__. Mod je stav, ve kerém počítač reaguje jedinečným způsobem na vstupy od uživatele. Čím méně modů se při komunikaci vyskytuje, tím lépe. Existují jisté typické modey:
- Zadávání příkazů v příkazovém jazyce.
- Odpověď na dotaz počítače (uložit, smazat, zrušit).
- Editace textu.
- Reakce na chybu.

## Událostmi řízené systémy
Událostmi řízené systémy představují základní princip práce s GUI. Tok programu je řízen různými událostmi (kliknutí myši, stisknutí klávesy). V programu existuje nějaky __naslouchač__ (listener), který čeká na přijmutí události. Po jejím přijmutí provede odpovídající akci. U HW obdobně funguje systém přerušení. Všechny moderní systémy jsou řízené událostmi. Ve _Windows_ jsou například reprezentovány zprávami, které jsou zasílány specializovanými funkcemi z prvků rozhraní.

V dnešní době se používají systémy GUI postavené na prvním GUI založeném na práci s okny __WIMP__ (Windows, Icon, Menu, Pointer). WIMP systém obsahuje:
- Okna, která reprezentují spuštěné programy, z nichž je každý izolován od ostatních programů ve vlastních oknách.
- Ikony, které reprezentují zkratky sloužící k provedení určité činnosti.
- Menu, což jsou textové (nebo ikonové) nabídky, ze kterých je možné jednu vybrat a provést tak určitou akci.
- Ukazatel, což je pohybující se grafický symbol reprezentující pohyb fyzického zařízení, pomocí něhož uživatel vybírá ikony, položky v menu nebo data.

## Standardní prvky rozhraní
Standardní prvky rozhraní využívají __metafor rozhraní__. Metafora rozhraní je kolekce vizuál, akcí a postupů, které využívají specifické znalosti, které již uživatelé mají o jiných doménách. Slouží pro urychlení naučení se práce s GUI.

- Tlačítko (button)
- Popisek (label)
- Editační řádek (edit box)
- Rádiová tlačítka (radio button)
- Zaškrtávátko (check box)
- Seznam (list box)
- Seznam s řádkem (combo box)
- Slider
- Progressbar
- Výběr souboru
- ...

### Dialogový box
Dialogový box je stavebnice, která se skládá z jiných prvků rozhraní. Prvky jsou vesměs okny. Dialogové boxy se dělí na:
- __Modální__ (modal) - Prioritní v aplikaci, uživatel musí odpovědět na dialog, jinak nemůže pokračovat v práci.
- __Nemodální__ (non-modal) - Neprioritní, uživatel může pokračovat v práci a na dialog odpovědět později.
- __Systémově modální__ (system-modal) - Mají prioritu nad aplikacemi.

Modalita dialogivého boxu je implementována tím, že při zobrazení modální boxu se zabrání průchodu zpráv od uživatele do níže položených oken v hierarchii oken. Pro přehlednost se většinou zbytek aplikace zašedne. Ve příkazové řádce je ukázkou pasivní modální komunikace například dotaz `Delete file? Y/N`.
