*Czym jest JVM?*

JVM to maszyna wirtualna, która:
- Uruchamia kod Java (czyli pliki `.class`skompilowane do *bytecode*).
- Tłumaczy bytecode na instrukcje, które mogą być zrozumiałe przez sprzęt (procesor).
- Zarządza pamięcią, wątkami, i innymi zasobami potrzebnymi do działania aplikacji.

*Analogia*

Wyobraź sobie orkiestrę, która gra partyturę (bytecode). W tym przypadku partytura jest uniwersalna - każda orkiestra może ją zagrać, niezależnie od tego, czy gra na nowoczesnych instrumentach czy na zabytkowych.

**Główne elementy JVM**

1. ~={red}**Class Loader - dyrygent orkiestry**=~ Class Loader odpowiada za ładowanie klas do pamięci na żądanie. Kiedy uruchamiasz program, JVM nie wczytuje wszystkich klas od razu, ale robi to stopniowo, w miarę potrzeby. *Co robi Class Loader?*
	- ~={red}**Bootstrap Class Loader**=~ ładuje podstawowe klasy Javy, takie jak `java.lang.String` czy `java.util.ArrayList`.
	- ~={red}**Extension Class Loader**=~ ładuje dodatkowe klasy znajdujące się w bibliotekach (np. w folderze JDK).
	- ~={red}**Application Class Loader**=~ ładuje klasy aplikacji (te, które ty piszesz).
	Analogia -> Dyrygent nie wprowadza od razu wszystkich muzyków, ale stopniowo włącza ich do gry, w odpowiednich momentach.

2. ~={8}**Execution Engine - muzycy wykonujący symfonię**=~ To tutaj byte code jest faktycznie wykonywany. Składa się z 3 części:
	- ~={8}**Interpreter**=~ Odczytuje bytecode linia po lini i tłumaczy go na język maszyny - szybki w uruchomieniu, ale wolniejszy w dłuższej perspektywie.
	- ~={8}**Just-In-Time Compiler (JIT)**=~ Tłumaczy bytecode na natywny kod maszynowy, aby działał szybciej. Raz skompilowany kod nie musi być już interpretowany.
	-~={8} **Garbage Collector**=~ Zarządza pamięcią, usuwając obiekty, które nie są już potrzebne.
	Analogia -> Interpreter to muzyk, który odczytuje nuty i gra je na bieżąco - nie zawsze idealnie. JIT Compiler to muzyk, który ćwiczył wcześniej i teraz gra płynnie i szybciej. Garbage Collector to członek zespołu sprzątającego - usuwa potrzebne przedmioty z estrady, aby muzycy mieli miejsce do pracy.

3. ~={green}**Memeory Management - sala koncertowa**=~ JVM zarządza pamięcią w podziale na kilka sekcji, które nazywamy *pamięcią stertową (heap)* i *stosowaą (stack)*:
	- ~={green}**Heap (Sterta)**=~: Tutaj przechowywane są obiekty i dane dynamiczne. Przykład: Tworzysz nowy obiekt klasy `Person`, jego instancja trafia do sterty.
	- ~={green}**Stack (Stos)**=~: Tutaj przechowywane są zmienne lokalne i informacje potrzebne do śledzenia wywołań metod, referencje do obiektów.
	- ~={green}**Metaspace**=~ Przechowuje dane o klasach i metadanych. W Javie 8 zastąpił to wcześniejszy "PermGen".
	Analogia: Sala koncertowa (heap) to miejsce, gdzie trzymane są wszystkie instrumenty. Stół dla dyrygenta (stack) to miejsce, gdzie ma pod ręką nuty potrzebne do bieżącego utworu. Metaspace to magazyn, gdzie przechowywane są informacje o utworach i instrumentach.

**Garbage Collector (GC) - osoba sprzątająca salę**
Garbage collector to proces, który usuwa obiekty, które nie są już używane, aby zwolnić pamięć dla nowych obiektów. Istnieje kilka strategii działania GC:
- *Serial GC* - Prosta, jednowątkowa wersja - dla aplikacji z małym obciążeniem.
- *Parallel GC* - korzysta z wielu wątków, aby jednocześnie zarządzać pamięcią.
- *G1 GC (Garbage-First)* - Najnowszy GC w Javie - dzieli stertę na mniejsze części i usuwa śmieci z najbardziej "zaśmieconych obszarów".
Analogia: GC to ktoś, to sprząta w czasie rzeczywistym. Czasem działa spokojnie (Serial GC), a czasem w grupie (Parallel GC), aby szybciej posprzątać bałagan.

