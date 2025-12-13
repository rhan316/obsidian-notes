Reguła ACID - czyli jak nie spieprzyć danych.

ACID to 4 zasady, które MUSI spełniać transakcja w bazie danych. Spring ich nie wymyśla, tylko ładnie opakowuje przez adnotację `@Transactional` (AOP).

### A - Atomicity (Atomowość) 

✍ *Albo wszystko, albo gówno*

Transakcja: **wykonuje się w całości albo cofa się w całości**.
Nie ma "prawie się udało" albo "na 98% transakcji się powiodło - NIE MA CZEGOŚ TAKIEGO!"
0% lub 100% i tyle.
```java
@Transactional
public void tranfer() {
	withdraw();
	deposit();
}
```
Jeśli `deposit()` wybuchnie:
- `withdraw()` też zostanie anulowane
- pieniądze nie znikają w eterze

Spring robi: `commit` gdy OK, `rollback` gdy RuntimeException itd...

### C - Consistency (Spójność)

✍ *Dane po transakcji mają sens. Koniec.*

Po transakcji:
- spełnione są contrainty
- nie łamiesz reguł biznesowych
- baza nie płacze

💢Nie może być:
- saldo = -99999999
- user bez emaila, jeśli email jest `NOT NULL`

Spring nie pilnuje logiki za ciebie ale nie zapisze nielegalnego stanu, jeśli DB ma constrainty.


### I - Isolation (Izolacja)

✍ *Rób swoje, nie wtrącaj się w cudze transakcje*.

Kilka transakcji naraz nie widzą się nawzajem, chyba że sam do tego dopuścisz.
```java
Spring:
@Transaction(isolation = Isolation.READ_COMMITTED)
```
Najczęstsze poziomy:
- `READ_COMMITTED` - standard, nie widzisz brudnych danych
- `REPEATABLE_READ` - to samo zapytanie = ten sam wynik
- `SERIALIZABLE` - beton, wolne, bezpieczne

➡Im wyższa izolacja:
- tym mniej bugów
- tym mniej blokad
- tym większa szansa, że DBA cię znienawidzi.

### D - Durability (Trwałość)

✍ *Jak commit poszedł - to choćby serwer spłonął.*

Po `commit`:
- dane są stale zapisane
- restart, crash, dramat -> dane zostają
To już robota:
- silnika bazy
- logów transakcyjnych
- dysku
Spring:
- ufa bazie
- i słusznie, bo sam by tego nie ogarnął

![[Pasted image 20251213101857.png]]

