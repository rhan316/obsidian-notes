### CPU - Central Processing Unit
"Mózg komputera" - uniwersalny, wszechstronny, elastyczny.

| Cecha        | Opis                                                                         |
| ------------ | ---------------------------------------------------------------------------- |
| Zadanie      | Obsługa logiki programu, systemu operacyjnego, operacji sekwencyjnych        |
| Budowa       | Kilka rdzeni (2-64), bardzo złożonych, bardzo szybkich                       |
| Typ obliczeń | Seryjne (sekwencyjne), np. `if`, `while`, I/O, planowanie zadań              |
| Cache        | Duży, wielopoziomowy cache (L1, L2, L3)                                      |
| Zastosowanie | Systemy operacyjne, logika gier, przeglądarki, zarządzenie pamięcią          |
| Elastyczność | Ogólnego przeznaczenia - świetnie radzi sobie z wieloma różnymi typami zadań |
#### GPU - Graphics Processing Unit
"Silnik równoległy" - zaprojektowany do wykonywania masowo równoległych obliczeń

| Cecha        | Opis                                                                                           |
| ------------ | ---------------------------------------------------------------------------------------------- |
| Zadanie      | Wykonywanie tysięcy takich samych operacji równoległe (np. na pikselach, neuronach, wektorach) |
| Budowa       | Tysiące prostych rdzeni (np. 10_000+ CUDA cores w NVIDIA)                                      |
| Typ obliczeń | Równoległe (SIMD - Single Instruction Multiple Data)                                           |
| Cache        | Mały, zoptymalizowany lokalnie                                                                 |
| Zastosowanie | Grafika 3D, AI, symulacje fizyczne, obliczenia naukowe (CUDA, OpenCL, Vulkan)                  |
| Elastyczność | Wysoka przepustowość, ale mniej elastyczny od CPU w logice sterującej                          |
Rysowanie 4 milionów pikseli => GPU (każdy rdzeń liczy 1 piksel).
Kompresja ZIP, logika aplikacji => CPU (precyzyjność, kontrola)