**Opcje konfiguracyjne JVM**
`-Xms` i `-Xmx` - ustalają minimalny i maksymalny rozmiar sterty.
`-XX:+UseG1GC` - wybór konkretnego Garbage Collector.
`-Xss` - ustala wielkość stosu dla jednego wątku.

### 1. Class Loader Subsystem
*czyli kto w ogóle ładuje twoje pieprzone klasy*

JVM ma 3 główne loadery:
- ##### Bootstrap ClassLoader - Ładuje rt.jar / moduły JDK, rzeczy najbardziej fudamentalne.
- ##### Platform ClassLoader - ładuje rzeczy z `java.*, jdk.*`
- ##### Application ClassLoader - ładuje twoje klasy, JAR-y, moduły aplikacji.

I możesz jeszcze dorzucać *custom class loadery*, jak zwyczajny sadysta.
JVM buduje z tego hierarchię delegacji - najpierw pyta wyżej, potem niżej.

### 2. Runtime Data Areas
czyli pamięć JVM - tu zaczyna się zabawa

JVM dzieli pamięć na kilka obszarów, każdy z innym przeznaczeniem.

#### Heap
- miejsce na obiekty
- podzielone na ***Young Gen*** (Eden + Survivor) i ***Old Gen***
- zarządzane przez GC (garbage collector)
- to, co wkurwia programistów najbardziej

#### Stack
- jeden stack *per thread*
- trzyma ramki wywołań, zmienne lokalne, referencje
- tu dzieją się wszystkie NPE tragedie

#### PC Register
- wskaźnik na aktualną instrukcję Java Bytecode
- każdy thread ma swoje

#### Native Method Stack
- dla metod `native`, C++ itd.

#### Metaspace
- successor PermGen
- trzyma metadane klas, metody, constant pool
- rośnie dynamicznie, nie ma stałego limitu jak stare PermGen

### Execution Engine
czyli sam mózg JVM - to, co tak naprawdę odpala kod.

Składa się z kilku potworów, każdy do czegoś ważnego.

#### Interpreter
- wykonuje bytecode linijka po linijce
- szybki start, wolna praca
- działa do momentu, aż JIT stwierdzi: "ten kod żyje wystarczająco długo"

#### JIT Compiler (C1 i C2 / GraalVM)
Tu jest magia.

- ***C1 (Client Compiler)*** -> szybki, lekki, kompiluje częściej
- ***C2 (Server Compiler)*** -> cięższa optymalizacja, robi cuda na poziomie kodu
- ***Graal JIT*** -> nowoczesny, agresywnie optymalizujący kompilator (w JVM od JDK 17+ jako opcja)
JIT kompiluje hot spoty z bytecode -> do natywnego kodu maszynowego.
Czyli JVM to hybryda:
- najpierw interpreter
- potem JIT
- potem natywny kod
- potem optymalizacje w locie

### Garbage Collector
czyli śmieciarz twoich błędów.

Nowoczesny JVM ma kilka GC, wybierasz w zależności od potrzeb:

**G1 GC** -> domyślny. Low-pause. Dzieli heap na regiony.
**ZGC** -> ultra-low pause, duże systemy, heap 100GB+
**Shenandoah** -> OpenJDK + RedHat, niski pause time, współbieżny marking
**Parallel GC** -> Stary, szybki throughput, ale długi stop-the-world
**Serial GC** -> dla systemów z małą pamięcią. Dinozaur

### Native Interface (JNI / Panama)
Pozwala JVM gadać z natywnym C/C++/Rust.
JNI jest koszmarem, więc robią nowy Projekt Panama, który ma to naprawić.

### Bytecode Verifier
Sprawdza, czy bytecode:
- nie łamie bezpieczeństwa
- nie psuje typów
- nie robi stack underflow/overflow
- nie manipuluje wskaźnikami
- nie zachowuje się jak ty po 3 piwach
Bez tego JVM by się rozpadał.

### JFR + JIT Profiling
Nowoczesny JVM sam monitoruje, które metody są:
- najczęściej wykonane
- najcięższe
- warte kompilacji
- do zoptymalizowania
- do de-optymalizacji
To dlatego JVM "uczy się w locie"

### Moduły (JPMS)
Od JDK 9 działają moduły Java:
- optymalizacja
- mniejszy footprint
- lepszy packaging
No i wkurwiają wszystkich.


