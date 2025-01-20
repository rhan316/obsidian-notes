Zastosowanie => Umożliwia przetwarzanie dużych ilości danych bez interakcji z użytkownikiem, np. przy okresowych operacjach biznesowych, jak miesięczne obliczenia czy integracja danych.

Przeznaczenie => Dedykowany do przetwarzania wsadowego w przedsiębiorstwach, ale nie jest narzędziem do planowania zadań - współpracuje z istniejącymi harmonogramami (np. Quartz, Tivoli).

Funkcje => Oferuje funkcje do zarządzania dużymi zbiorami danych, w tym logowanie, zarządzanie transakcjami, statystyki, ponowne uruchomienie zadań, pomijanie błędów i zarządzanie zasobami. Umożliwia też wysoką skalowalność i optymalizację.

Tło => Spring Batch powstał we współpracy firm Accenture i SpringSource w celu standaryzacji architektury wsadowej opartej na Javie. W odpowiedzi na potrzebę ujednoliconego rozwiązania wsadowego, Accenture wniosło swoje doświadczenia i rozwiązania, pomagając w rozwinięciu projektu.

Scenariusze użycia => Typowy program wsadowy czyta dane, przetwarza je i zapisuje w zmodyfikowanej formie. Spring Batch obsługuje m.in. przetwarzanie równoległe, etapowe, wielowątkowe oraz restart po błędach.

Scenariusz biznesowe => Obsługuje przetwarzanie wsadowe z częstym zatwierdzeniem transakcji, restart manualny lub automatyczny po błędach oraz przetwarzanie sekwencyjne lub równoległe.

Cele techniczne => Uławia korzystanie z modelu programowania Spring, rozdziela warstwy infrastruktury, udostępnia podstawowe usługi oraz łatwość w konfiguracji i rozszerzaniu przy użyciu Springa.




