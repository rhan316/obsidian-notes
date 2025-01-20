Spring Framework intensywnie wykorzystuje refleksję do realizacji wielu swoich funkcji, takich jak:
1. **Dependency Injection (wstrzykiwanie zależności)** Spring używa refleksji do dynamicznego tworzenia instancji obiektów i wstrzykiwania ich do odpowiedniego miejsca.
2. **Adnotacje** Spring odczytuje adnotacje z klas, metod i pól, aby dowiedzieć się, jakie komponenty, konfiguracje i zachowania powinny być zastosowane.
3. **AOP (Aspect - Oriented Programming)** Dzięki refleksji Spring potrafi modyfikować zachowanie metod podczas ich wywoływania (np. dodanie logiki przed/po metodzie).
4. **Dynamicznie konfiguracja Beanów** Spring interpretuje klasy i metody zdefiniowane w konfiguracji, aby tworzyć i zarządzać obiektami.

***Wstrzykiwanie zależności (Dependency Injection)***
Gdy używasz Springa do wstrzykiwania zależności za pomocą takich jak `@Autowired`, Spring korzysta z refleksji, aby:
1. Zidentyfikować, które pola (lub konstruktory) wymagają wstrzyknięcia.
2. Utworzyć instancję wymaganych klas (lub znaleźć istniejące beany w kontenerze).
3. Wstrzyknąć odpowiedni obiekt w oznaczone pole.

***Odczytywanie adnotacji (metadanych)***
Spring interpretuje adnotacje na klasach, polach, metodach i konstruktorach, aby dowiedzieć się, jak konfigurować aplikację.

***Modyfikowane zachowanie metod - AOP***
Spring AOP (Aspect-Oriented Programming) to potężny mechanizm, który pozwala modyfikować zachowanie metod bez zmiany ich kodu. Jest używany do takich zadań, jak:
- logowanie
- obsługa wyjątków
- transakcyjność

***Dynamiczne tworzenie Beanów***
Spring interpretuje klasy z adnotacjami takimi jak `@Component`, `@Service`, czy metody oznaczone `@Bean`, aby dynamicznie tworzyć obiekty i zarządzać ich cyklem życia.