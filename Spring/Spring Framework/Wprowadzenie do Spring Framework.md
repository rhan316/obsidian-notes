Inversion of Control (IoC) => W Spring IoC donosi się do procesu, w którym kontener przejmuje odpowiedzialność za zarządanie zależnościami obiektów (beanów). Obiekty nie tworzą bezpośrednio swoich zależności, zamiast tego kontener je "wstrzykuje"

Dependency Injection (DI) => Specjalna forma IoC, w której zależności obiektów są definiowane przez:
	- argumenty konstruktora (preferowane)
	- argument metody fabrycznej
	- właściwości ustawiane po utworzeniu obiektu

Pakiety Spring =>
	- org.springframework.bean i org.springframework.context stanowią podstawę kontenera IoC
	- BeanFactory oferuje zaawansowane mechanizmy konfiguracji dla zarządzania obiektami
	- ApplicationContext rozszerza BeanFactory i dodaje:
		- Integracje z AOP
		- Obsługę zasobów (np. do internacjonalizacji)
		- Publikowanie zdarzeń
		- Konteksty aplikacyjne (np. WebApplicationContext dla aplikacji webowych)

Bean =>
	Obiekt zarządzany przez kontener Spring IoC. Każdy bean jest instancjonowany, składany i kontrolowany przez kontener, a zależności między nimi są definiowane są w metadanych konfiguracji kontenera

ApplicationContex vs BeanFactory =>
	ApplicationContext to rozszerzenie BeanFactory, zawierające funkcje dedykowane dla rozwiązań korporacyjnych i jest głównie używany do opisów kontenera IoC w Spring 
