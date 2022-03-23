# Modul zápisy

## Zadanie


> Modul zápisy slouží k zapisování studentů do předmětů v semestrech a k zápisu na konkrétní rozvrhové lístky předmětu v rozvrhu na daný semestr. Zápis do lístku s naplněnou kapacitou je možný do čekací listiny předmětu. Student se nemůže zapsat na předmět, který má jako prerekvizitu předmět, který ještě úspěšně neabsolvoval. Dále se nemůže zapsat na předmět, který již absolvoval, pokud nemá předmět explicitně povoleny opakované zápisy. Garanti předmětu a vyučující přiřazení k jednotlivým rozvrhovým lístkům mohou vidět seznam studentů zapsaných do předmětu i na jednotlivé rozvrhové lístky a mohou jim rozesílat zprávy. Dále mohou studenty přesouvat mezi rozvrhovými lístky. Modul umožňuje vytvářet statistické reporty o počtech studentů zapsaných do předmětů a do rozvrhových lístků v jednotlivých semestrech a o podílech učitelů na výuce.

## Možné / potrebné features

<ol>
<li id="zapis">Zápis na rozvrhový lístok</li>

- __Popis feature:__ Študent sa zapíše na konkrétny rozvrhový lístok.
- __Roly využívajúce feature:__ študent, učiteľ, študijné oddelenie
- __Obmedzenia:__
    - musí byť povolený zápis (obdobie v semestri, opakovaný zápis ...)
    - musia byť splnené prerekvizity predmetu

<li id="odhlasenie">Odhlásenie z rozvrhového lístku</li>

- __Popis feature:__ Študent sa odhlási z rozvrhového lístku.
- __Roly využívajúce feature:__ študent, učiteľ, študijné oddelenie
- __Obmedzenia:__
    - musí byť povolené odhlasovanie (obdobie v semestri, resp. špeciálna rola, ...)
    - odhlasovaný lístok / predmet musí mať študent zapísaný
</ol>

3. Zmena rozvrhového lístku
    - __Popis feature:__ Študent změní rozvrhový lístek.
    - __Roly využívajúce feature:__ rovnaké ako v [1.](#zapis) a [2.](#odhlasenie)
    - __Obmedzenia:__
        - rovnaké ako v [1.](#zapis) a [2.](#odhlasenie)
        - rozvrhové lístky musia být na rovnaký predmet a jeho kategóriu(prednáška / cvičenie)


4. Získanie zoznamu zapísaných študentov
    - __Popis feature:__ Zobraziť všetkých študentov zapísaných na predmet / rozvrhový lístok.
    - __Roly využívajúce feature:__ učiteľ / garant, študijné oddelenie
    - __Obmedzenia:__
        - učiteľ daný predmet / rozvrhový lístok vyučuje


5. Poslať správu
    - __Popis feature:__ Poslať správu všetkým zapísaným študentom (e-mail).
    - __Roly využívajúce feature:__ učiteľ / garant, študijné oddelenie
    - __Obmedzenia__:
        - učiteľ musí vyučovať daný rozvrhový lístok / predmet


6. Štatistický report
    - __Popis feature:__ Vytvorí report o počtoch študentov a jednotlivých učiteľoch konkrétneho predmetu.
    - __Roly využívajúce feature:__ modul
    - __Obmedzenia:__


7. Získanie zoznamu rozvrhových lístkov
    - __Popis feature:__ Nájde všetky rozvrhové lístky, na ktoré sa študent môže prihlásiť
    - __Roly využívajúce feature:__ študent, učiteľ, študijné oddelenie
    - __Obmedzenia:__
        - predmet musí mať nejaké existujúce rozvrhové lístky


# TODO:
- github issue tracking (popis s template)

### adresár na analýzu požiadavok
- dokumentácia výsledku analýzy ako MD dokument
- user / system requirements ako sekcie dokumentu
- usecase diagramy ako kapitoly
- cross-referencie z kódu a ostatných častí dokumentu