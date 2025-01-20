1. ApplicationContext: Interfejs Spring IoC, odpowiada za tworzenie, konfigurowanie i łączenie beanów na podstawie metadanych konfiguracji (np. klasy z adnotacjami, klasy konfiguracji, pliki XML, skrypty Groovy)
2. Implementacje ApplicationContext:
	1. AnnotationConfigApplicationContext i ClassPathXmlApplicationContext są popularne w aplikacjach stand-alone
	2. W aplikacjach webowych lub Spring Boot, kontener tworzy się automatycznie, bez kodu inicjującego
3. Metadane konfiguracji:
	1. Java-based - konfiguracja poprzez klasy @Configuration i metody @Bean
	2. XML-based - definicje beanów jako elementy <bean/> wewnątrz <beans/>, konfiguracja przez atrybuty id, class, property
	3. Groovy DSL - alternatywa dla XML, oferująca definiowanie beanów w plikach .groovy
4. Korzystanie z ApplicationContext:
	1. getBean pozwala na pobieranie skonfigurowanych beanów
	2. Możliwość łączenia XML, Groovy i innych źródeł konfiguracji
	3. W aplikacjach, dzięki wstrzykiwaniu zależności (DI), zalecane jest unikanie bezpośrednich wywołań getBean()