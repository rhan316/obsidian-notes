
*Proces* = program, który właśnie działa.
Nie ten, który leży grzecznie na dysku.
Ten, który się odpalił i pożera zasoby.

**Program = przepis**
**Proces = gotowanie według przepisu**
**System operacyjny = kucharz gotuje**

### Co siedzi w procesie?

Taki proces nie jest pusty:
- **Kod** - to, co program ma robić.
- **Dane** - zmienne, konfiguracje, twoje błędy
- **Stos (stack)** - krótkotrwałe rzeczy, np. zmienne lokalne
- **Sterta (heap)** - wszystko, co alokujesz dynamicznie i zapomnisz zwolnić
- **Rejestry CPU** - aktualny stan wykonywania
- **PID** - numer procesu, coś jak PESEL

### Cykl życia procesu

Proces nie działa wiecznie (chyba że jest Windowsem, wtedy czasem nie umie umrzeć).
Typowy przebieg:
1. **NEW** - proces powstaje
2. **READY** - czeka w kolejce ja ty w sklepie
3. **RUNNING** - CPU go wykonuje
4. **WAITING/BLOCKED** - np. czeka na I/O, albo na to, aż przestaniesz pisać głupoty
5. **TERMINATED** - koniec, papa.

### Jak OS robi, że wiele procesów "działa jednocześnie"?

Spoiler:
Nie działa. OS tylko szybko nimi żongluje.

*CPU robi: "ty działasz... stop, następny... stop... następny...*
*tak szybko, że wydaje ci się, że wszystko leci naraz.*

Context switch jest jak ktoś przerywający ci co 5 sekund.

### Proces vs wątek

Wątki to takie "podprocesiki" działające w tym samym adresie pamięci.

**Proces** - osobne pudełko
**Wątki** - ludzie w tym samym pudełku, każdy robi coś innego, ale wszyscy pracują razem w przeciwieństwie od procesów.
![[Pasted image 20251208211613.png]]

### Jak procesy się izolują?

Tu OS robi magię:
- każdy proces ma własną przestrzeń adresową
- jeden nie powinien dotknąć pamięci drugiego
- chyba że jesteś karnelem albo malwarem

### Jak procesy ze sobą gadają?

**IPC** -> inter-process communication
Czyli jak dzieci w przedszkolu: może być pięknie albo katastrofa.

Najważniejsze formy:
- pipes
- kolejki komunikatów
- shared memory (najszybsza i najbardziej niebezpieczna)
- sygnały
- sockety - w tym TCP, UDP, tak, nawet lokalnie
Shared memory to: wszyscy mamy dostęp do jednego pokoju, aby nikt nie nasrał na dywan.

### Co OS robi, kiedy tworzysz nowy proces?

**1. Kopiuje lub przygotowuje przestrzeń adresową**

Czyli tworzą całe środowisko pamięci dla nowego procesu.
Stos, sterta, segmenty kodu, dane - jak budowanie mieszkania od zera w pół sekundy (lub mniej).

**2. Ładuje binarkę i biblioteki**

Executable, zależności, mapowanie do pamięci...
Wszystko musi być idealnie ustawione, bo inaczej BAM - segfault.

**3. Tworzy tablice deskryptorów plików**

Czyli cały zestaw "co ten proces może otworzyć, czytać, pisać".
Wąskie gardło dla bezpieczeństwa.

**4. Kopie kontekst CPU**

Rejestry, licznik programu, stos - wszystko
Jakby klonował biegnącego sprintera w locie.

**5. Ustawia uprawnienia**

UID, GID, capabillities
Jak zbrojenie procesu w policyjnym magazynie.

**6. Inicjalizuje schedulera**

Scheduler decyduje, kiedy CPU w ogóle łaskawie go wykona.
Komu dać czas, komu zabrać, któremu procesowi dać w ryj, bo za dużo żre pamięci.

**7. Podłącza sygnały, handlery, tablice systemowe**

Czy proces może być zabity? Pauzowany? Czy coś odziedziczy po rodzicu?
Cała infrastruktura.