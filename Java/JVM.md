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