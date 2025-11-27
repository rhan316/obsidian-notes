**GraalVM** to nowoczesna maszyna wirtualna (JVM) od Oracle, zaprojektowana do:
- Szybszego uruchamiania aplikacji niż standardowa JVM
- Lepszej wydajności w czasie działania (JIT Compiler)
- Uruchamiania wielu języków programowania (Java, Kotlin, JavaScript, Ruby, R itp.)
- Tworzenie natywnych obrazów binarnych `Native Image`, które nie wymagają JVM i działają błyskawicznie.


| Zastosowanie                                                           | Korzyści                                        |
| ---------------------------------------------------------------------- | ----------------------------------------------- |
| Optymalizacja wydajności Javy                                          | Szybsze wykonywanie kodu dzięki komplilacji JIT |
| Kompilacja do natywnych binarek `Native Image`                         | Szybsze uruchamianie i mniejsze zużycie pamięci |
| Lepsza wydajność w mikrousługach `Spring Boot`, `Quarkus`, `Micronaut` | Skrócony czas startu, mniejsze zużycie RAM      |
| Uruchamianie wielu języków na jednej VM                                | Java, JS, Python, Ruby, R, LLVM (c, c++)        |
| Optymalizacja AI/ML i Big Data                                         | Obsługuje JIT dla języków analizy danych        |
**Jak działa GraalVM?**

Just-In-Time Comiler (JIT) - optymalizacja wydajności w locie.
GraalVM zastępuje domyślny kompilator JIT w JVM.
Optymalizuje kod podczas jego wykonywania, eliminując niepotrzebne instrukcje.

Native Image - kompilacja do natywnych binarek
Zamiast uruchamiać kod na JVM, GraalVM kompiluje go do pliku wykonywalnego `.exe`, `.bin`.
Nie wymaga JVM do działania -aplikacja startuje nawet 10x szybciej!
Idealne do mikrousług (spring-boot, Quarkus, micronaut).

### GraalVM = alternatywna implementacja JVM
Nie niszczy klasycznej JVM, nie zastępuje jej siłą, nie odpina kabelków.
Po prostu... jest inną wersją, z innymi zestawem bajerów.

To jak:
- OpenJDK - zwykła wersja
- Oracle HotSpot - popularna wersja
- GraalVM - szybka wersja z magicznymi sztuczkami

### Minusy:
- Kompilacja natywna trwa bardzo długo.
- Musisz dodać "native hints", bo refleksja i dynamiczna magia często nie działa.
- Debugowanie natywnego kodu może być upierdliwe.

### Kiedy używać?
- mikroserwisy
- CLI tools
- Serverless
- Wszystko, co musi startować szybko
