W Spring Boot (i ogólnie w Spring Framework) context to centralny kontener, który zarządza cyklem życia i konfiguracją beanów w aplikacji. Jest to implementacja wzorca Inversion of Control (IoC) i działa jako fundament aplikacji, obsługując tworzenie, zarządzanie oraz wstrzykiwanie zależności.

Spring Boot automatycznie konfiguruje różne konteksty w zależności od rodzaju aplikacji:
1. **ApplicationContext** 
 - To główny kontener Spring, który przechowuje wszystkie obiekty (beany) i zarządza nimi.
 - W Spring Boot implementacją tego interfejsu jest zazwyczaj **AnnotationConfigApplicationContext** lub **WebApplicationContext**.
2. **WebApplicationContext**
- Specjalny typ ApplicationContext dla aplikacji webowych
- Obsługuje komponenty MVC (np. kontrolery) i integruje się z serwletami (np. DispatcherServlet)
- W Spring Boot ładowany automatycznie dla aplikacji webowych
3. **Root Application Context i Servlet Application Context**
- Root Application Context => Zawiera ogólne beany, np. serwisy, konfiguracja bazy danych. Tworzony przez ContextLoaderListener
- Servlet Application Context => Specyficzny dla DispatcherServlet. Obsługuje kontrolery, mapowania, widoki itp. Działa w hierarchii, dziedzicząc beany z Root Application Context