# Webová uživatelská a aplikační rozhraní
- Otázky: správa sezení a autentizace
- Předmět: IIS
- zdroje:
  - https://www.youtube.com/watch?v=9Jub5t1allI&list=PLAlfkFSsPLoVjtryLRPnt0nZJlYkmeudA&index=34
## HTML (HyperText Markup Language)
- značkovací jazyk
- Určený pro tworbu webových stránek - obsahu
- Značky mohou být párové, nebo nepárové
    - př.
        - `<html></html> - párová` 
        - `<br> - nepárová`
    - ukončení značky (tagu) pomocí `/`
- patří pod SGML jazyky:
    - značkovací jazyky
## CCS (Cascading Style Sheets)
- jazyk pro stylizaci HTML elementů
- syntax
  ```
  selektor {
    vlastnost: hodnota;
    vlastnost2: hodnota2;
    .
    .
    .
  }
  ```
- přístup pomocí:
    - značky
    - třídy
    - id
- styly se vybírají pomocí priority selektoru:
    1. styly přímo u atributu
    2. id
    3. class 
    4. typ značky
- také rozhoduje úroveň specifikace

př.: (seřazeno podle priority)
1. .red #bigRectangle{}
2. .red.rectangle{}
3. .red{}
4. div{}

## Javascript
- skriptovací jazyk
- interpretovan, nebo kompilovaný za běhu - JIT ( just-in-time compiled )
- Pro přístup k elementům HTML dokumentu využívá DOM
- DOM - stromová struktura obsahující prvky HTML dokumentu
- umožnujě přidávat event listeners "naslouchače událostí"
    - například při kliknutí
- Intrukce jsou vykonávány po řádku - synchroně, ale podporuje i asynchroní volání
- Otázka:
  - Jak se dostane 

## API (application programming interface)
- aplikační rozhraní - způsob, jak spolu mohou komunikovat aplikace

Příklady typů API:
- REST (Representational state transfer)
  - Není protokol, ale přístup k vývoji API
  - Založen na využití HTTP protokolu
  - Definuje operace:
    - CREATE
      - POST požadavek
    - READ
      - GET požadavel
    - UPDATE
      - PUT / PATCH požadacek
    - DELETE
      - DELETE požadavek
  - Není standardizovaný
  - K serializace může využívat(není standardizováno): 
    - JSON
    - XML
    - další

- Simple Object Access protokol:
  - protokol
  - nezávyslý na internetových stránkách - nebyl vyvynut pro internetnetové stránky
  - posílání zpráv
    - zpráva zabalena do obálky, obsahuje hlavičku
  - serializace dat pomocí XML
  - výhody:
    - standardizovaný protokol
  - nevýhody:
    - XML - hodně nadbytečných znaků?

- GraphQL
  - Není protokol
  - Silně typovaný jazyk pro tvorbu dotazů
  - Definuje syntax
  - Dotazujeme se na konkrétní data
  - Není závyslý na protokolu HTTP
  - Serializace dat:
    - JSON
  - Výhody:
    - Server zasílá pouze data, o které si klient zažádá

## Sezení (Session)
- Protokol HTTP je bezstavový => pro aplikace si potřebujeme pamatovat kontext
  - např.: 
    - uživatel je přihlášený
    - uživatel si nastavil tmavý režim - posíláme jiné css soubory...
    - atd.

**Správa sezení:**
- uživtateli se přiřadí unikátní identifikátor = Session ID
  - uloží se do COOCKIES
  - Coockies = malý objem dat, který server uloží nba straně klienta
    - klient zasílá tyto coockies serveru s každým požadavkem
- při odcizení Session ID, se může útočník vydávat za oběť
  - např. pokud jsme přihlášeni na nějaké službě, je dané přihlášení spojeno s našim Session ID
  - Pokud útočník získá moje Session ID, může ho zaslat na server a server mu poskytne plný přístup k mému účtu

## Autentizace uživatele
- pomocí formuláře 
- Jak probíhá ověření:
    - klient vyplní formulář
    - server ověří korektnost údajů ve formuláři
    - Server vygeneruje Session ID a zašle ho klientovi
    - klient pak v každém dalším dotazu zasílá Session ID
- JWT = Json Web Token
    - části:
        - header
            - informace, použité algoritmy, typ dat
        - payload
            - data
        - podpis
            - pro ověření integrity dat
    - části se spojí, zakódují pomocí Base64 a pošle se serveru
    - Jak probíhá ověření:
        - klient vyplní formulář
        - server ověří korektnost údajů ve formuláři
        - Server vygeneruje JWT a zašle ho klientovi
        - klient pak v každém dalším dotazu zasílá JWT
- OAuth
    -  příklad využití:
        - přihlášení na nšjaký web pomocí google účtu
        - DrawIO
            - potřebuje přístup na google disk
            - přihlásíme se pomocí google účtu a povolíme přístup k našemu disku
            - Google vygenerutje Access token pro přístup aplikace na náš disk
            - aplikace pak využívá tento token pro zasílání dat
