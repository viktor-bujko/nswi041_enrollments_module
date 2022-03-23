# Modul zápisy

## Zadanie


> Modul zápisy slouží k zapisování studentů do předmětů v semestrech a k zápisu na konkrétní rozvrhové lístky předmětu v rozvrhu na daný semestr. Zápis do lístku s naplněnou kapacitou je možný do čekací listiny předmětu. Student se nemůže zapsat na předmět, který má jako prerekvizitu předmět, který ještě úspěšně neabsolvoval. Dále se nemůže zapsat na předmět, který již absolvoval, pokud nemá předmět explicitně povoleny opakované zápisy. Garanti předmětu a vyučující přiřazení k jednotlivým rozvrhovým lístkům mohou vidět seznam studentů zapsaných do předmětu i na jednotlivé rozvrhové lístky a mohou jim rozesílat zprávy. Dále mohou studenty přesouvat mezi rozvrhovými lístky. Modul umožňuje vytvářet statistické reporty o počtech studentů zapsaných do předmětů a do rozvrhových lístků v jednotlivých semestrech a o podílech učitelů na výuce.

## Use cases:



1. __Zápis na rozvrhový lístok__
   - __Popis feature:__ Študent sa zapíše na konkrétny rozvrhový lístok.
   - __Roly využívajúce feature:__ študent, učiteľ, študijné oddelenie
   - __Obmedzenia:__
    - musí byť povolený zápis (obdobie v semestri, opakovaný zápis ...)
    - musia byť splnené prerekvizity predmetu
  
1. __Odhlásenie z rozvrhového lístku__
   
   - __Popis feature:__ Študent sa odhlási z rozvrhového lístku.
   - __Roly využívajúce feature:__ študent, učiteľ, študijné oddelenie
   - __Obmedzenia:__
       - musí byť povolené odhlasovanie (obdobie v semestri, resp. špeciálna rola, ...)
       - odhlasovaný lístok / predmet musí mať študent zapísaný

1. __Zmena rozvrhového lístku__
    - __Popis feature:__ Študent změní rozvrhový lístek.
    - __Roly využívajúce feature:__ rovnaké ako v [1.](#zapis) a [2.](#odhlasenie)
    - __Obmedzenia:__
        - rovnaké ako v [1.](#zapis) a [2.](#odhlasenie)
        - rozvrhové lístky musia být na rovnaký predmet a jeho kategóriu(prednáška / cvičenie)


1. __Získanie zoznamu zapísaných študentov__
    - __Popis feature:__ Zobraziť všetkých študentov zapísaných na predmet / rozvrhový lístok.
    - __Roly využívajúce feature:__ učiteľ / garant, študijné oddelenie
    - __Obmedzenia:__
        - učiteľ daný predmet / rozvrhový lístok vyučuje


1. __Poslať správu__
    - __Popis feature:__ Poslať správu všetkým zapísaným študentom (e-mail).
    - __Roly využívajúce feature:__ učiteľ / garant, študijné oddelenie
    - __Obmedzenia__:
        - učiteľ musí vyučovať daný rozvrhový lístok / predmet


1. __Štatistický report__
    - __Popis feature:__ Vytvorí report o počtoch študentov a jednotlivých učiteľoch konkrétneho predmetu.
    - __Roly využívajúce feature:__ modul
    - __Obmedzenia:__


1. __Získanie zoznamu rozvrhových lístkov__
    - __Popis feature:__ Nájde všetky rozvrhové lístky, na ktoré sa študent môže prihlásiť
    - __Roly využívajúce feature:__ študent, učiteľ, študijné oddelenie
    - __Obmedzenia:__
        - predmet musí mať nejaké existujúce rozvrhové lístky

```plantuml
@startuml
'left to right direction
skinparam actorStyle awesome
actor "Student" as student
actor "Teacher" as teacher
actor "Study Department" as studyDep

package "Enrolment module" as EnrolmentModule {
  usecase "Enroll in ticket" as Enroll
  usecase "List student enrollments" as ListEnrollments
  usecase "List subject tickets" as ListSubjectTickets
  usecase "List students in ticket" as ListTicketStudents
  usecase "List students in subject" as ListSubjectStudents
  usecase "Move student to ticket" as MoveStudent
  usecase "Send mail to students" as SendMails
  usecase "Create report" as CreateReport
  usecase "Validate enrolment" as Validate
}
' Extentions of use-cases
Enroll <|.. Validate : extends
Enroll ..|> ListSubjectTickets : includes
MoveStudent ..|> Enroll : includes
ListSubjectStudents ..|> ListTicketStudents : includes
ListSubjectTickets <|.. ListSubjectStudents : includes


' Extentions of actors
studyDep ..|> student : includes
studyDep ..|> teacher : includes


student --> Enroll
student --> ListEnrollments
student --> ListSubjectTickets

teacher --> MoveStudent
teacher --> ListSubjectStudents
teacher --> SendMails
teacher --> ListTicketStudents
teacher --> ListSubjectTickets

studyDep --> CreateReport

@enduml
```


# TODO:
- github issue tracking (popis s template)

### adresár na analýzu požiadavok
- dokumentácia výsledku analýzy ako MD dokument
- user / system requirements ako sekcie dokumentu
- usecase diagramy ako kapitoly
- cross-referencie z kódu a ostatných častí dokumentu